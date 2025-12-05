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
Klik submenu di bagian kiri urutan kedua, kemudian cari _board_ yang ingin dipasang. Misalnya, ketik **ESP32**, maka daftar _board_ ESP32 akan muncul. Pilih _board_ tersebut lalu klik **Install** untuk memulai instalasi.
_Board_ berisi konfigurasi yang diperlukan agar Arduino IDE dapat mengenali dan berkomunikasi dengan mikrokontroler. Setiap pabrikan memiliki arsitektur dan metode pemrograman yang berbeda, sehingga instalasi _board_ diperlukan sebelum perangkat dapat digunakan.

**Install Library**
![[Install_Library.png]]
Instalasi _library_ dilakukan dengan cara yang serupa dengan instalasi _board_. Buka **Library Manager**, kemudian cari _library_ yang diperlukan dan klik **Install**.

**Port**  
Setiap mikrokontroler menggunakan port yang berbeda. Untuk mengatur port, pilih **Tools → Port**, lalu pilih port yang sesuai. Umumnya nama port diawali dengan kata _USB_.

**Board**  
Untuk memilih _board_, masuk ke menu **Tools → Board**, pilih merek (misalnya ESP32), kemudian pilih jenis mikrokontroler yang digunakan. _Board_ harus dipilih sesuai dengan perangkat yang digunakan. Jika berbeda, proses _upload_ mungkin tetap berjalan, tetapi dapat menyebabkan kesalahan logika pada program.

**Verify**  
Fitur _Verify_ berfungsi untuk mendeteksi kesalahan _syntax_ pada kode. Jika terdapat kesalahan penulisan, pemanggilan fungsi yang tidak dikenal, variabel yang belum dideklarasikan, atau _library_ yang tidak ditemukan, proses ini akan menampilkan pesan kesalahan (_error_).
![[Verify.png]]

**Upload**  
_Upload_ pada Arduino IDE merupakan proses pengiriman program (_sketch_) yang telah berhasil dikompilasi atau melalui tahap _verify_ ke dalam mikrokontroler, sehingga perangkat dapat menjalankan instruksi yang telah dituliskan.
![[Upload.png]]