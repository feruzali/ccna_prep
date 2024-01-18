---
description: Day 53
---

# WAN Architectures

A **WAN** (Wide Area Network) is a network that extends over a large geographical area. WANs are used to connect geographically separate LANs.&#x20;

<figure><img src=".gitbook/assets/image (9) (1) (1).png" alt="WAN example" width="563"><figcaption></figcaption></figure>

### Leased Lines

A leased line is a dedicated physical link, typically connecting two sites. Leased lines use serial connections (PPP or HDLC encapsulation). Various standards provide different speeds and different standards are available in different countries.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt="leased line standards" width="563"><figcaption></figcaption></figure>

Ethernet WAN technologies are becoming popular because of the higher cost, higher installation lead time and slower speed of leased lines.

### MPLS

Similar to the Internet, the service provider's **MPLS** (Multi-Protocol Label Switching) networks are shared infrastructure because many customer enterprises connect to and share the same infrastructure to make WAN connections. When the PE routers receive frames from the CE router, they add a label to the interface. These labels are used instead of the IP address to make forwarding decisions within the service provider's network.

* CE router - Customer Edge router
* PE router - Provider Edge router
* P router - Provided core router

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt="MPLS example" width="563"><figcaption></figcaption></figure>

The CE routers don't use MPLS. When using a Layer 3 MPLS VPN, the CE and PE routers peer using OSPF to share routing information. When using a Layer 2 MPLS VPN, the CE and PE routers don't perform peerings. The service provider network is entirely transparent to the CE routers. It's like the two CE routers are directly connected. If a routing protocol is used, the two CE routers peer directly with each other.&#x20;

<figure><img src=".gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt="MPLS VPN example" width="563"><figcaption></figcaption></figure>

### Internet Connections

#### DSL

**DSL** (Digital Subscriber Line) provides internet connectivity to customers over phone lines and can share the same phone line that is already installed in most homes. A DSL **modem** (modulator-demodulator) is required to convert data into a format suitable to be sent over the phone lines. The modem might be incorporated into the home router or be a separate device.

<figure><img src=".gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt="DSL example" width="563"><figcaption></figcaption></figure>

#### Cable Internet

CableInternet provides internet access via the same **CATV** (Cable Television) lines used for TV service. Like DSL, a cable modem is required to convert data into a format suitable to be sent over the CATV cables. Like a DSL modem, this can be built into the home router or be a separate device.

<figure><img src=".gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt="CATV example" width="563"><figcaption></figcaption></figure>

#### Redundancy

* **Single Homed** - 1 connection to 1 ISP
* **Dual Homed** - 2 connections to 1 ISP
* **Multihomed** - 1 connection to each of 2 ISPs
* **Dual Multihomed** - 2 connections to each of 2 ISPs

### Site-to-Site VPNs

When using the Internet as a WAN to connect sites, there is no built-in security by default. To provide secure communications over the Internet **VPN**s (Virtual Private Networks) are used.&#x20;

A **site-to-site** VPNs typically use IPsec (IP security). It is a VPN between two devices and is used to connect two sites over the Internet. It is typically used to permanently connect two sites. Site-to-site VPNs provide service to many devices within the sites they are connecting. A VPN **tunnel** is created between the two devices by encapsulating the original IP packet with a VPN header and a new IP header. When using IPsec, the original packet is encrypted before being encapsulated with the new header.&#x20;

1. The sending device combines the original packet and session key (encryption key) and runs them through an encryption formula.
2. The sending device encapsulates the encrypted packet with a VPN header and a new IP header.
3. The sending device sends the new packet to the device on the other side of the tunnel.
4. The receiving device decrypts the data to get the original packet and then forwards the original packet to its destination.

#### GRE over IPsec

IPsec doesn't support broadcast and multicast traffic, only unicast. E.g. OSPF can't be used over the tunnels because it relies on multicast traffic. **GRE** (Generic Routing Encapsulation) can encapsulate a variety of Layer 3 protocols as well as broadcast and multicast messages. It creates tunnels like IPsec, however it doesn't encrypt the original packet. We can use GRE over IPsec to get the flexibility of GRE with the security of IPsec. The original packet is encapsulated by a GRE header and a new IP header. Then the GRE packet is encrypted and encapsulated within an IPsec VPN header and a new IP header.

#### DMVPN

Configuring a full mesh of tunnels between many sites is labor-intensive work. **DMVPN** (Dynamic Multipoint VPN) is a Cisco-developed solution that allows routers to dynamically create a full mesh of IPsec tunnels without having to manually configure every single tunnel.

1. IPsec tunnels are configured to a hub site.
2. The hub router gives each router information on how to form an IPsec tunnel with other routers.

### Remote-Access VPNs

Whereas site-to-site VPNs are used to make a point-to-point connection between two sites over the Internet, remote-access VPNs are used to allow end devices to access the company's internal resources securely over the Internet. They provide on-demand access to one end device the VPN client software is installed on. Remote-access VPNs typically use **TLS** (Transport Layer Security). TLS was formerly known as **SSL** (Secure Sockets Layer).&#x20;

VPN client software is installed on end devices. These end devices then form secure tunnels to one of the company's routers/firewalls acting as a TLS server. This allows the end users to securely access resources on the company's internal network without being directly connected to the company network.&#x20;

<figure><img src=".gitbook/assets/image (8) (1) (1) (1) (1).png" alt="Remote-access VPN demo" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 53 Flashcards - WAN Architectures.apkg" %}

{% file src=".gitbook/assets/Day 53 Lab - GRE Tunnels.pkt" %}

{% embed url="https://youtu.be/_MMuU5viinM" %}
