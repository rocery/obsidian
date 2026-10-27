OS: Debian 13
Latest Update: 24-10-2026

### Install unixODBC (Driver Manager)
```
sudo apt update
sudo apt install -y unixodbc unixodbc-dev odbcinst
```

### Install driver database
FreeTDS:
```
sudo apt install -y tdsodbc freetds-bin freetds-common

- Add driver to /etc/odbcinst.ini
sudo nano /etc/odbcinst.ini
[FreeTDS]
Description = FreeTDS Driver
Driver = /usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so
Setup = /usr/lib/x86_64-linux-gnu/odbc/libtdsS.so
UsageCount = 1

- Add credetial to /etc/odbc.ini
sudo nano /etc/odbc.ini
[dblive]
Description = Sybase ASE Connection
Driver = FreeTDS
Servername = dblive
Database = dblive
UID = dba
PWD = apple
TDS_Version=5.0
UseServerSidePrepare=0
TextSize=64512
AnsiNPW=No
QuotedId=No

- Add host to /etc/freetds/freetds.conf
sudo nano /etc/freetds/freetds.conf
[dblive]
    host = 192.168.10.255
    port = 2638
    tds version = 5.0
    database = dblive
    text size = 64512
    
- Test
tsql -S dblive -U user -P password
isql -v dblive user passowrd
odbcinst -q -d

- Test PHP
php -r '$c = odbc_connect("dblive","dba","apple"); var_dump($c);'
If the result `resource`/`object(Odbc\Connection)` it'r working
```
SQL Anywhere 17:
```
Download file sqla17_client_linux_x86x64.tar.gz
tar -xzf sqla17_client_linux_x86x64.tar.gz
cd client17011
sudo ./setup -nogui
Choose default option, don't make custom config while instalation progress

Add library to linker, important for php-fpm 
echo /opt/sqlanywhere17/lib64 | sudo tee /etc/ld.so.conf.d/sqlanywhere17.conf
sudo ldconfig
ldd /opt/sqlanywhere17/lib64/libdbodbc17_r.so | grep "not found"
if "not found" install libtinfo and libncurses

Add driver to /etc/odbcinst.ini
[SQL Anywhere 17]
Description = SQL Anywhere 17 native
Driver = /opt/sqlanywhere17/lib64/libdbodbc17_r.so
```