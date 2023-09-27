---
description: First Hop Redundancy Protocols
---

# Day 29

### FHRP

**FHRP** (First Hop Redundancy Protocol) is designed to protect the default gateway used on a subnetwork by allowing two or more routers to provide backup for that address. In the event of failure of an active router, the backup router takes over the address. A virtual IP is configured on two routers, and a virtual MAC address is generated for the virtual IP. An **active** and a **standby** routers are elected. Routers negotiate their roles with each other using multicast Hello messages. End hosts in the network are configured to use the virtual IP as their default gateway. The active router replies to ARP requests using the virtual MAC address. If the active router fails, the standby becomes the next active router. The new active router then sends **gratuitous ARP messages** (ARP replies without any ARP request) to the broadcast address. If the old active router comes back, it becomes the standby router by default. But preemption can be configured so that the old active router takes back its old role.&#x20;

### HSRP

**HSRP** (Hot Standby Router Protocol) is a Cisco proprietary protocol. Active and standby routers are elected. There are two versions:

1. Version 1:&#x20;
   * Multicast address: `224.0.0.2`
   * Virtual MAC address: `0000.0c07.ac**` (`**` is HSRP group number)
2. Version 2:&#x20;
   * Multicast address: `224.0.0.102`
   * Virtual MAC address: `0000.0c9f.f***` (`***` is HSRP group number)

Version 2 adds IPv6 support and increases the number of groups that can be configured. In a situation with multiple subnets/VLANs, different active routers can be configured on each subnet/VLAN for load balancing.&#x20;

#### Configuration

HSRP is configured directly on the interface. To change the version, the command `standby version` followed by the version number is used. Versions should match between the routers. To enable HSRP, use the command `standby` followed by the group number followed by `ip` and the IP address you want to use as the default gateway, e.g. `standby 1 ip 172.16.0.1`. To configure the preemption, enter the command `standby` followed by the group number and `preempt`. It is only necessary to configure on the active router. To see the HSRP configuration, enter the `show standby` command from the privileged EXEC mode. To change the priority, use the command `standby` followed by the group number followed by `priority` and number in the range 0 to 255.&#x20;

The active router is determined in this order:

1. Highest priority (default is 100)
2. Highest IP address

### VRRP

**VRRP** (Virtual Router Redundancy Protocol) is an open standard. Master and backup routers are elected. Multicast IPv4 address is `224.0.0.18`. The virtual MAC address is `0000.5e00.01**` (`**` is VRRP group number). In a situation with multiple subnets/VLANs, different master routers can be configured on each subnet/VLAN for load balancing.&#x20;

### GLBP

**GLBP** (Gateway Load Balancing Protocol) is a Cisco proprietary protocol which load balances among multiple routers within a single subnet. **AVG** (Active Virtual Gateway) is elected. Up to 4 **AVF**s (Active Virtual Forwarders) are assigned by the AVG (AVG can be AVF, too). Each AVF acts as the default gateway for a portion of the hosts in the subnet. Multicast IPv4 address is `224.0.0.102`. The virtual MAC address is `0007.b400.**##` (`**` is GLBP group number, `##` is AVF number).

Here is a chart summarizing the three protocols covered above.

<figure><img src=".gitbook/assets/image (11).png" alt="HSRP protocols summary" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 29 Flashcards - FHRPs.apkg" %}

{% file src=".gitbook/assets/Day 29 Lab - HSRP Configuration.pkt" %}

{% embed url="https://youtu.be/uho5Z2nFhb8" %}
