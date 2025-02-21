## SSL Orchestrator Applications

${\large{\textbf{\textsf{\color{red}Definition}}}}$

An **Application** is the entry point for network traffic into SSL Orchestrator, and is expressed as a number of use cases based on type and direction of traffic flowing through the BIG-IP:

* Inbound Application - Generic inbound application
* Inbound Gateway - Inbound routed "next hop"
* Outbound Gateway - Outbound routed "next hop"
* Outbound Explicit - Outbound explicit proxy
* Inbound/Outbound Layer 2 - A "bump-in-the-wire" pathway

An **Inbound** flow is generally characterized as a reverse proxy, external users sending requests into a locally-managed server environment. In a reverse proxy, TLS offload and certificate management are handled by locally-managed certificates. An **Outbound** flow is generally characterized as a forward proxy, internal users sending requests to external (ex. Internet) resources. In a forward proxy, TLS decryption and re-encryption is handled through an *SSL Forward Proxy* process that forges a copy of the remote server certificate to the internal client.

A **Service Chain** is a logical grouping of services in a defined order through which SSL Orchestrator processes traffic. Security policies match traffic flow conditions, which then assign flows to service chains. The service chain then orchestrates the traffic through the defined set of services in the defined order. An SSL Orchestrator service chain is uniquely different than the “daisy chain” approach of other SSL visibility products. In the SSL Orchestrator service chain model, all services are connected (physically or logically) to SSL Orchestrator. The service chain model improves over the daisy chain model in the following ways:

* If some services are not designed to inspect some types of traffic, a traffic policy can simply send traffic to services that are interested, bypassing those that are not. For example, the policy could be configured to only send outbound HTTP traffic to a HTTP proxy device.
* If a specific throughput requirement is needed for the solution, but not all traffic needs to go to all services, then not all services have to scale at the same rate.
* As these services are independently orchestrated, it becomes easy to scale and perform maintenance (i.e. add/remove devices from individual service pools), without incurring any downtime.









