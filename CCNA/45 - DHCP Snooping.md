## What is DHCP Snooping?
* DHCP snooping is a security feature of switches that is used to filter DHCP messages received on untrusted ports.
* DHCP snooping only filters DHCP messages. Non-DHCP messages aren't affected.
* DHCP snooping won't inspect any DHCP messages on trusted ports, the switch will simply forward them as normal.
* All ports are untrusted by default.
	* Usually, **uplink** ports are configured as trusted ports, and **downlink** ports remain untrusted.

![DHCP trusted and untrusted ports](./img3/dhcp-snooping-trusted-untrusted-ports.png)
* The downlink ports on the switches (interfaces pointing towards the end hosts), should be untrusted.
	* The network admin does not have direct control over the end user devices. A malicious user could initiate a DHCP-based attack from one of their device. Therefore, its best to leave these ports in the default untrusted state.
* The uplink ports point toward the network infrastructure, the devices the network admin has control over.

![Valid DHCP traffic](./img3/valid-dhcp-traffic.png)
* The DHCP message is valid and is checked by both SW1 and SW2 since it is entering their untrusted interfaces.
* On the way back to PC1, it is not checked since it is going through the switches trusted interfaces.

![DHCP snooping invalid message](./img3/dhcp-snooping-invalid-message.png)
* The DHCP message was blocked by SW1 because maybe it was trying to use a DHCP exploit.
## What Attacks Does It Prevent ?
### DHCP Starvation
* An example of a DHCP-based attack is a **DHCP starvation** attack.
* An attacker uses spoofed MAC addresses to flood DHCP Discover messages.
* The target server's DHCP pool becomes full, resulting in a denial-of-service to other devices.

![DHCP starvation walkthrough](./img3/DHCP-starvation.png)
* DHCP uses a field in the DHCP message, written as **CHADDR**, which stands for **Client Hardware Address**. It is used to indicate the MAC address of the client that originated the DHCP message.
	* The field is needed because in the event that a DHCP relay is being used to send the DHCP message over the internet, the source MAC address will not be the one from the original client once it reaches the DHCP server. Therefore, the DHCP server cannot use it as a way of referencing the client that sent the message. The CHADDR field maintains the client's source MAC address regardless of the number of hops.
### DHCP Poisoning (Man-in-the-Middle)
* Similar to ARP poisoning, DHCP Poisoning can be used to perform a Man-in-the-Middle attack.
* A *spurious* (illegitimate) DHCP server replied to clients DHCP Discovery messages and assigns them IP addresses, but makes the clients use the spurious server's IP as the default gateway.
	* Multiple DHCP servers can respond to DHCP Discover messages, but clients usually accept the first offer message they receive. If the spurious DHCP server beats the legitimate DHCP server in reaching the requesting client, it could be picket.
* This will cause the client to send traffic to the attacker instead of the legitimate default gateway.
* The attacker can then examine/modify the traffic before forwarding it to the legitimate default gateway, which will send the traffic to the external destination.
* The client probably won't even notice that its traffic is being intercepted since it is reaching its destination.
## DHCP Messages


## DHCP Snooping Config
