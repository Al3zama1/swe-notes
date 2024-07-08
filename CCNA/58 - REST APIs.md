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
		* Simplifies and decouples the architecture, allowing each part to evolve independently. It ensures that the communication between client and server is standardized and consistent.
	* Client-server.
		* The separation between the client and server means they can both change and evolve independently of each other.
		* When the client application changes or the server application changes, the interface between them must not break.
	* Stateless.
		* Statelessness mandates that each request from the client to the server must contain all of the information necessary to understand and complete the request.
		* The server cannot take advantage of any previously stored context information on the server. For this reason, the client application must entirely keep the session state.
	* Cacheable or non-cacheable.
		* Not all resources have to be cacheable.
		* The cacheable constraint requires that a response should implicitly or explicitly label itself as cacheable or non-cacheable.
		* If the response is cacheable, the client application gets the right to reuse the response data later for equivalent requests and a specified period.
	* Layered system.
		* The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior. In a layered system, each component cannot see beyond the immediate layer they are interacting with.
		* The MVC pattern allows for a clear separation of concerns, making it easier to develop, maintain, and scale the application.
	* Code-on-demand(optional).
		* REST also allows client functionality to extend by downloading and executing code in the form of applets or scripts.
## Cisco DevNet
* Cisco DevNet is Cisco's developer program to help developers and IT professionals who want to write applications and develop integrations with Cisco products, platforms, and APIs.
* DevNet offers lots of free resources such as courses, tutorials, labs, sandboxes, documentation, etc. to learn about automation and develop your skills.
* There is also a DevNet certification track that you can pursue if you're interested in automation.
* We will use their Cisco **DNA Center** Sandbox to send a REST API call using Postman.
	* DNA Center is one of Cisco's SDN controllers.