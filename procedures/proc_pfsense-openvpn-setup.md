# pfSense OpenVPN Setup

## Install Client Export Package

pfSense
System > Package Manager > Available Packages
Search *openvpn*
Click +Install > openvpn-client-export package
Confirm

## Configure OpenVPN on pfSense

VPN > OpenVPN > Wizards
Type of Server > Local User Access

## Creating a Certificate Authority

Create new Certificate Authority > Descriptive Name: Lab VPN CA Certificate
Country Code: GB
State or Province: <insert>
City: <insert>
Organisation: <insert>
Add new CA

## Create a Server Certificate

Add new Certificate
Descriptive Name: VPN Server Certificate
Country Code: GB
State or Province: <insert>
City: <insert>
Organisation: <insert>
Create new Certificate

## General OpenVPN Server Information

Description: Lab VPN Server
Protocol: UDP on IPv4 only
Interface: WAN
Local Port: 1194


### Cryptographic Settings

TLS Authentication: Enabled
Generate TLS Key: Enabled
Data Encryption Algorithms: CHACHA20
Fallback Data Encryption Algorithm: CHACHA20

### Tunnel Settings

Tunnel Network: 192.168.100.0/24
Local Network: 10.0.0.0/24
Concurrent Connections: 1

### Client Settings

DNS Default Domain: lab.internal
DNS Server 1: 10.0.0.1
Next

## Firewall Rules

Firewall Rule > Enabled
OpenVPN Rule > Enabled
Next
Finish

## Create a VPN Users

System > User Manager > +Add
Specify Username/Password
Confirm Password
Groups: admins
Certificate > Enabled

### Create Certificate for User

Descriptive Name: Lab User Certificate
Certificate Authority: Lab VPN CA Certificate
Save

## pfSense OpenVPN Client Export

VPN > OpenVPN > Client Export
Remote Access Server: Lab VPN Server

### OpenVPN Clients

User: lab-vpn-user

OpenVPN not installed on client:
Current Windows Installers: 64-bit

OpenVPN installed on client:
Bundled Configurations : Config File only