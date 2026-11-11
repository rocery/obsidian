saya memiliki task scheduler di windows
C:\xampp\php\php.exe -f C:\xampp\htdocs\bp_hco\index.php tes_xml/read_all1/

14 bw015AU

sudo dd if=~/Downloads/AMDM/Windows 8.1 AIO November 2020 x64_1.iso of=/dev/sdb1 bs=4M status=progress conv=fsync


sudo chown -R admin_219:www-data /var/www/html/autosendTerlambat
sudo find /var/www/html/autosendTerlambat -type d -exec chmod 2775 {} \;
sudo find /var/www/html/autosendTerlambat -type f -exec chmod 664 {} \;


- BPHCO 1 - DAILY 17:30 - -f C:\xampp\htdocs\bp_hco\index.php tes_xml/read_all/1
- BPHCO 2 - DAILY 18:00 - -f C:\xampp\htdocs\bp_hco\index.php tes_xml/create_all_from_orlan/1
+ HABIS KONTRAK HRD - TGL 4 SETIAP BULAN 10.00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\mailHabisKontrak\index.php
+ HABIS KONTRAK PSN - SETIAP HARI KAMIS 10.00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\mailHabisKontrak\IMMonitoringKontrakREAL.php
+ STOCK SPAREPART - DAILY 08:00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\mailsparepart\index.php
+ ABSENSI - TGL 4 SETIAP BULAN 10.00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\mailAbsen\index.php
+ CEKLIS KENDARAAN - DAILY 15:00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\mailCeklistKendaraan\index.php
+ TERLAMBAT - DAILY - 10.00 - C:\xampp\php\php.exe -f C:\xampp\htdocs\autosendTerlambat\autosend_terlambat.php



mysqldbcopy \
  --source=admin:itbekasioke@192.168.10.223 \
  --destination=admin:itbekasioke@192.168.10.223 \
  counter_hit:counter_hit_test --force --verbose
  

mysql -h 192.168.10.223 -u admin -p -e \
"CREATE DATABASE IF NOT EXISTS counter_hit_test;"

mysqldump -h 192.168.10.223 -u admin -p \
  --single-transaction \
  --routines \
  --triggers \
  counter_hit | \
mysql -h 192.168.10.223 -u admin -p counter_hit_test --verbose