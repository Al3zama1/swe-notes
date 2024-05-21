## The Purpose of DNS
* DNS is used to resolve human-readable names (google.com) to IP addresses.
* The DNS server(s) your device uses can be manually configured via DHCP.
## Basic Functions of DNS

`ipconfig /all`: 
* display various network information, including DNS in a windows computer.
`nslookup <domain-name>`:
* It tells the device to ask its DNS server for the Ip address of the specified domain name.
* You don't have to use the `nslookup` command before sending the ping. If your server doesn't know the correct IP address, it will automatically ask the DNS server.
### DNS UDP & TCP
* Standard DNS queries/responses typically use UDP. TCP is used for DNS messages greater than 512 bytes. In either case, port 53 is used.

## Configuring DNS in Cisco IOS
