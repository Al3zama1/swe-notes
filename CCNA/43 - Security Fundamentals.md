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
	* Should be implemented everywhere a vulnerability can be exploited: client devices, servers, switches, routers, firewalls, etc.
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
* **Malware** (malicious software) refers to a variety of harmful programs that can infect a computer.
* **viruses** infect other software (a 'host program). The virus spreads as the software is shared by users. Typically they corrupt or modify files on the target computer.
* **Worms** do not require a hot program. They are standalone malware and they are able to spread on their own, without user interaction. The spread of worms can congest the network, but the 'payload' of a worm can cause additional harm to target devices.
* **Trojan Horses** are harmful software that is disguised as legitimate software. They are spread through user interactions such as opening email attachments, or downloading a file from the internet.
* The above malware types can exploit various vulnerabilities to threaten any of the CIA of the target device. There are many types of malware!
### Social Engineering Attacks
* Social engineering attacks target the most vulnerable part of any system - people!
* They involve psychological manipulation to make the target reveal confidential information or perform some action.
* **Phishing** typically involves fraudulent emails that appear to come from a legitimate business (Amazon, bank, credit card company, etc) and contain links to a fraudulent website that seems legitimate.
	* **Spear phishing** is a more targeted form of phishing, ie. aimed at employees of a certain company.
	* **Whaling** is phishing targeted at high-profile individuals, ie. a company president.
* **Vishing** (voice phishing) is phishing performed over the phone.
* **Smishing** (SMS phishing) is phishing using SMS text messages.

* **Watering hole** attacks compromise sites that the target victim frequently visits. If a malicious link is placed on a website the target trusts, they might not hesitate to click it.
* **Tailgating** attacks involve entering restricted, secured areas by simply walking in behind an authorized person as they enter. Often, the target will hold the door open for the attacker to be polite, assuming the attacker is also authorized to enter.
### Password-related Attacks
* Most systems use a username/password combination to authenticate users.
* The username is often simple/easy to guess (for example, the user's email address) , and the strength and secrecy of the password is relied on to provide the necessary security.
* Attackers can learn a user's password via multiple methods:
	* Guessing.
	* **Dictionary attacks**: A program runs through a 'dictionary' or list of common words/passwords to find the target's password.
	* **Brute force attack**: A program tries every possible combination of letters, numbers, and special characters to find the target's password.
* String passwords should contains:
	* At least 8 characters.
	* A mixture of uppercase and lowercase letters.
	* A mixture of letters and numbers.
	* One or more special characters.
	* Should be changed regularly.
## Passwords/Multi-Factor Authentication (MFA)
* **Multi-factor authentication** involves providing more than just a username/password to prove your identity.
* It usually involves providing two of the following (=two factor authentication):
	* **Something you know**: a username/password combination, a PIN, etc.
	* **Something you have**: pressing a notification that appear on your phone, a badge that is scanned, etc.
	* **Something you are**: biometrics such a a face scan, palm scan, fingerprint scan, retina scan, etc.
* Requiring multiple factors of authentication greatly increases the security. Even if an attacker learns the target's password (**something you know**), they won't be able to login to the target's account.
## Digital Certificates
* **Digital certificates** are another form of authentication used to prove the identify of the holder of the certificate.
* They are used for websites to verify that the website being accesses is legitimate.
* Entities that want a certificate to prove their identify send a CSR (Certificate Signing Request) to a CA (Certificate Authority), which will generate and sign the certificates.
## Authentication, Authorization, Accounting (AAA)
For the CCNA, know the difference between Authentication, Authorization, and Accounting.

* **AAA** (triple-A) stands for **A**uthentication, **A**uthorization, and **A**ccounting.
* **Authentication** is the process of verifying a user's identity.
	* Logging in.
* **Authorization** is the process of granting the user the appropriate access and permissions.
	* Granting the user access to some files/services, restricting access to other files/services.
* **Accounting** is the process of recording the user's activities on the system.
	* Logging when a user makes a change to a file, etc.
* Enterprises typically use a AAA server to provide AAA services.
	* ISE (Identity Services Engine) is Cisco's AAA server.
* AAA servers usually support the following two AAA protocols:
	* **RADIUS**: an open standard protocol. Uses UDP ports 1812 and 1813.
	* **TACACS+**: A Cisco proprietary protocol. Uses TCP port 49.
## Security Program Elements
* **User awareness** programs are designed to make employees aware of potential security threads and risks.
	* For example, a company might send out false phishing emails to make employees click a link and sing in with their login credentials.
	* Although the emails are harmless, employees who fall for the false emails will be informed that it is part of a user awareness program and they should be more careful about phishing emails.
* **User training** programs are more formal than user awareness programs.
	* For example, dedicated training sessions which educate users on the corporate security policies, how to create strong passwords, and how to avoid potential threads.
* **Physical access control** protects equipment and data from potential attackers by only allowing authorized users into protected areas such as network closets or data center floors.
	* Multi-factor locks can protect access to restricted areas.
		* ie. a door that requires users to swipe a badge and scan their fingerprints to enter.
		* Permissions of the bade can easily be change. For example, permissions can be removed when an employee leaves the company.