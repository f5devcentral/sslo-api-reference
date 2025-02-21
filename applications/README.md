## SSL Orchestrator Applications

${\large{\textbf{\textsf{\color{red}Definition}}}}$

An **Application** is the entry point for network traffic into SSL Orchestrator, and is expressed as a number of use cases based on type and direction of traffic flowing through the BIG-IP:

* Inbound Application - Generic inbound application
* Inbound Gateway - Inbound routed "next hop"
* Outbound Gateway - Outbound routed "next hop"
* Outbound Explicit - Outbound explicit proxy
* Inbound/Outbound Layer 2 - A "bump-in-the-wire" pathway

An **Inbound** flow is generally characterized as a reverse proxy, external users sending requests into a locally-managed server environment. In a reverse proxy, TLS offload and certificate management are handled by locally-managed certificates. An **Outbound** flow is generally characterized as a forward proxy, internal users sending requests to external (ex. Internet) resources. In a forward proxy, TLS decryption and re-encryption is handled through an *SSL Forward Proxy* process that forges a copy of the remote server certificate to the internal client.









