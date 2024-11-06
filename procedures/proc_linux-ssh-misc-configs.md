# Linux SSH/Docker/Python/Git

## Modify Ubuntu 22.04 IP Address Configuration
---
sudo nano /etc/netplan/00-installer-config.yaml
set IP address configuration
sudo netplan apply

### Modify Ubuntu 22.04 Hostname Configuration
---
sudo hostnamectl set-hostname host.domain

## Install CIFS:
sudo apt install cifs-utils

### Persistent connection to specific share
---
sudo mkdir /media/<mount-name>
nano .smbcredentials
username=<username>
password=<password>>
chmod 600 ~/.smbcredentials
sudo nano /etc/fstab
//<server-ip>/<server-share> /media/<mount-name> cifs credentials=/home/<username>/.smbcredentials,vers=2.0,iocharset=utf8,uid=1000,gid=1000 0 0
sudo mount -a

## Configure Putty and Linux for SSH Key-pair Authentication
---
ssh keypair:
https://shuaiber.medium.com/setting-up-ssh-connection-to-ubuntu-from-windows-using-putty-public-key-based-authentication-51ead6fbcc8a

### Run Puttygen
No of Bits: 2048
Generate
Randomise cursor movements
Save private key as id_rsa.ppk to local machine
Copy public key to clipboard

### Linux Public key for pasting into OpenSSH authorized_keys file
ssh-rsa <public-key-removed-for-privacy> <keyfile-name>

### Linux System
cd ~/.ssh
nano authorized_keys
Paste public key
Save/Exit
chmod 600 ~/.ssh/authorized_keys

### Local System Putty
Session
Enter Server IP address
Connection > SSH > Auth > Credentials
Browse > Private Key
Locate id.rsa.ppk > Open
Session > Type an identifying name > Save
Open > Login to server with key pair authentication

### Linux Enable SSH Server
sudo apt install openssh-server
sudo systemctl status ssh
sudo systemctl start ssh
sudo systemctl status ssh
sudo systemctl enable ssh

# Add current user to docker security group
---
sudo groupadd docker
sudo gpasswd -a $USER docker
sudo usermod -aG docker $(whoami)
restart

## Docker
docker info
docker run hello-world
	docker ps

# Python
sudo apt install python3-pip -y
pip3 install -U netmiko
pip3 install -U napalm
pip3 install -U simplejson
python3 --version
pip3 list

# Git
cd /path/to/local/git/repo
git status
