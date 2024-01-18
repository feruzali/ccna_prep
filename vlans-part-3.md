---
description: Day 18
---

# VLANs (Part 3)

### Native VLAN on a Router

There are 2 methods to configure a native VLAN on a router:

1. Using the command `encapsulation dot1q` followed by VLAN id and `native` on the router subinterface. This tells the router that this subinterface belongs to the native VLAN.
2. Configuring an IP address for the native VLAN on the router's physical interface. But first, you may need to delete the subinterface of this VLAN on the router.

### Layer 3 (Multilayer) Switches

<figure><img src=".gitbook/assets/image (29).png" alt="layer 3 switch icon" width="375"><figcaption></figcaption></figure>

A **multilayer switch** has a lot of advantages over a Layer 2 switch:&#x20;

* It is capable of both switching and routing.&#x20;
* You can assign IP addresses to its interfaces.&#x20;
* You can create virtual interfaces and assign IP addresses to those as well.&#x20;
* You can configure routes, just like a router.
* It can be used for inter-VLAN routing, unlike Layer 2 switches.

### SVI

**SVIs** (Switch Virtual Interfaces) are virtual interfaces with assigned IP addresses in a multilayer switch. It is used to avoid using a router for inter-VLAN routing. Gateway addresses on PCs should be configured to use the SVI. For the packets destined outside the LAN, a separate subnet is created between the Layer 3 switch and the router. Then a default route pointing to the router is configured on the switch. The command which enables Layer 3 routing on a switch is `ip routing`, entered from the global configuration mode. The command to change a switch port (Layer 2) to a routed port (Layer 3) is `no switchport`, entered from the interface config mode.

To configure an SVI, first, you need to create one. The command is `interface vlan` followed by the VLAN id existing on the switch. Then, assign an IP address and enable the interface with `no shutdown` command. SVIs are shut down by default.

Requirements for an SVI to be `up/up`:

* The VLAN must exist on the switch
* The switch must have at least one access or trunk port in the VLAN in an `up/up` state
* The VLAN must not be shut down
* The SVI must not be shut down

{% file src=".gitbook/assets/Day 18 Flashcards - VLANs Part 3.apkg" %}

{% file src=".gitbook/assets/Day 18 Lab - Multilayer Switching.pkt" %}

{% embed url="https://youtu.be/MQcCr3QW1vE" %}
