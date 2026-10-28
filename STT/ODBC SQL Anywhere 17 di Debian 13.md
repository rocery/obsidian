# ODBC SQL Anywhere 17 di Debian 13

Lingkungan: Debian 13 (Trixie), Apache2, PHP 5.6 (mod_php), PHP 8.5 (php-fpm + apache2), PHP 8.2 (server test).

## 1. Install

### Paket dasar

```bash
sudo apt update
sudo apt install -y unixodbc unixodbc-dev odbcinst
# opsional, driver lama (FreeTDS)
# FreeTDS memiliki banyak kekurangan dalam mengeksekusi kompleks query, digunakan untuk pengetesan atau untuk projek sederhana
sudo apt install -y tdsodbc freetds-bin freetds-common
```

### Client SQL Anywhere 17 (driver native)

```bash
Download SQLAnywhere 17 (Pilih 1):
https://drive.google.com/file/d/1oRiKRpHPgUbp1RFERgA0eZR_LAAWqw6e/view?usp=sharing (recomended)
atau:
https://github.com/rocery/sqlanywhere17

copy filke sqla17_client_linux_x86x64.tar.gz ke server

sudo ./setup -nogui setelah menjalankan shell ini, instalasi driver dijalankan.
Set value instalasi secara default
```

```bash
tar xzf sqla17_client_linux_x86x64.tar.gz
cd client17011/
sudo ./setup -nogui          # default: /opt/sqlanywhere17

echo /opt/sqlanywhere17/lib64 | sudo tee /etc/ld.so.conf.d/sqlanywhere17.conf
sudo ldconfig
ldd /opt/sqlanywhere17/lib64/libdbodbc17_r.so | grep "not found"
```
Jika `libtinfo.so.5` hilang:

```bash
sudo ln -s /usr/lib/x86_64-linux-gnu/libtinfo.so.6 /usr/lib/x86_64-linux-gnu/libtinfo.so.5
```

### Ekstensi PHP

```bash
sudo apt install -y php8.x-odbc          # 8.x
sudo apt install -y php5.6-odbc          # 5.6 (repo sury)
```

## 2. Konfigurasi

### /etc/odbcinst.ini

```ini
[SQL Anywhere 17]
Description = SQL Anywhere 17 native
Driver = /opt/sqlanywhere17/lib64/libdbodbc17_r.so
```

### /etc/odbc.ini

```ini
[dblive]
Driver = SQL Anywhere 17
ServerName = dblive
DatabaseName = dblive
UserID = dba
Password = <password>
CommLinks = tcpip(host=IP_SERVER_DB;port=2638)
```

Jika ada, entri FreeTDS lama di-comment. Opsi `TDS_Version`, `TextSize`, `AnsiNPW`, dan `QuotedId` tidak dipakai lagi.

### Environment (kunci utama)

Driver SQL Anywhere tidak membaca `/etc/odbc.ini` tanpa `ODBCINI`. Tanpa itu muncul error `DSN 'dblive' does not exist`.

| Konteks                  | Tempat set                                                                                                              |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| Shell semua user         | `/etc/profile.d/odbcini.sh` berisi `export ODBCINI=/etc/odbc.ini`, plus `source /opt/sqlanywhere17/bin64/sa_config.sh`. |
| Apache mod_php (PHP 5.6) | `/etc/apache2/envvars`                                                                                                  |
| php-fpm 8.5 / 8.2        | `/etc/php/<versi>/fpm/pool.d/www.conf`                                                                                  |

Shell user, jalankan:

```bash
echo 'export ODBCINI=/etc/odbc.ini' | sudo tee /etc/profile.d/odbcini.sh
```

Isi untuk Apache `envvars` dibaris paling bawah:

```ini
export ODBCINI=/etc/odbc.ini
export SQLANY17=/opt/sqlanywhere17
export LD_LIBRARY_PATH=/opt/sqlanywhere17/lib64
```

Isi untuk pool php-fpm Isi untuk Apache `envvars` dibaris paling bawah:

```ini
env[ODBCINI] = /etc/odbc.ini
env[SQLANY17] = /opt/sqlanywhere17
env[LD_LIBRARY_PATH] = /opt/sqlanywhere17/lib64
```

Lalu `sudo systemctl restart apache2` atau `php<versi>-fpm`. Harus restart, bukan reload.

### Catatan per versi PHP

- **PHP 5.6**: dilayani lewat mod_php (`php5_module`), sehingga `php5.6-fpm` tidak dipakai. Edit: `sudo nano /etc/apache2/envvars`, bukan `www.conf`.
- **PHP 8++**: php-fpm untuk apache2. Edit: `sudo nano /etc/php/<versi>/fpm/pool.d/www.conf`

## 3. Tes

Urutan dari lapisan paling bawah ke atas.

1. **Driver tanpa DSN** (memastikan driver dan server beres):

    ```bash
    isql -v -k "Driver={SQL Anywhere 17};ServerName=dblive;DatabaseName=dblive;UserID=dba;Password=<password>;CommLinks=tcpip(host=IP;port=2638)"
    ```
    
2. **Dengan DSN**:
    
    ```bash
    export ODBCINI=/etc/odbc.ini
    isql -v dblive dba <password>
    ```
    
3. **PHP CLI**:
    
    ```bash
    php5.6 -r 'var_dump(odbc_connect("dblive","dba","<password>"));'   # resource(...) of type (odbc link)
    php8.2 -r 'var_dump(odbc_connect("dblive","dba","<password>"));'   # object(Odbc\Connection)
    ```
    
4. **Lewat web** (wajib, karena CLI tidak membuktikan environment web):
    
    ```bash
    echo '<?php $c=@odbc_connect("dblive","dba","<password>"); var_dump($c); echo odbc_errormsg(); echo "\nODBCINI=".getenv("ODBCINI");' | sudo tee /var/www/html/odbc_test.php
    curl http://localhost/odbc_test.php
    sudo rm /var/www/html/odbc_test.php
    ```
    

## 4. Troubleshooting

|Error|Penyebab|Solusi|
|---|---|---|
|`IM004 SQLAllocHandle ... failed`|Environment SQL Anywhere belum ada|`source sa_config.sh`, cek `ldd` dan `libtinfo.so.5`|
|`Parse error: DSN '...' does not exist` (08004)|`ODBCINI` kosong|`export ODBCINI=/etc/odbc.ini`|
|`IM002 Data source name not found`|Nama DSN salah atau tidak ada di `odbc.ini`|Cek nama section|
|CLI sukses, web `bool(false)`|Env belum ada di Apache atau fpm|Set di `envvars` atau `www.conf`, restart, cek `error.log`|
|`Permission denied`|`www-data` tidak bisa membaca|`chmod -R o+rX /opt/sqlanywhere17`, grup `www-data` untuk `odbc.ini`|

## 5. Catatan

- Alternatif tanpa bergantung environment: pakai connection string langsung, atau isi `dsn` di `database.php` CodeIgniter 3 dengan `Driver={SQL Anywhere 17};...`.
- Query yang mengandalkan perilaku FreeTDS/ASE (misalnya tipe `TEXT`) perlu diuji ulang.
- PHP 5.6 sudah EOL. Batasi aksesnya ke jaringan internal.
- `odbc.ini` berisi password teks biasa. Batasi dengan `chmod 640` dan grup yang sesuai.