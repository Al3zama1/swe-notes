## Topology Introduction
![Wireless LAN configuration network topology](./img4/wireles-config-network-topology.png)
* LAG (Link Aggregation Group) is just another name for EtherChannel. But in the context of WLCs (Wireless LAN Controllers), the term LAG is used.
	* It's not necessary to connect the WLC to the switch using a LAG, but it's a good idea to provide additional throughput and redundancy.
* VLAN 100 and VLAN 200 will be mapped to a wireless LAN and advertised by the APs.
* VLAN 10 will be used  to connect to the network devices (WLC, switch, APs, etc) to manage them (via SSH, etc).
* SW1 has an SVI in each VLAN.
* WLC1 has an IP in each VLAN.
* The APs will need an IP address in the management VLAN so they can communicate with the WLC. The IP addresses will be assigned via DHCP.
	* The WLC could be configured as the DHCP server, but the switch will server as both, the the DHCP server and NTP server for this network.
* A split-MAC architecture is being used, therefore the interfaces connected to the APs are access ports. Only the WLC needs to connect via a trunk port with all of the necessary VLANs.
* The APs will form a CAPWAP tunnel to the WLC.
## Switch Configuration
### VLAN Creation and Assignment
```
SW1(config)#vlan 10
SW1(config-vlan)#name management
SW1(config-vlan)#vlan 100
SW1(config-vlan)#name Internal
SW1(config-vlan)#vlan 200
SW1(config-vlan)#name Guest

SW1(config)#int range f0/6 - 8
SW1(config-if-range)#switchport mode access
SW1(config-if-range)#switchport access vlan 10
SW1(config-if-range)#spanning-tree portfast

SW1(config)#int range f0/1 - 2
SW1(config-if-range)#channel-group 1 mode on

SW1(config-if-range)#interface port-channel 1
SW1(config-if)#switchport mode trunk
SW1(config-if)#switchport trunk allowed vlan 10,100,200
```
* Interfaces F0/6 was also included to be able to connect to it with a PC to gain access to WLC1's GUI. 
	* A device's CLI can be accessed via the console port or connected to over the network using Telnet or SSH.
	* The GUI cannot be accessed via the console port. You must connect over the network, using HTTP or HTTPS.
* WLCs only support static LAG, no PAgP or LACP.
### SVIs Creation
```
SW1(config)#interface vlan 10
SW1(config-if)#ip address 192.168.1.1 255.255.255.0
SW1(config-if)#interface vlan 100
SW1(config-if)#ip address 10.0.0.1 255.255.255.0
SW1(config-if)#interface vlan 200
SW1(config-if)#ip address 10.1.0.1 255.255.255.0
```
### DHCP Pool Configuration
```
SW1(config)#ip dhcp pool VLAN10
SW1(dhcp-if)#network 192.168.1.0 255.255.255.0
SW1(dhcp-if)#default-router 192.168.1.1
SW1(dhcp-if)#option 43 ip 192.168.1.100

SW1(config)#ip dhcp pool VLAN100
SW1(dhcp-if)#network 10.0.0.0 255.255.255.0
SW1(dhcp-if)#default-router 10.0.0.1

SW1(config)#ip dhcp pool VLAN200
SW1(dhcp-if)#network 10.1.0.0 255.255.255.0
SW1(dhcp-if)#default-router 10.1.0.1

SW1(config)#ntp master
```
* The `default-router` command specifies SW1's SVI IP addresses as the default gateway for each subnet.
* VLAN10 DHCP pool will be used by the APs to get their IP addresses, which they need to communicate with the WLC.
* DHCP option 43 can be used to tell the APs the IP address of their WLC.
	* When the APs get an IP address from SW1, it will tell them the IP of their WLC. The APs will then try to communicate with the WLC and form their CAPWAP tunnels.
	* This is not necessary in this case though because the APs and WLC are in the same subnet, the same local VLAN. The WLC will hear the APs broadcast CAPWAP discovery messages.
	* Option 43 is needed if the WLC is located somewhere that it won't be able to hear the broadcast discovery messages from the APs.
* SW1 is configured as an NTP server. Later, the WLC will be configured to use SW1 as its NTP server.
## WLC Initial Setup (CLI)
![WLC initial setup](./img4/WLC-initial-setup.png)
* When the WLC first boots up, you will be greeted with a configuration wizard.
	* You don't need to know any CLI commands for the WLC to do this basic setup, the wizard will walk you through it.
* Autoinstall can be used to automatically download the WLC's configuration from a TFTP server.
* A system name (hostname), username, and password  are configured to be able to log into the device.
* LAG will be used to connect to SW1, so it is enabled.
* The management interface is also configured, which is a virtual interface (not a physical port) in the WLC.
	* In most context, we can use the terms port and interface interchangeably.
	* However, in the context of WLCs, ports means physical ports and interfaces means logical interfaces within the device.

