## APIs
* An API (Application Programming Interface) is a software interface that allows two applications to communicate with each other.
* APIs are essential not just for network automation, but for all kinds of applications.
* In SDN architecture, APIs are used to communicate between apps and the SDN controller (via the NBI), and between the SDN controller and the network device (via the SBI).
* The NBI typically uses REST APIs.
* NETCONF and RESTCONFT are popular southbound APIs.
## REST
* REST stands for Representational State Transfer.
* REST APIs are also know as REST-based APIs or RESTful APIS.
	* REST isn't a specific API. Instead, it describes a set of rules about how the API should work.
* The six constraints of RESTful architecture are:
	* Uniform interface.
	* Client-server.
		* The separation between the client and server means they can both change and evolve independently of each other.
		* When the client application changes or the server application changes, the interface between them must not break.
	* Stateless.
	* Cacheable or non-cacheable.
		* Not all resources have to be cacheable, but cacheable resources MUST be declared as cacheable.
	* Layered system.
	* Code-on-demand(optional).
## Cisco DevNet
* Cisco DevNet is Cisco's developer program to help developers and IT professionals who want to write applications and develop integrations with Cisco products, platforms, and APIs.
* DevNet offers lots of free resources such as courses, tutorials, labs, sandboxes, documentation, etc. to learn about automation and develop your skills.
* There is also a DevNet certification track that you can pursue if you're interested in automation.
* We will use their Cisco **DNA Center** Sandbox to send a REST API call using Postman.
	* DNA Center is one of Cisco's SDN controllers.