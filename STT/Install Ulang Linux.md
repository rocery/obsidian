Microsoft Edge
```
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft-edge.gpg > /dev/null  
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft-edge.gpg] https://packages.microsoft.com/repos/edge stable main" | sudo tee /etc/apt/sources.list.d/microsoft-edge.list
```

Apps
```
sudo apt update
sudo apt install openssh-server -y
sudo apt upgrade -y

sudo apt install vlc remmina remmina-plugin* smbc samba python3-smbc python-smbc smbclient system-config-samba microsoft-edge-stable synaptic

sudo apt autoremove
```

Etc
```
Add user itb (root)
sudo touch /etc/libuser.conf
```