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
![[Flow_Chart.png]]

**Kode**



Arduino IDE
Instalasi
Software Arduino IDE bisa didownload melalui: https://www.arduino.cc/en/software/, pilih sesuai dengan OS yang terinstall. Khusus untuk Windows 8 kebawah hanya bisa menginstall versi Legacy IDE (1.8.19).
Proses instalasi bata OS Linux berbeda tiap Distro menyesusaikan package manager yang terinstall, apt install arduino (debian), yay -S adruino (arch), zypper install arduino (opensuse) atau dnf install arduino (rhel) akan menginstall versi 1.8.19. Untuk menginstall versi 2++ bisa menggunakan Flatpak. Setup: https://flatpak.org/setup/, instalasi: flatpak install flathub cc.arduino.IDE2

Driver
Pada OS Windows perlu dilakukan instalasi driver hardware untuk bisa digunakan, secara umum ESP32, Arduino dan Raspberry Pi menggunakan chip CH340/CH341 atau CP210x.
CH340/CH341
Download file di: https://cdn.sparkfun.com/assets/learn_tutorials/8/4/4/CH341SER.EXE
Buka file CH341SER.EXE, kemudian klik Install.
![[CH340.png]]
CP210x
Download file di: https://www.silabs.com/documents/public/software/CP210x_Windows_Drivers.zip
Ekstrak file zip hasil download
Buka folder
Instalasi file CP210xVCPInstaller_x64.exe

Install Board
Buka Arduino IDE, klik 'File' kemudian 'Preferences', pada bagian 'Additional boards manager URLs' isi dengan link berikut.
http://arduino.esp8266.com/stable/package_esp8266com_index.json,https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
Tutup pop up 'Preferences', 
![[Instalasi_Board.png]]
Klik submenu bagian kiri urutan ke-2, kemudian search boards yang akan diinstall, contoh ESP32, maka akan muncul board ESP32 kemudian klik Install.

Board berguna untuk 

Install Library
![[Install_Library.png]]
Sama seperti proses instalasi board, proses instalasi library dilakukan di submenu Library Manager, kemudian cari library yang akan diinstall lalu klik install.


Compile/Upload




