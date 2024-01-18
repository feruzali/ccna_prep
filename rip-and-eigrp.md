---
description: Day 25
---

# RIP & EIGRP

### RIP

RIP (Routing Information Protocol) uses hop count as its metric. The maximum hop count is 15. It is not usually used in real networks. It has three versions:

* RIPv1 and RIPv2 - used for IPv4
* RIPng (RIP Next Generation) - used for IPv6

It uses two message types:

* Request - to ask neighbours to send their routing table
* Response - to send the local router's routing table to neighbouring routers

By default, routing tables are shared every 30 seconds.

#### Versions

RIPv1:

* only advertises classful addresses
* doesn't include subnet mask information
* doesn't support VLSM, CIDR
* messages are broadcast to `255.255.255.255`

RIPv2:

* supports VLSM, CIDR
* includes subnet mask information
* messages are multicast to `224.0.0.9`

#### Configuration

First, enter the RIP config mode, using the command `router rip` from the global config mode. Choose a version with the command `version` followed by the version number. To disable classful networking logic use the command `no auto-summary`. Then you have to use the `network` command. The `network` command tells the router to:

* look for an interface with an IP address that is in the specified range
* activate RIP on the interfaces that fall in the range
* form adjacencies with connected RIP neighbours
* advertise the network prefix of the interface

If there are no RIP neighbours connected to the interface, the interface should be configured as a passive interface so that the router doesn't send RIP advertisements out of the interface. To do so, use the command `passive interface` followed by the interface number. The command is entered from the RIP config mode. To advertise the default route via RIP, use the command `default-information originate`. To check the information on the routing protocol being used, enter the command `show ip protocols` from the privileged EXEC mode.

### EIGRP

EIGRP (Enhanced Interior Gateway Routing Protocol) is a Cisco proprietary protocol that is considered an advanced distance vector routing protocol. It is much faster than RIP and doesn't have a 15 hop-count limit. It sends messages using a multicast address `224.0.0.10`. By default, it load-balances like RIP over 4 paths but it is the only IGP that can perform unequal-cost load-balancing.

#### Configuration

To enter the EIGRP config mode, use the command `router eigrp` followed by the AS number. The AS (Autonomous System) number must match between the routers to form an adjacency. Auto-summary and passive-interface configurations are the same as in RIP. The `network` command assumes a classful address if the network mask is not specified. EIGRP uses a wildcard mask instead of a regular subnet mask. A wildcard mask is just an inverted subnet mask. All `1`s in the subnet mask are `0` (zero) in the equivalent wildcard mask and vice versa.

{% file src=".gitbook/assets/Day 25 Flashcards - RIP _ EIGRP.apkg" %}

{% file src=".gitbook/assets/Day 25 Lab - EIGRP Configuration.pkt" %}

{% file src=".gitbook/assets/Day 25 Lab - Extra Flashcards - EIGRP Terms.apkg" %}

{% embed url="https://youtu.be/ffnJ5oBIObY" %}
