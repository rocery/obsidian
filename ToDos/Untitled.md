usb_orlan
"tJr*5k8gV7<$3]^mHu"

it_bekasi
_Yi5V5$8e6\%znj#r/


BAGIAN 1: Instalasi Gitea di Server 225 (Debian)
1.1 Persiapan Server
bashssh user@192.168.10.225

# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt install -y git curl wget

# Buat user khusus gitea
sudo adduser --system --shell /bin/bash --gecos 'Gitea' --group --disabled-password --home /home/gitea gitea

# Buat direktori yang dibutuhkan
sudo mkdir -p /var/lib/gitea/{custom,data,log}
sudo chown -R gitea:gitea /var/lib/gitea/
sudo chmod -R 750 /var/lib/gitea/

sudo mkdir /etc/gitea
sudo chown root:gitea /etc/gitea
sudo chmod 770 /etc/gitea
1.2 Download & Install Gitea
bash# Download gitea (cek versi terbaru di https://dl.gitea.com/gitea/)
wget https://dl.gitea.com/gitea/1.22.6/gitea-1.22.6-linux-amd64 -O gitea

# Install
sudo mv gitea /usr/local/bin/gitea
sudo chmod +x /usr/local/bin/gitea

# Verifikasi
gitea --version
1.3 Setup Database (SQLite - simple untuk tim kecil)
SQLite sudah built-in, tidak perlu install tambahan.

Jika tim besar, gunakan MySQL/PostgreSQL.

1.4 Buat Systemd Service
bashsudo nano /etc/systemd/system/gitea.service
Isi file:
ini[Unit]
Description=Gitea
After=network.target

[Service]
RestartSec=2s
Type=simple
User=gitea
Group=gitea
WorkingDirectory=/var/lib/gitea/
ExecStart=/usr/local/bin/gitea web --config /etc/gitea/app.ini
Restart=always
Environment=USER=gitea HOME=/home/gitea GITEA_WORK_DIR=/var/lib/gitea

[Install]
WantedBy=multi-user.target
bashsudo systemctl daemon-reload
sudo systemctl enable gitea
sudo systemctl start gitea

# Cek status
sudo systemctl status gitea
1.5 Setup Awal via Browser
Buka: http://192.168.10.225:3000
Isi form instalasi:
FieldValueDatabaseSQLite3Site URLhttp://192.168.10.225:3000Repository Root/home/gitea/repositoriesRun AsgiteaHTTP Port3000
Klik Install Gitea, lalu register akun admin.

BAGIAN 2: Setup Repository di Gitea
2.1 Buat Organization & Repository
Di http://192.168.10.225:3000:
1. Login sebagai admin
2. Buat Organization: sttbekasi (opsional)
3. Buat Repository baru:
   - Name: project-web
   - Visibility: Private
   - JANGAN centang "Initialize repository"
4. Catat URL repo: http://192.168.10.225:3000/sttbekasi/web-app.git
2.2 Tambah User Tim
Admin → Site Administration → User Accounts → Create User Account
Buat akun untuk setiap anggota tim

BAGIAN 3: Push File dari Debian 219
bashssh user@192.168.10.219

cd /var/www/html

# Inisialisasi git
git init

# Buat .gitignore (sesuaikan kebutuhan)
cat > .gitignore << 'EOF'
*.log
*.tmp
.env
config/database.php
EOF

# Set identitas git
git config user.name "Server Debian"
git config user.email "debian@192.168.10.219"

# Add semua file & commit
git add .
git commit -m "initial: semua file dari debian /var/www/html"

# Tambah remote & push ke branch main
git remote add origin http://192.168.10.225:3000/sttbekasi/web-app.git
git checkout -b main
git push -u origin main

BAGIAN 4: Push File dari Windows 252
Buka Git Bash di C:/xampp/htdocs:
bashcd C:/xampp/htdocs

# Inisialisasi git
git init

# Buat .gitignore
cat > .gitignore << 'EOF'
*.log
*.tmp
.env
config/database.php
EOF

