# Nessus Essentials

https://www.tenable.com/products/nessus/nessus-essentials
Register for Nessus Essentials

https://www.tenable.com/downloads/nessus?loginAttempted=true
Version: Nessus 10.8.3
Platform: Linux-Ubuntu-amd64

sudo dpkg -i Nessus-10.8.3-ubuntu1604_amd64.deb
provide password

after successful installation:
sudo systemctl start nessusd.service
sudo systemctl enable nessusd.service
sudo systemctl status nessusd.service

browser:
https://kali:8834
at the warning:
Accept the Risk and Continue

At the Welcome window:
Continue
Select Nessus Essentials
Continue

At the activation code window:
Skip
Paste the code: EBBM-4MS4-2WFG-YHH3-SP37
Continue

Wait for Initialisation to complete
Nessus Essentials interface displays
Wait for Plugins to complete compiling
