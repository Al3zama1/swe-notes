## Topology Introduction
* LAG is just another name for EtherChannel. But in the context of WLCs (Wireless Lan Controllers), the term LAG is used.
* It's not necessary to connect the WLC to the switch using a LAG, but it's a good idea to provide additional throughput and redundancy.
* VLAN 100 and VLAN 200 will be mapped to a wireless LAN and advertised by the APs.
* VLAN 10 will be used  to connect to the network devices (WLC, switch, APs, etc) to manage them (via SSH, etc).
* SW1 has an SVI in each VLAN.
* WLC1 has an IP in each VLAN.
* The APs will need an IP address in the management VLAN so they can communicate with the WLC. The IP addresses will be assigned via DHCP.
	* The WLC could be the DHCP server, but the switch will server as both, the the DHCP server and NTP server for this network.
## Switch Configuration
## WLC Setup
## WLC Interface Configuration
## WLAN Configuration
## Additional WLC Features
