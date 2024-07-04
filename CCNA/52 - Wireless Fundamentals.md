## Wireless Networks
* Although we will briefly look at other types of wireless networks, in this section of the course we will be focusing on wireless LANs using Wi-Fi.
* The standards we use for wireless LANs are defined in IEEE 802.11.
* The term **Wi-Fi** is a trademark of the **Wi-Fi Alliance**, not directly connected to the IEEE.
* The Wi-Fi Alliance tests and certifies equipment for 802.11 standards compliance interoperability with other devices.
* However, Wi-Fi has become the common term that people use to refer to 802.11 wireless LANs.
### Factors to Consider When Building Wireless Networks
#### Security & Collisions
* When a wireless device transmits a frame, all wireless-enabled devices within range will be able to pick up that frame. This can lead to data privacy concerns, as well as collisions when devices communicate on the same channel at the same time.
* Privacy of data within the LAN is a greater concern. In wired networks we don't usually encrypt data within the LAN, only when sending data over a shared network such as the internet. However, for wireless networks it is very important to encrypt data even within the LAN, or else anyone with a device in range of the transmitter can access that data.
* **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) is used to avoid collisions and facilitate half-duplex communications.
	* **CSMA/CD** is used in wired networks to detect and recovery from collisions.
	* **CSMA/CA** is used in wireless networks to avoid collisions.

![CSMA/CA workflow](./img4/CSMA-CA-workflow.png)
* When using **CSMA/CA**, a device will wait for other devices to stop transmitting before it transmits data itself.
	* The transmitting device assembles the frame and prepares it to be sent.
	* Then, it listens to check if the channel is free.
	* If the channel is not free, it will wait for a random period of time.
	* Then, it will listen again.
	* If the channel is free this time, it will transmit the frame.
* Note that this is a simplification of the process. There is an optional feature in which the transmitting device sends a 'request to send' (RTS) packet and waits for a 'clear to send' (CTS) packet from the receiver device, before actually sending the data packet.
#### Regulations
* Wireless communications are regulated by various international and national bodies.
* You aren't allowed to transmit data on any channel you want, and which channels you are allowed to use can vary depending on the country.
* The 802.11 standard outlines which frequencies can be used for wireless LANs, and devices are designed to use those frequencies.
#### Coverage Area (Signal Quality)
* In wired connections we have to consider the cable length and in some cases electromagnetic interference, but with wireless connections, there are other factors that must be considered.
* The wireless signal coverage area must be considered along with the various factors that can affect how far the signal can travel intact.
	* Absorption
	* Reflection
	* Refraction
	* Diffraction
	* Scattering
* When planning the positioning of wireless access points for a network, you have to take all of these factors under account.
##### Signal Absorption
![Wireless signal absorption](./img4/wireless-absorption.png)
**Absorption** happens when a wireless signal passes through a material and is converted into heat, weakening the original signal.
##### Signal Reflection
![Wireless reflection](./img4/wireless-reflection.png)
**Reflection** happens when a signal bounces off a material, for example metal. This is why Wi-Fi reception is usually poor in elevators. The signal bounces off the metal and very little penetrates into the elevator.
##### Signal Refraction
![Wireless refraction](./img4/wireless-refraction.png)
**Refraction** happens when a wave is bent when entering a medium where the signal travels at a different speed. For example, glass and water can refract waves.
##### Signal Diffraction
![Wireless diffraction](./img4/wireless-diffraction.png)
**Diffraction** happens when a wave encounters an obstacle and travels around it to some degree. This can result in blind spots behind the obstacle where the devices don't receive sufficient signal from the access point.
##### Signal Scattering
![Wireless scattering](./img4/wireless-scattering.png)
**Scattering** happens when a material causes a signal to scatter in all directions. Usually, dust, smog, uneven surfaces, etc. can cause scattering.
#### Interference
* Other devices using the same channels can cause interference.  For example, a wireless LAN in your neighbor's house/apartment.
## Radio Frequencies (RF)
* To send wireless signals, the sender applies an alternating current to an antenna. This creates electromagnetic fields which propagate out as waves.
* Electromagnetic waves can be measured in multiple ways, such as **amplitude** and **frequency**.

![Amplitude](./img4/amplitude-waves.png)
* **Amplitude** is the maximum strength of the electric and magnetic fields.

