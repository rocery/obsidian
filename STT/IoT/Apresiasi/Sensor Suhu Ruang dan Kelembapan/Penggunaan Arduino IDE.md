**Arduino IDE** 

**Instalasi**
Perangkat lunak Arduino IDE dapat diunduh melalui situs resmi Arduino, dengan pilihan versi yang disesuaikan dengan sistem operasi yang digunakan. Untuk Windows 8 ke bawah, instalasi hanya dapat dilakukan menggunakan _Legacy IDE_ versi 1.8.19.
Pada sistem operasi Linux, proses instalasi berbeda untuk setiap distribusi karena menyesuaikan _package manager_ yang digunakan. Perintah berikut dapat digunakan untuk memasang Arduino IDE versi 1.8.19:
- Debian/Ubuntu: `apt install arduino`
- Arch Linux: `yay -S arduino`
- openSUSE: `zypper install arduino`
- RHEL/CentOS/Fedora: `dnf install arduino`
Untuk menginstal Arduino IDE versi 2.x, dapat menggunakan Flatpak. Konfigurasi repositori Flatpak dilakukan melalui halaman _setup_ yang tersedia, kemudian instalasi Arduino IDE dilakukan dengan perintah berikut:
`flatpak install flathub cc.arduino.IDE2`

**Driver**
Pada sistem operasi Windows, diperlukan instalasi _driver_ perangkat keras agar dapat dikenali dan digunakan. Secara umum, ESP32, Arduino, dan Raspberry Pi menggunakan chip CH340/CH341 atau CP210x sebagai antarmuka USB-to-Serial.

**CH340/CH341**
Unduh _driver_ melalui tautan berikut:  
`https://cdn.sparkfun.com/assets/learn_tutorials/8/4/4/CH341SER.EXE`
Setelah selesai diunduh, buka berkas **CH341SER.EXE** kemudian pilih opsi **Install** untuk memulai proses pemasangan.
![[CH340.png]]
**CP210x**
Unduh _driver_ melalui tautan berikut:  
`https://www.silabs.com/documents/public/software/CP210x_Windows_Drivers.zip`
Ekstrak berkas `.zip` yang telah diunduh, kemudian buka folder hasil ekstraksi. Jalankan berkas **CP210xVCPInstaller_x64.exe** untuk memulai proses instalasi.
Pada sistem operasi Linux, _driver_ biasanya terpasang secara otomatis. Namun, apabila proses _upload_ program gagal, jalankan perintah berikut pada terminal untuk memberikan akses yang diperlukan: `sudo usermod -aG dialout $USER` 
Setelah menjalankan perintah tersebut, lakukan _logout_ atau restart sesi untuk menerapkan perubahan.

**Install Board**
Buka Arduino IDE, pilih menu **File → Preferences**. Pada bagian **Additional Boards Manager URLs**, masukkan tautan berikut pada kolom yang tersedia:
http://arduino.esp8266.com/stable/package_esp8266com_index.json,https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
Setelah selesai, tutup jendela **Preferences**.
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
![[Verify.png]]

Upload
Upload pada Arduino IDE adalah proses untuk mengirimkan program (sketch) yang sudah berhasil dikompilasi/verify ke mikrokontroler.
![[Upload.png]]