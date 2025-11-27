Komponen Elektroik
ESP32
Mikrokontroler yang digunakan dalam proyek ini adalah **ESP32**, dipilih karena telah dilengkapi modul WiFi terintegrasi pada board. Terdapat banyak varian ESP32 di pasaran; model yang digunakan pada proyek ini adalah **ESP32 DOIT/Dev Kit V1 (30 pin)**. Meskipun demikian, varian ESP32 lainnya secara umum tetap kompatibel untuk implementasi serupa.
Konfigurasi pin yang digunakan adalah sebagai berikut:
- **I2C:** SCL pada pin **22** dan SDA pada pin **21** untuk koneksi LCD
- **DHT21:** pin **33** atau **14**
- **VIN** dan **GND** untuk suplai daya
ESP32 memiliki batas maksimum tegangan input sebesar **5.5 V DC**. Pemberian tegangan melebihi batas tersebut akan menyebabkan komponen internal mengalami panas berlebih (overheat) dan berpotensi merusak IC, sehingga perangkat tidak dapat digunakan kembali.

DHT21 AM2301
DHT21 atau AM2301 merupakan sensor suhu dan kelembapan dengan keluaran berupa sinyal digital. Sensor ini memiliki tiga pin yang perlu dihubungkan ke ESP32, yaitu:
- **VCC (merah)** dihubungkan ke **VIN**
- **GND (hitam)** dihubungkan ke **GND**
- **DATA (kuning)** dihubungkan ke pin **14** atau **33**

Spesifikasi teknis sensor:
- **Tegangan input:** 3.5 V – 5 V
- **Rentang kelembapan:** 0 – 100% RH
- **Rentang suhu:** −40°C – 80°C
- **Akurasi:** ±3% RH dan ±0.5°C
Sensor ini digunakan untuk memperoleh data suhu dan kelembapan secara real-time dan dapat diintegrasikan secara langsung dengan ESP32 melalui pin digital.

LCD 16x2 I2C
LCD 16x2 dapat terdiri dari 16 kolom dan 2 baris karakter. Membutuhkan input 5V. Pin SCL di LCD dihubungkan ke pin SCL di ESP32 dan pin SDA dihubungkan ke pin SDA ESP32.

LM2596
Digunakan untuk menurunkan tegangan dari adaptor, contoh menurunkan tegangan dari 12V ke 5V DC. Nilai hasil penuruan tegangan dikontrol oleh trimpod (baut emas) pada board LM2596. 

PCB Dot Matrix
Tempat menghubungan antar komponen elektronik. Proses penghubungan menggunakan solder agar lebih kuat.

Adaptor 12V 1A
Sumber arus listrik. Penggunaan adaptor tidak harus 12V, tapi setidaknya 5V sesuai kebutuhan ESP32 dan komponen listrik lainnya. Untuk nilai arus direkomendasikan minimal 1A.

Box x4
Box dengan ukuran 12.5CM x 8.5CM x 5CM

Kabel JST 2, 3 dan 4 Pin
JST 2 Pin : Penghubung dari LM2596 ke PCB
JST 3 Pin : Penghubung DHT21 ke PCB
JST 4 Pin : Penghubung LCD ke PCB

**Diagram Elektronik**
![[Diagram Elektronik.png]]

**Flow Chart**
![[Flow_Chart.png]]

**Kode**
https://github.com/rocery/arduino/blob/master/9.%20Suhu%20Ruangan/DHT21_Template/DHT21_Template.ino