![Frequency](./img4/frequency.png)
* **Frequency** measures the number of up/down cycles per a given unit of time.
* The most common measurement of frequency is **hertz**.
	* Hz (Hertz): Cycles per second.
	* KHZ (Kilohertz): 1, 000 cycles per second.
	* MHz (Megahertz): 1, 000, 000 cycles per second.
	* GHz (Gigahertz): 1, 000, 000, 000 cycles per second.
	* THz (Terahertz): 1, 000, 000, 000, 000 cycles per second.

![Frequency example](./img4/frequency-example.png)
* The frequency in a time interval of one second is 4 HZ.
* There is 4 cycles in an interval of 1 second, therefore the **period** is 0.25 seconds.
### Radio Frequency Range
* The visible frequency range is about 400 THz to 790 THz.
* The radio frequency range is from 30 Hz to 300 GHz and is used for many purposes.
* Wi-Fi uses two main bands (frequency ranges).
	* **2.4 GHz** band which ranges from 2.400 GHz to 2.4835 GHz
	* **5 GHz** band which ranges from 5.150 GHz to 5.825 GHz. The range is divided into four smaller bands.
* The 2.4 GHz band typically provides further reach in open space and better penetration of obstacles such as walls.
	* However, more devices tend to use the 2.4 GHz band so interference can be a bigger problem compared to the 5GHz band.
* **Wi-Fi 6** (802.11ax) has expanded the spectrum range to include a band in the **6 GHz** range.
### Radio Frequency Channels
* Each band is divided up into multiple channels.
* Devices are configured to transmit and receive traffic on one (or more) of these channels.
	* Channel bonding can be used to combine channels together to be able to receive traffic on more than one channel.

#### 2.4 GHz Frequency Band Channels
![2.4 GHz channels](./img4/2.4-channels.png)
* The 2.4 GHz band is divided into several channels, each with a 22 MHz range.
	* Note that it differs by country.
* An important aspect of 2.4 GHz frequency channels is that they overlap.
	* To avoid interference between adjacent wireless access points, we have to carefully chose which channels we configure our access points to use.
* In a small wireless LAN with only a single AP, you can use any channel because there are no other channels that can cause interference.
* In larger WLANs with multiple APs, it's important that adjacent APs don't use overlapping channels to avoid interference.
	* Using overlapping channels between adjacent APs will result in reduced performance and worse user experience.

![2.4 GHz frequency visualization](./img4/2.4-requency-vizualization.png)
* In the 2.4GHz band, it is recommended to use channels 1, 6, and 11 because they don't overlap.
* Outside of North America you could use other combinations, but for the CCNA exam remember 1, 6, and 11.

![](./img4/2.4-frequency-APs-positioning-pattern.png)
* Using the 1, 6, and 11 pattern you can place APs in a 'honeycomb' pattern to provide complete coverage of an area without interference between channels.
* **The coverage area of each AP overlaps to provide complete coverage of the area, but the frequencies don't overlap, which helps avoid interference between the APs.**
* When you have to provide wireless coverage over a large space, you should arrange your APs like this.
#### 5 GHz Frequency Band Channels
* The 5 GHz band consists of non-overlapping channels, so it is much easier to avoid interference between adjacent APs.
## Wi-Fi Standards
![802.11 standards](./img4/802.11-standards.png)
* 802.11 enabled devices might support one of these standards, some of them, or all of them.
* 802.11n is also known as High Throughput (HT) Wi-Fi.
* 802.11ac is also known as Very High Throughput (VHT) Wi-Fi.
## Service Sets
* 802.11 defines different kinds of **service sets** which are groups of wireless network devices.
* There are three main types:
	* Independent
	* Infrastructure
	* Mesh
* All devices in a service set share the same **SSID** (Service Set Identifier).
	* The SSID is a human-readable name which identifies the service set.
	* The SSID does not have to be unique, although it's best to configure unique SSIDs since that's what you'll be looking at when you select which network to connect to.
### Independent Basic Service Set (IBSS)
![Service Set IBSS](./img4/service-set-IBSS.png)
* An **IBSS** is a wireless network which two or more wireless devices connect directly without using an AP (Access Point).
* Also called **ad hoc** networks.
* Not scalable beyond a few devices.
* Are used for limited purposes, such as quick file transfers (ie. AirDrop).
### Basic Service Set (BSS)
![Service Set BSS](./img4/service-set-BSS.png)
* A BSS is a kind of infrastructure Service Set in which clients connect to each other via an AP (Access Point), but not directly to each other.
* The **BSSID** (Basic Service Set ID) of an AP is a unique identifier used to distinguish between different wireless networks (SSID) broadcasted by the AP. 
	* It is derived from the MAC address of the AP's radio interface but can be modified or generated uniquely for each SSID that the AP broadcasts.
	* Other APs can have the same SSID, but no the same BSSID.
