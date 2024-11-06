# Greenbone Vulnerability Management

https://www.geeksforgeeks.org/installing-openvas-on-kali-linux/

Update the Kali Linux host system:
sudo apt update
sudo apt upgrade -y
sudo apt dist-upgrade -y

Run the installation process:
sudo apt install openvas

Begin the setup process:
gvm-setup

Wait for Network Vulnerability Tests (NVTs) to download
    this may take some time

Note the admin user password displayed on screen
The admin password can be changed using this command:
gvmd --user=admin --new-password=<new-password>;

Verify the installation:
gvm-check-setup

The web interface is available at https://localhost:9392
Enter the username: admin and password when prompted

The framework consumes a lot of resources so it is recommended to disable these services when not using OpenVAS.

To start the services:
sudo gvm-start

Wait until all services have confirmed running before accessing the web interface

To stop the services:
sudo gvm-stop