# Set identitas git
git config user.name "Server Windows"
git config user.email "windows@192.168.10.252"

# Add semua file & commit
git add .
git commit -m "initial: semua file dari windows c:/xampp/htdocs"

# Tambah remote & push ke branch windows
git remote add origin http://192.168.10.225:3000/sttbekasi/web-app.git
git remote set-url origin windows-acc@192.168.10.225:sttbekasi/windows.git
git remote set-url origin http://192.168.10.225:3000/sttbekasi/windows.git
git remote set-url origin admin_225@192.168.10.225:sttbekasi/windows.git
git checkout -b windows
git push -u origin windows

BAGIAN 5: Setup di Komputer Developer
5.1 Clone Repository
bash# Clone branch main (untuk develop file Debian)
git clone -b main http://192.168.10.225:3000/sttbekasi/web-app.git project-debian

# Clone branch windows (untuk develop file Windows)
git clone -b windows http://192.168.10.225:3000/sttbekasi/web-app.git project-windows

# Atau clone semua branch sekaligus
git clone http://192.168.10.225:3000/sttbekasi/web-app.git project-web
cd project-web
git checkout main     # pindah ke branch main
git checkout windows  # pindah ke branch windows
5.2 Set Identitas Developer
bashcd project-debian  # atau project-windows
git config user.name "Nama Developer"
git config user.email "email@domain.com"

BAGIAN 6: Contoh Workflow Harian
Pull (ambil perubahan terbaru)
bashcd project-debian
git checkout main
git pull origin main
Coding & Push Langsung (tim kecil / tanpa review)
bash# Pastikan di branch yang benar
git checkout main        # untuk file Debian
# atau
git checkout windows     # untuk file Windows

# Setelah coding...
git status               # lihat file yang berubah
git diff                 # lihat detail perubahan
git add .                # staging semua file
# atau spesifik file:
git add index.php login.php

git commit -m "fix: perbaikan form login"
git push origin main     # atau windows
Workflow dengan Feature Branch (tim dengan review)
bash# Buat branch fitur dari main
git checkout main
git pull origin main
git checkout -b feature/halaman-produk

# Coding...
git add .
git commit -m "feat: tambah halaman produk"
git push origin feature/halaman-produk

# Buka Gitea → buat Pull Request → minta review
# Setelah di-merge, hapus branch lokal
git checkout main
git pull origin main
git branch -d feature/halaman-produk
Sinkronisasi Perubahan Antar Developer
bash# Developer A push perubahan
# Developer B ambil perubahan tersebut
git pull origin main

# Jika ada conflict
git pull origin main
# Edit file yang conflict (tandai <<<<<< dan >>>>>>)
git add file-yang-conflict.php
git commit -m "fix: resolve conflict"

BAGIAN 7: Auto-Deploy ke Server (Opsional)
Install webhook di 219 & 252
Di Debian 219:
bashsudo apt install -y webhook

# Buat script deploy
sudo mkdir -p /opt/deploy
sudo nano /opt/deploy/deploy.sh
bash#!/bin/bash
cd /var/www/html
git pull origin main
bashsudo chmod +x /opt/deploy/deploy.sh

# Buat konfigurasi webhook
sudo nano /etc/webhook.conf
json[
  {
    "id": "deploy-debian",
    "execute-command": "/opt/deploy/deploy.sh",
    "command-working-directory": "/var/www/html"
  }
]
bashsudo systemctl enable webhook
sudo systemctl start webhook
Di Gitea UI:
Repository → Settings → Webhooks → Add Webhook → Gitea
URL: http://192.168.10.219:9000/hooks/deploy-debian
Trigger: Push events → branch: main

Ringkasan Perintah Penting
PerintahFungsigit clone -b main <url>Clone branch tertentugit pull origin mainAmbil perubahan terbarugit push origin mainUpload perubahangit statusLihat status filegit log --onelineLihat history commitgit checkout -b feature/xxxBuat branch fitur barugit branch -aLihat semua branchgit diffLihat detail perubahan
