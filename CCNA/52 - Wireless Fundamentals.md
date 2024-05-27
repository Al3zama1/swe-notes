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
**Reflection** happens when a signal bounces off a metal, for example metal. This is why Wi-Fi reception is usually poor in elevators. The signal bounces off the metal and very little penetrates into the elevator.
##### Signal Refraction
![Wireless refraction](./img4/wireless-refraction.png)
**Refraction** happens when a wave is bent when entering a medium where the signal travels at a different speed. For example, glass and ware can refract waves.
##### Signal Diffraction
![Wireless diffraction](./img4/wireless-diffraction.png)
**Diffraction** happens when a wave encounters an obstacle and travels around it to some degree. This can result in blind spots behind the obstacle where the devices don't receive sufficient signal from the access point.
##### Signal Scattering
![Wireless scattering](./img4/wireless-scattering.png)
**Scattering** happens when a material causes a signal to scatter in all directions. Usually, dust, smog, uneven surfaces, etc. can cause scattering.
#### Interference
* Other devices using the same channels can cause interference.  For example, a wireless LAN in your neighbor's house/apartment.
## Radio Frequencies (RF)

## Wi-Fi Standards

## Wireless LAN Fundamentals