![WLC initial setup continued](./img4/WLC-initial-config-2.png)
* The *Virtual Gateway IP Address* is an IP address used when then WLC is communicating directly with wireless clients, such as when relaying DHCP requests.
* The *Multicast IP Address* is used when forwarding traffic to its APs.
	* Note that an IP address in the class D range was used, which is reserved for multicast IP addresses.
* The *Mobility/RF Group Name* is used when you have multiple WLCs and you want them to work together.
* Wireless LAN configuration:
	* For wireless clients' DHCP requests to reach the DHCP server (SW1), they must pass through WLC1 first. If *DHCP Bridging Mode* is enabled, the WLC becomes totally transparent to the clients. It will appear as if the APs are communicating directly to the DHCP server. However, that is not needed here, so it is disabled.
	* Static IP addresses are allows, which means that clients are allowed to use static IP addresses if they prefer. They don't have to use DHCP.
	* The WLAN security policy will be changed to PSK. Therefore, a RADIUS server does not need to be configured
* *Country Code List* is used to enter countries that fall in the regulatory domain of the AP. 
	* In this case FR (France) was entered because it falls in the regulatory domain of the AP, which is E (Europe).
	* The AP's model name specifies its regulatory domain. The model name of the AP being used is *AIR-CAP3502l-==E==-K9*.
	* If the regulatory domain of the country specified in the WLC configuration doesn't match the regulatory domain of the AP, the AP won't be able to join the WLC.

![WLC initial setup continues](./img4/WLC-initial-config-3.png)
* Enabled 802.11b, 802.11a, and 802.11g protocols.
* *Auto-RF* is enabled, which allows the WLC to automatically select which channels to use and how much transmit power to use.
	* This is much better than doing everything manually.
* Configured NTP settings so that the WLC has the correct time.

### Accessing the WLC GUI
![Access WLC's GUI on the browser](./img4/access-WLC-GUI.png)
* Now that the WLC's initial setup is complete, it has an IP address in the management VLAN (VLAN 10).
* Instead of connecting a PC to the WLC's console port or accessing it remotely (Telnet, SSH), the PC is connected to the switch (f0/6 interface, which was previously configured).
	* Once connected to the switch, HTTP or HTTPS can be used to access the WLC's GUI in a web browser.
### WLC Ports
![WLC ports](./img4/CLC-ports.png)
* WLC ports are the physical ports that cables connect to.
* WLC has a few different kinds of ports:
	* **Service ports**: A dedicated management port. Used for out-of-band management. Must connect to a switch access port because it only supports one VLAN. This port can be used to connect to the device while it is booting, perform system recovery, etc.
		* A dedicated management port means keeping management traffic totally separate from regular data traffic, not using the same physical interface.
	* **Distribution system port**: These are the standard network ports that connect to the 'distribution system' (wired network) and are used for data traffic.These ports usually connect to switch trunk ports, and if multiple distribution ports are used they can form a LAG.
		* Distribution system is the 802.11 term for the wired network.
	* **Console port**: This is a standard console port, either RJ45, USB, or both.
	* **Redundancy port**: This port is used to connect to another WLC to form a high availability (HA) pair.
		* If one WLC fails, the other one can continue to support the network.
### WLC Interfaces
* WLC interfaces are the logical interfaces within the WLC (ie. SVIs on a switch).
* WLCs have a few different kinds of interfaces:
	* **Management interface**: Used for management traffic such as Telnet, SSH, HTTP, HTTPS, RADIUS authentication, NTP, Syslog, etc. CAPWAP tunnels are also formed to/from the WLC's management interfaces.
	* **Redundancy management interface**: When two WLCs are connected by their redundancy ports, one WLC is 'active' and the other is 'standby'. This interface can be used to connect to and manage the 'standby' WLC.
	* **Virtual Interface**: This interface is used when communicating with wireless clients to relay DHCP requests, perform client web authentication etc.
	* **Service port interface**: If the service port is used, this interface is bound to it and used for out-of-band management instead of the regular management interface.
	* **Dynamic interface**: These interfaces are used to map a WLAN to a VLAN. For example, traffic from the 'internal' WLAN will be sent to the wired network from the WLC's 'internal' dynamic interface.
## WLAN Configuration
### WLC Interface Configuration
![WLC dynamic interface configuration](./img5/WLC-dyanmic-interface-config.png)
* Navigate to the controller view to view and create new interfaces.
* Create a dynamic Interface per WLAN, which is mapped to a specific VLAN.
	* One interface for the internal WLAN, which is mapped to VLAN 100.

## Additional WLC Features