* Wireless devices request to associate with the BSS.
* Wireless devices that have associated with the BSS are called 'clients' or 'stations'.
* The area around an AP where its signal is usable is called a **BSA** (Basic Service Area).
### Extended Service Set (ESS)
![Service sets ESS](./img4/service-sets-ESS.png)
* To create larger wireless LANs beyond the range of a single AP, we use an **ESS** (Extended Service Set)
	* This is an infrastructure service set.
* APs with their own BSS are connected by a wired network.
	* Each BSS uses the same SSID.
	* Each BSS has a unique BSSID.
	* Each BSS uses a different channel to avoid interference.
* Clients can pass between APs without having to reconnect, providing a seamless Wi-Fi experience when moving between APs.
	* This is called **roaming**, when you move between two APs in an ESS.
* The BSAs should overlap about 10 - 15%, or else the connectivity can be lost when moving between APs.
### Mesh Basic Service Set (MBSS)
![Service Set MBSS](./img4/service-set-MBSS.png)
* A **MBSS** can be used in situations where it's difficult to run an Ethernet connection to every AP.
* Mesh APs use two radios:
	* One provides a BSS to wireless clients.
	* The other forms a 'backhaul network' which is used to bridge traffic from AP to AP.
* At least one AP is connected to the wired network, and it is called the **RAP** (Root Access Point).
* The other APs are called **MAP**s (Mesh Access Points).
* A protocol is used to determine the best path through the mesh (similar to dynamic routing protocols are used to determine the best path to a destination).
## Distribution System
* Most wireless networks aren't standalone networks. They are a way for wireless clients to connect to the wired network infrastructure.
	* APs function is to translate between the tow mediums (wireless, wired).
* In 802.11, the upstream wired network is called the **DS** (Distribution System).

![Wireless network connection to Wired network](./img4/AP-connection-to-distribution-system.png)
* Each wireless BSS or ESS is mapped to a VLAN in the wired network.

![AP with multiple WLANs connect to wired network](./img4/AP-connection-to-distribution-system-multiple-VLANs.png)
* It's possible for an AP to provide multiple wireless LANs, each with a unique SSID.
	* This is the same as how a switch can divide a single physical wired network into multiple VLANs.
* Each WLAN is mapped to a separate VLAN and connected to the wired network via a trunk.
* Each WLAN uses a unique BSSID, usually by incrementing the last digit of the BSSID by one.
## Additional AP Operational Modes
### Repeater
![AP operating as a repeater](./img4/AP-as-a-repeater.png)
* An AP in **repeater** mode can be used to extend the range of a BSS.
* The repeater will simply retransmit any signal it receives from the AP.
* A repeater with a single radio must operate on the same channel as the AP. However,  this can drastically reduce the overall throughput on the channel because the repeater will be repeating the AP's signals back to it using the same channel, keeping the channel busy. This cuts the effective throughput of the channel by 50%.
* A repeater with two radios can receive on one channel, and then retransmit on another channel.
### Workgroup Bridge (WGB)
* An AP in **workgroup bride** (WGB) mode operates as a wireless client of another AP, and can be used to connect wired devices to the wireless network.
	* It's a solution which allows clients that don't support wireless connections to connect to the wireless network via an AP operating as a workgroup bridge.
* There are two kinds of WGBs:
	* **Universal WGB** (uWGB): an 802.11 standard that allows one device to be bridged to the wireless network.
	* **WGB**: a Cisco-proprietary version of the 802.11 standard that allows multiple wired clients to be bridged to the wireless network.

![AP operating as a workgroup bridge](./img4/AP-as-a-workgroup-bridge.png)
* PC1 does not have wireless capabilities, and also does not have access to a wired connection to SW1.
* PC1 has a wired connection to the WGB, which has a wireless connection to the AP.
### Outdoor Bridge
![AP in outdoor bridge mode](./img4/AP-as-outdoor-bridge-mode.png)
* An AP in **outdoor bridge** mode can be used to connect networks over long distances without a physical cable connecting them.
* The APs will use specialized antennas that focus most of the signal power in one direction, which allows the wireless connection to be made over longer distances than normally possible.
* The connection can be point-to-point as in the diagram above or point-to-multipoint in which multiple sites connect to one central site (forming a Hub and Spoke topology).