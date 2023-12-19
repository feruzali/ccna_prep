---
description: IPv6 Part 3
---

# Day 33

### IPv6 Header

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="ipv6 header" width="563"><figcaption></figcaption></figure>

IPv6 header is much simpler than IPv4's because it has a fixed size of 40 bytes. Processing of IPv6 header is easier for routers so performance has improved.&#x20;

* **Version** is 4 bits long and has a value of 6 (`0110`) to indicate it is IPv6.
* **Traffic Class** is 8 bits in length and is used for **QoS** (Quality of Service) to indicate high-priority traffic, e.g. live video calls.
* **Flow Label** is 20 bits long and is used to specify specific traffic flows (communications between a specific source and destination).
* **Payload Length** is 16 bits long and indicates the length of the payload (Layer 4 segment) in bytes.&#x20;
* **Next Header** is 8 bits in length and indicates the type of the header of the encapsulated segment, e.g. TCP or UDP. It has the same function as IPv4's **Protocol** field.
* **Hop Limit** is 8 bits long and it has the same function as IPv4's **TTL** field.
* **Source**/**Destination** addresses are 128 bits each.

### NDP

An IPv6 **solicited-node multicast address** is calculated from a unicast address. It begins with `ff02::1:ff` and adds the last 6 hex digits of the unicast address.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="solicited-node multicast address" width="563"><figcaption></figcaption></figure>

**NDP** (Neighbour Discovery Protocol) is a protocol used with IPv6. One of its functions is to replace ARP for IPv6. It uses ICMPv6 and solicited-node multicast addresses to learn the MAC addresses of other hosts. The analogue of the ARP table for IPv6 is the **IPv6 Neighbour Table**. There are two message types used:

*   NS (Neighbour Solicitation) - ICMPv6 Type 135 - analogue of ARP Request\


    <figure><img src=".gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="NS message" width="563"><figcaption></figcaption></figure>
*   NA (Neighbour Advertisement) - ICMPv6 Type 136 - analogue of ARP Reply\


    <figure><img src=".gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt="NA message" width="563"><figcaption></figcaption></figure>

Another function of NDP allows hosts to automatically discover routers on the local network. Two messages are used for this purpose:

* RS (Router Solicitation) - ICMPv6 Type 133. It is sent to the multicast address `ff02::2` (all routers). It asks all routers on the local network to identify themselves. It is sent when an interface is enabled or a host gets connected to a network.
* RA (Router Advertisement) - ICMPv6 Type 134. It is sent to the multicast address `ff02:1` (all nodes). It is sent in response to the RS message. Also, it is sent periodically even if the router hasn't received an RS.

#### SLAAC

**SLAAC** (Stateless Address Auto-configuration) is a standard function of IPv6. Hosts use RS/RA messages to learn the IPv6 prefix of the local link and then automatically generate an IPv6 address. To configure it on an interface, use the command `ipv6 address autoconfig`.

#### DAD

**DAD** (Duplicate Address Detection) allows hosts to check if other devices on the local network are using the same IPv6 address. When an IPv6-enabled interface initializes or gets assigned an IPv6, it performs DAD. DAD uses NS and NA messages. The host sends an NS to its own IPv6 address, and if it doesn't get any reply, the address is unique. If it gets a reply, another host is using the same IPv6 address.

### IPv6 Static Routing

IPv6 routing works the same as IPv4 routing. But these two processes as well as the routing tables are separated. Routes for link-local addresses are not added to the routing table. There are 3 types of static routes (for both IPv4 and IPv6):

* **Directly attached** static route - only the exit interface is specified. It doesn't work in IPv6 if the interface is an Ethernet interface.
* **Recursive** static route - only the next hop is specified.
* **Fully specified** static route - both the exit interface and the next hop are specified.

Floating static routes in IPv6 are configured the same as in IPv4 (by specifying an AD).

Link-local next-hop routes should be fully specified.&#x20;

{% file src=".gitbook/assets/Day 33 Flashcards - IPv6 (Part 3).apkg" %}

{% file src=".gitbook/assets/Day 33 Lab - IPv6 Static Routes.pkt" %}

{% embed url="https://youtu.be/WSBEVFANMmc" %}
