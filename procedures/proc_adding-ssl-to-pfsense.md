system > certificate manager
method > create an internal CA
descriptive name: XXX-Root-CA
country code: GB
state
city
organisation
OU
email address
common name: same as descriptive name (XXX-Root-CA)
save

system > certificate manager
create an intermediate CA
descriptive name: XXX-Sub-CA
signing certificate authority: lab-root-ca
country code: GB
state
city
organisation
OU
email address
common name: same as descriptive name (XXX-Sub-CA)
save

certificate manager > certificates
add new certificate
create an internal certificate
descriptive name: host.domain (lab-splunk.lab.internal)
ca: Sub-CA
common name: same as descriptive name
certificate type: server
alt name: IP address
    value: IP address of server
save

certificate manager > CAs
root-CA > Export
Save As

certificate manager > CAs
sub-CA > Export
Save As

certificate manager > certificates
server certificate (sub-CA) > Export
Save As

server > run > mmc
add snap-in
bottom option > Certificate? > OK
bottom option > next
local computer 
ok

expand local computer
2nd option down > expand > certificate > right click > all tasks
import assistant > next
browse > root-CA
next/next/finish
XXX-Root-CA in list

expand local computer
4th option down > expand > certificate > right click > all tasks
import assistant > next
browse > sub-CA
next/next/finish
XXX-Sub-CA in list

pfsense > system > advanced > admin access
https
ssl > server certificate (host.domain
dns rebind check > ON
disable HTTP_REFERER > ON
save

add certs to Firefox

browse to https pfsense
check certificate

if any internal systems need to access the secured domain name
    then add A record to the DNS server for the host/ip combination
ipconfig /flushdns at the client

