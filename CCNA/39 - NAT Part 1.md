## Private IPv4 Addresses
* IPv4 doesn't provide enough addresses for al devices that need an IP address in the world.
* The long-term solution is to switch to IPv6 addresses.
* There are three main short-term solutions:
	* CIDR
	* Private IPv4 addresses
	* NAT
* RFC 1918 specifies the following IPv4 address ranges as private:
	* `10.0.0.0/8` (`10.0.0.0` to `10.255.255.255`)
	* `172.16.0.0/12` (`172.16.0.0` to `172.31.255.255`)
	* `192.168.0.0/16` (`192.168.0.0` to `192.168.255.255`)
* You are free to use these addresses in your networks. They don't have to be globally unique.
	* Your PC in your home network, is almost certainly using a private IP address.
* Private IP addresses cannot be used over the internet!
	* The IPS (Internet Service Provider) will drop traffic to or from private IP addresses.
## Intro to NAT (Network Address Translation)
* Network Address Translation (NAT) is used to modify the source and/or destination IP address of packets.
* There are various reasons to use NAT, but the most common reason is to allow hosts with private IP addresses to communicate with other hosts over the internet.
* For the CCNA you have to understand **source NAT** and how to configure it on Cisco routers.

## Static NAT
## Static NAT Configuration
