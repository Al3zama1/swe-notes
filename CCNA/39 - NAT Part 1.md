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
![Source NAT](./img3/source-NAT.png)
* Source NAT process.
## Static NAT
* **Static NAT** involves statically configuring one-to-one mappings of private IP addresses to public IP addresses.
	* It doesn't have to be private to public. You can NAT any address to any other address.

![Static NAT](./img3/static-NAT.png)
* On R1, PC1's private IP address `192.168.0.167` was mapped to the public IP address `100.0.0.1`.
	
![static NAT sample 2](./img3/static-NAT-sample2.png)
* If PC2 also wants to reach `8.8.8.8`, it will need its own *inside global* address configured on R1.
	* The router will not allow both, PC1 and PC2 to be mapped to the same *inside global* address using static NAT.
### NOTE
**Static NAT** allows devices with private IP addresses to communicate over the internet. However, because it requires a one-to-one IP address mapping, it doesn't help preserve IP addresses. 

If each internal device needs its own public IP address anyway, you might as well just configure a public IP address on the device itself. Although, there are reasons to use static NAT, It's not the most useful for preserving IP addresses.
## Static NAT Configuration
