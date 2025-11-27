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

Board berisi konfigurasi-konfigurasi dari microcontroller yang berbeda untuk dikenali Arduino IDE. Setiap pabrikan memiliki arsitektur dan cara pengkodean yang berbeda sehingga diperlukan board sebelum bisa digunakan.

Install Library
![[Install_Library.png]]
Sama seperti proses instalasi board, proses instalasi library dilakukan di submenu Library Manager, kemudian cari library yang akan diinstall lalu klik install.

Port
Setiap Microcontroller memiliki port yang berbeda, untuk melakukan pengaturan port pilih Tools => Port => Pilih port yang sesuai. Pada umumnya nama port diawali dengan kata USB.

Board
Untuk memilih board klik Tools => Board => pilih merk (misal esp32) => pilih microcontroller yang sesuai. Board ini harus sesuai dengan yang digunakan, jika berbeda kode tetap bisa di Upload tapi akan ada kesalahan logika kode.


Verify
Verify digunakan untuk mendeteksi kesalahan syntax pada kode. ika ada kesalahan penulisan, pemanggilan fungsi yang tidak dikenal, variabel yang tidak dideklarasikan, atau library yang hilang, proses ini akan menampilkan pesan error.



Upload
Upload pada Arduino IDE adalah proses untuk mengirimkan program (sketch) yang sudah berhasil dikompilasi/verify ke mikrokontroler.