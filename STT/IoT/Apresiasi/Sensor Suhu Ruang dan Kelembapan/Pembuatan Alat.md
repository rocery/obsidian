Komponen Elektroik
ESP32
Microcontroller yang digunakan, dipilih karena memiliki module WiFi bawaan pada board. ESP32 yang beredar memiliki banyak jenis, yang digunakan pada projek ini adalah ESP32 DOIT/Dev Kit V1 30 Pin, jenis ESP lain masih bisa digunakan pada projek ini. Pin yang digunakan: I2C (SCL Pin 22, SDA Pin 21) untuk LCD, Pin 33/14 untuk DHT21, VIN, GND. Nilai maksimal input tegangan untuk ESP32 adalah 5.5V DC. Jika kelebihan tegangan, IC pada ESP32 akan overheat kemudian rusak, tidak bis gunakan.

DHT21 AM2301
Sensor DHT21 merupakan sensor Suhu dan Kelembapan dengan output pin digital. Memiliki 3 pin yang perlu dihubungkan ke ESP32, yaitu: VCC (merah) dihubungkan ke VIN, GND (hitam) dihubungkan ke pin GND, dan pin DATA (kuning) dihubungkan ke pin 14/33
Input: 3.5V - 5V
Humidity: 0 - 100%
Temperature: -40°C - 80°C
Accuracy: ±3% RH, ±0.5 degrees C

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


**Kode**



Instalasi Arduino IDE



Install Library/Board



Compile/Upload




