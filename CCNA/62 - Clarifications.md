## WLC AAA Override Feature
The AAA Override feature on a Cisco WLC can be used to configure VLAN tagging, QoS, ACLs to individual clients based on Remote authentication Dial-In User Service (RADIUS) attributes.
* When using the AAA Override feature, the access control server, such as Cisco Identity Services Engine (ISE), should be configured with the appropriate override properties.

## RADIUS Change of Authorization (CoA)
It can be used to modify or terminate an already authenticated session. It allows an administrator to send CoA packets from the AAA server. CoA packets can be sent to request session re-authentication, session termination, and more.

## Split-MAC Architecture Traffic Flow
The functionality provided by the lightweight AP includes handling the real-time processing of data, such as sending and receiving 802.11 traffic, responding to beacon and probe messages, encryption, and packet prioritization. In addition, the LAP must send management information to the WLC so that the WLC can forward the information to a management station.

By contrast, a WLC handles tasks that are not time-sensitive, such as security management, lightweight AP configuration management, and client load balancing. It is also responsible for client association requests, data encapsulation, client authentication, key exchange, security policy enforcement, and radio frequency management.