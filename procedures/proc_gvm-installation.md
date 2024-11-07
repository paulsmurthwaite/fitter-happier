# Greenbone Vulnerability Management

https://www.geeksforgeeks.org/installing-openvas-on-kali-linux/

### Update the Kali Linux host system
```
sudo apt update
```
```
sudo apt upgrade -y
```
```
sudo apt dist-upgrade -y
```

### Install OpenVAS
```
sudo apt install gvm
```

### Begin the OpenVAS setup process
```
gvm-setup
```

- Wait for Network Vulnerability Tests (NVTs) to download (this may take some time)
- Note the admin user password displayed on screen
```
[*] Please note the password for the admin user
[*] User created with password 'XXXXXXXX'
```

### Errors relating to PostgreSQL cluster version upgrade
- https://greenbone.github.io/docs/latest/22.4/kali/troubleshooting.html

```
┌──(kali㉿kali)-[~]
└─$ sudo pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
16  main    5432 online postgres /var/lib/postgresql/16/main /var/log/postgresql/postgresql-16-main.log                                               
17  main    5433 online postgres /var/lib/postgresql/17/main /var/log/postgresql/postgresql-17-main.log
```

- Ensure the newer version is installed:
```
sudo apt install postgresql-17
```
```
sudo apt install postgresql-client-17
```

- Remove the later version cluster:
```
sudo pg_ctlcluster 17 main stop
```
```
sudo pg_dropcluster 17 main
```

- Upgrade the older version cluster:
```
sudo pg_upgradecluster 16 main
```

- After remaining GVM Setup remove older version cluster:
```
postgresql-16
```
```
postgresql-client-16
```

- If removed the incorrect cluster recreate and start the correct one:
```
pg_createcluster
```
```
sudo pg_ctlcluster 16 main start
```

### Verify the installation
```
gvm-check-setup
```

- Successful output:
```
It seems like your GVM-23.11.0 installation is OK.
```

- The web interface is available at https://localhost:9392
- Enter the username: admin and password when prompted

The framework consumes a lot of resources so it is recommended to disable these services when not using OpenVAS.  

### To start the services
```
sudo gvm-start
```

- Wait until all services have confirmed running before accessing the web interface

### To stop the services
```
sudo gvm-stop
```
