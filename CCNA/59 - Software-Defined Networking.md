## SDN Architecture
![SDN architecture](./img5/sdn-architecture.png)

## SD-ACCESS
![SD-Access Infrastructure](./img5/SD-Access-architecture.png)
* Cisco **SD-Access** is Cisco's SDN solution for automating campus LANs.
	* ACI (Application Centric Infrastructure) is their SDN solution for automating data center networks.
	* SD-WAN is their SDN solution for automating WANs.
* Cisco **DNA (Digital Network Architecture) Center** is the controller at the center of SD-Access.

![SDN underlay](./img5/underlay.png)
* The **underlay** is the underlying physical network of devices and connections (including wired and wireless) which provides IP connectivity (ie. using IS-IS).
	* Multilayer switches and their connections.

![overlay](./img5/overlay.png)
* The **overlay** is the virtual network built on top of the physical underlay network.
	* SD-Access uses VXLAN (Virtual Extensible LAN) to build tunnels.
* When hosts in the network communicate with each other, their traffic is sent over the VXLAN tunnels.

![fabric](./img5/fabric.png)
* the **fabric** is the combination of the overlay and underlay; the physical and virtual network as a whole.

## SD-Access Underlay
* The underlay's purpose is to support the VXLAN tunnels of the overlay.
* There are three different roles of switches in the SD-Access:
	* **Edge nodes**: Connect to tend hosts.
	* **Border nodes**: Connect to devices outside of the SD-Access domain, ie. WAN routers.
	* **Control nodes**: Uses LISP (Locator ID Separation Protocol) to perform various control plane functions.
* You can add AD-Access on top of an existing network (brownfield deployment) if your network hardware and software supports it.
	* Google 'Cisco SD-Access compatibility matrix' if you'r curious.
	* In this case DNA Center won't configure the underlay.
* A new deployment  (greenfield deployment) will be configured by DNA Center to use the optimal SD-Access underlay:
	* 