## Why Security ?
* The principles of the **CIA Triad** form the foundation of security:
	* **C**onfidentiality:
		* Only authorized users should be able to access data.
		* Some information/data is public and can be accesses by anyone, some is secret and should only be accessed by specific people.
	* **I**ntegrity:
		* Data should not be tampered with (modified) by unauthorized users.
		* Data should be correct and authentic.
	* **A**vailability:
		* The network/systems should be operational and accessible to authorized users.
* Attackers can threaten the confidentiality, integrity, and availability of an enterprise's systems and information.
## Key Security Concepts
* A **vulnerability** is any potential weakness that can compromise the CIA of a system/info.
	* A potential weakness isn't a problem on its own.
* An **exploit** is something that can potentially be used to exploit the vulnerability.
	* Something that can potentially be used as an exploit isn't a problem on its own.
* A **thread** is the potential of a **vulnerability** to be **exploited**.
	* A hacker **exploiting** a **vulnerability** in your system is a **thread**.
* A **mitigation technique** is something that can protect agains threads.
	* Should be implemented everywhere a vulnerability can be exploited: client devices,
	* servers, switches, routers, firewalls, etc.
### No System is Perfectly Secure
Systems can be more secure or less secure, but there are no guarantees in security.
## Common Attacks
### Denial-of-service Attacks (DoS)
* DoS attacks threaten the availability of a system.
* One common DoS attack is the TCP SYN flood.
	* TCP three-way handshake: SYN | SYN-ACK | ACK
	* The attacker sends countless TCP SYN messages to the target. 
	* The target sends a SYN-ACK message in response to each SYN it receives.
	* The attacker never replies with the final ACK of the TCP three-way handshake.
	* The incomplete connections fill up the target's TCP connection table.
	* The attacker continues sending SYN messages.
	* The target is no longer able to make legitimate TCP connections.
* In a DDoS (Distributed Denial-Of-Service) attack, the attacker infects many target computers with malware and uses them all to initiate a denial-of-service attack, for example a TCP SYN flood attack.
	* This group of infected computers is called a **botnet**.
### Spoofing Attack
* To **spoof** an address is to use a fake source address (IP or MAC address).
* Numerous attacks involve spoofing, it's not a single kind of attack.
* An example is a **DHCP exhaustion** attack.
	* An attacker uses spoofed MAC addresses to flood DHCP Discover messages.
	* The target server's DHCP pool becomes full, resulting in a denial-of-service to other devices.
### Reflection/Amplification Attacks
* In a **reflection** attack, the attacker sends traffic to a *reflector*, and spoofs the source address of its packets using the target's IP address.
	* The *reflector* (ie. a DNS server) sends the reply to the target's IP address.
	* If the amount of traffic sent to the target is large enough, this can result in a denial-of-service to the target.
* A reflection attack becomes an **amplification** attack when the amount of traffic sent by the attacker is small, but it triggers a large amount of traffic to be sent from the *reflector* to the target.
### Man-in-the-middle Attacks
* In a **man-in-the-middle** attack, the attacker places himself between the source and destination to eavesdrop on communications, or to modify traffic before it reaches the destination.
* This attack compromises the confidentiality and integrity of packets.
* A common example is **ARP spoofing**, also known as **ARP poisoning**. 
	* A host sends an ARP request, asking for the MAC address of another device.
	* The target of the request sends an ARP reply, informing the requester of its MAC address.
	* The attacker waits and sends another ARP reply after the legitimate replier.
	* If the attacker's ARP reply arrives last, it will overwrite the legitimate ARP entry in the requester's ARP table.
	* In the requester's ARP table, the entry for the the destination IP will have the attacker's MAC address. Therefore, the traffic sent from it will be sent to the attacker instead of the intended target.
	* The attacker can inspect or modify the packets, and then forward them to the intended target.
### Reconnaissance Attacks
*  Reconnaissance attacks aren't attacks themselves, but they are used to gather information about a target which can be used for a future attack.
* This is often publicly available information.
* ie. `nslookup` to learn the IP address of a site.
* or a WHOIS query to learn email address, phone numbers, physical addresses, etc.
### Malware
* Malware (malicious software) 
## Passwords/Multi-Factor Authentication (MFA)
## Authentication, Authorization, Accounting (AAA)
## Security Program Elements
