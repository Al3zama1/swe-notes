## The Purpose of DHCP
* DHCP is used to allow hosts to automatically/dynamically learn various aspects of their network configuration, such as IP addresses, subnet mask, default gateway, DNS server, etc, without manual/static configuration.
* It is an essential part of modern networks.
* Typically used for 'client devices' such as workstations (PCs), phones, etc.
* Devices such as routers, servers, etc, are usually manually configured.
* In small networks (such as home networks) the router typically acts as the DHCP server for hosts in the LAN.
* In larger networks, the DHCP server is usually a Windows/Linux server.
## Basic Function of DHCP

### Release IP
```
ipconfig /release
```
* The device releases the assigned IP address (windows).
* The device sends a DHCP release message to the DHCP server, setting it that the IP address isn't needed anymore.
	* The IP becomes available and can be assigned to another client.

## Configuring DHCP in Cisco IOS

