## pfSense List Interfaces
- pfsense option 8: shell

- list interfaces:
```
tcpdump -D
```
- pfsense output:
```
vtnet0 WAN
vtnet1 LAN
```

## pfSense Packet Capture
- pfSense GUI > diagnostics > packet capture
```
/use/sbin/tcpdump -ni vtnet1 -c '1000' -U -w -
```

- pfSense Command Line:
```
tcpdump -ni vtnet1 -c 1000 -w /tmp/capture.pcap
```

## Editing pcap files
- https://www.wireshark.org/docs/man-pages/editcap.html

