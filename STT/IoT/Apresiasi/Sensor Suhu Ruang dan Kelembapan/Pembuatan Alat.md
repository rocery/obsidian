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

**LCD 16×2 I2C**  
LCD 16×2 merupakan modul tampilan yang mampu menampilkan 16 karakter per baris pada dua baris. Modul ini menggunakan antarmuka **I2C**, sehingga hanya memerlukan dua jalur komunikasi untuk terhubung dengan ESP32. Modul LCD membutuhkan suplai daya sebesar **5 V**.
Konfigurasi pin yang digunakan:
- **SCL** pada modul LCD dihubungkan ke pin **SCL (pin 22)** pada ESP32
- **SDA** pada modul LCD dihubungkan ke pin **SDA (pin 21)** pada ESP32
Dengan antarmuka I2C, penggunaan jumlah pin dapat diminimalkan sehingga integrasi dengan komponen lain menjadi lebih efisien.

**LM2596**  
LM2596 merupakan modul **buck converter** yang digunakan untuk menurunkan tegangan DC dari sumber daya yang lebih tinggi ke tegangan yang lebih rendah dan stabil. Contoh penggunaan umumnya adalah menurunkan tegangan dari **12 V DC** menjadi **5 V DC** untuk keperluan rangkaian elektronik.
Besaran tegangan keluaran dapat diatur melalui **trimpot** (potensiometer kecil berwarna emas) yang tersedia pada modul LM2596. Pengaturan ini memungkinkan penyesuaian tegangan sesuai kebutuhan perangkat yang akan disuplai.

**PCB Dot Matrix**  
PCB Dot Matrix berfungsi sebagai media untuk menghubungkan komponen elektronik dalam rangkaian. Proses penyambungan antar komponen dilakukan melalui penyolderan guna memastikan kekuatan dan keandalan koneksi.

**Adaptor 12 V 1 A**  
Adaptor ini berfungsi sebagai sumber daya utama bagi rangkaian. Meskipun nilai tegangan tidak harus 12 V, sumber harus menyediakan **minimal 5 V DC** untuk memenuhi kebutuhan ESP32 dan komponen pendukung lainnya. Arus keluaran yang direkomendasikan adalah **minimum 1 A** agar suplai daya tetap stabil.

**Box x4**  
Menggunakan kotak berukuran **12.5 cm × 8.5 cm × 5 cm** sebagai wadah untuk menempatkan rangkaian dan komponen secara terorganisir serta melindunginya dari faktor luar.

**Kabel JST 2, 3, dan 4 Pin**  
Jenis konektor JST yang digunakan dalam rangkaian adalah sebagai berikut:
- **JST 2 pin**: penghubung dari modul **LM2596** ke **PCB**
- **JST 3 pin**: penghubung **DHT21** ke **PCB**
- **JST 4 pin**: penghubung **LCD** ke **PCB**

**Diagram Elektronik**
![[Diagram Elektronik.png]]

**Flow Chart**
![[Flow_Chart.png]]

**Kode**
https://github.com/rocery/arduino/blob/master/9.%20Suhu%20Ruangan/DHT21_Template/DHT21_Template.ino









