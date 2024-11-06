# Active Directory Project

## Splunk Server

### VM Specifications

Ubuntu 24.04 server
  8192 mem
  2 cpu
  96gb disk
  set ip addressing during installation 10.0.0.12/24
    otherwise defaults
    install openssh
    no other install options needed
  update/upgrade
  install vmware tools
  snapshot

### Splunk Enterprise software

splunk > signin
    splunk enterprise > free trial
    linux > .deb

transfer file to ubu-server
sudo dpkg -i <splunk-installer>
cd /opt/splunk
all users/groups > splunk
sudo -u splunk bash (login as splunk user)
cd ~/bin
./splunk start (installer)
admin username: set during ubu installation
exit
cd /opt/splunk/bin (splunk install dir)
sudo ./splunk enable boot-start -user splunk

http://10.0.0.12:8000 to test

### Splunk Universal Forwarder software

splunk > signin
products > free trials
universal forwarder > free download
select OS (windows 64-bit)

run installer on target machines
    on-prem splunk instance
    username: admin
    generate random password
    no deployment server
    receiving indexer: 10.0.0.12 port 9997
    install

### Sysmon software

search sysmon: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
download sysmon
search sysmon olaf config
github
look for sysmonconfig.xml
raw > save as > name file.xml
move to folder of choice
locate the xml file in the same location
powershell as admin
change to sysmon download folder
.\Sysmon64.exe -i sysmon-file.xml
installer launches > finish

on target hosts:
c:\program files\splunkuniversalforwarder\etc\system\default\inputs.conf
move one level up to \local
notepad as admin
create new file
    copy contents of inputs.local to new file
    this pushes events from Application/Security/System logs to sysmon
    note the index = endpoint
    server also needs an index named the same or will not receive anything
save the file to the \local dir above as inputs.conf
NOTE any time this file is changed must restart splunkuniversalforwarder service
services > run as admin > splunkforwarder > properties
login as local system account > ok
restart the service > start if errors

### Splunk Index configuration

splunk login portal
login
settings > indexes
name column = indexes
new index
name: endpoint
save
check is in name column

### Splunk Receiving Port configuration

settings > forwarding/receiving
    receive data > configure receiving
    new receiving port > 9997
    save

### Test Splunk is receiving events

apps > search and reporting
    "index=endpoint" > search icon
    look for events from the windows endpoint
    source should show the event logs previously pushed in inputs.conf

### Configure other Windows Hosts

configure other windows hosts in same way
end

### Splunk Trial license conversion

convert trial to free license
https://docs.splunk.com/Documentation/Splunk/9.3.1/Admin/MoreaboutSplunkFree