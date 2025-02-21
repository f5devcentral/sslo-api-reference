## SSL Orchestrator Inspection Services

${\large{\textbf{\textsf{\color{red}Definition}}}}$

An **Inspection Service** represents a single security product (ex. FireEye NX, Palo Alto NGFW, McAfee DLP, etc.). However, a service and a “device” refer to different things in SSL Orchestrator. A device in this case is a single appliance, while a service represents the load balanced and monitored set of like devices. For example, a single FireEye service might define a set of multiple FireEye NX appliances (devices). SSL Orchestrator allows administrators to create many services, each containing a number of like devices. Services fall into five categories based on how they consume network traffic. Almost all modern security products today fit into at least one category, but in some cases a security product can be configured to operate in different modes. SSL Orchestrator supports the following service types:

* **Inline Layer 3** - an inline L3 device is an IP-based device that can route. It is “inline” in the sense that network traffic enters one (physical or logical) interface and routes out another. In this case, the SSL Orchestrator routes to it, and it routes back.
* **TAP** - a TAP device is a passive receive-only service. Intrusion Detection Systems (IDS) are commonly deployed as TAP, and simply receive an out-of-band copy of the network packets.
* **ICAP** - an ICAP device is one that adheres to RFC 3507 specifications. ICAP itself is a payload encapsulation protocol and is often used to encapsulate payloads to various types of services, including DLP and malware detection products. In this case SSL Orchestrator is the ICAP client, encapsulating HTTP request and response payloads to an ICAP service.
* **Inline HTTP** - an inline HTTP device is a subset of inline L3 devices, except that it is a proxy-type device. Proxy-type devices can be transparent or explicit, but the most important difference between HTTP and L3 devices is that HTTP devices, as a function of proxying, change the TCP flows. In particular, a proxy device will always minimally change the source port but may also change source and destination addresses.
* **Inline Layer 2** - an inline L2 device does not have IP addresses and does not participate in routing. It is effectively no more than a physical presence on the wire.
* **Secure Web gateway** - an F5 SWG policy to process layer 7 (HTTP) policy functions.

