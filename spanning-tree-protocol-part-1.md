---
description: Day 20
---

# Spanning Tree Protocol (Part 1)

### Redundancy

**Redundancy** is an essential part of network design. Modern networks are expected to run 24/7/365. Even a short downtime can be disastrous for a business. Networks should be designed so that if one component fails, another one takes over with little or no downtime. Most PCs have only one NIC, so they can be plugged into a single switch only. But important servers have multiple NICs, so they can be plugged into multiple switches for redundancy.

#### Broadcast storms

&#x20;

<figure><img src=".gitbook/assets/image (24).png" alt="network topology" width="563"><figcaption></figcaption></figure>

Let's take a look at simple topology. When PC1 wants to send a frame to PC2, it first sends an ARP Request frame which is a broadcast frame. PC2 receives the frame and replies with an ARP Reply.

<figure><img src=".gitbook/assets/image (25).png" alt="network topology" width="563"><figcaption></figcaption></figure>

But the problem is that the broadcast frames between SW2 and SW3 still remain in the network. The Ethernet header doesn't have a TTL field, so the broadcast frames loop around the network forever. If too many looped broadcast frames accumulate in the network, the network gets congested for legitimate traffic to use the network. This is called a **broadcast storm**.

#### MAC Address Flapping&#x20;

Network congestion isn't the only problem. Each time a frame arrives on a switchport the switch uses the source MAC address field to 'learn' the MAC address and update its MAC address table. When frames with the same source MAC address repeatedly arrive on different interfaces, the switch is continuously updating the interface in its MAC address table. This is known as **MAC Address Flapping**.

### STP

**STP** solves these problems. Classic Spanning Tree Protocol is IEEE 802.1D and switches run STP by default. STP prevents Layer 2 loops by placing redundant ports in a blocking state, disabling the interface. They act as backup interfaces that can be activated if the main interface fails. Interfaces in a blocking state only send or receive STP messages called **BPDU**s (Bridge Protocol Data Units). "Bridge" here refers to switches.&#x20;

By selecting which ports are forwarding and which ports are blocking, STP creates a single path to/from each point in the network. STP-enabled switches send/receive Hello BPDUs out of all interfaces, the default timer is 2 seconds. If a switch receives a Hello BPDU on an interface, it knows that the interface is connected to another switch (routers, PCs, etc. do not use STP, so they do not send Hello BPDUs).

#### BPDU

Switches use the **Bridge ID** field in the STP BPDU to select a **root bridge** for the network. The switch with the lowest Bridge ID becomes the root bridge. All ports on the root bridge are put in the forwarding state and other switches in the network must have a path to reach it. Bridge ID consists of 2 fields: **Bridge Priority** (the default is 32768) and the MAC address of the switch.&#x20;

#### Bridge Priority

<figure><img src=".gitbook/assets/image (26).png" alt="bridge priority" width="563"><figcaption></figcaption></figure>

**Bridge Priority** (16 bits) was updated and consists of Bridge Priority (4 bits) and **Extended System ID** (12 bits) fields. Extended System ID is equal to VLAN ID. In the default VLAN of 1, the default bridge priority is 32769 because of the VLAN ID. The STP bridge priority can only be changed in units of 4096.&#x20;

Cisco switches use **PVST** (Per-VLAN Spanning Tree). PVST runs a separate STP instance for each VLAN, so in each VLAN different interfaces can be forwarding/blocking.&#x20;

When first powered on, a switch assumes it is the root bridge. It only gives up its position when it receives a superior BPDU with a lower Bridge ID. When all switches in the topology agree on the root bridge, only the root bridge sends BPDUs, other switches just forward them.

#### Root Port

Each switch selects one of its interfaces as the **root port**. Root ports are also in a forwarding state. The interface with the lowest **root cost** is the root port. Each interface has a Spanning Tree associated root cost. The root cost is the total cost of the outgoing interfaces along the path to the root bridge. The cost of the receiving interface is not counted, only the sending.

<figure><img src=".gitbook/assets/image (27).png" alt="root cost" width="375"><figcaption></figcaption></figure>

So, in the example below, the interface `G0/1` becomes a root port.

<figure><img src=".gitbook/assets/image (28).png" alt="root port example" width="563"><figcaption></figcaption></figure>

If a switch has multiple ports with the same root cost, it selects the interface connected to a switch with the lowest neighbour bridge ID. So, SW3 selects the `G0/0` interface as its root port in the example below.

<figure><img src=".gitbook/assets/image (21).png" alt="lowest neighbour bridge id demo" width="563"><figcaption></figcaption></figure>

The last tie-breaker is a **port ID**. The neighbour with the lowest port ID is selected. STP Port ID is equal to port priority (default 128) and port number.

<figure><img src=".gitbook/assets/image (22).png" alt="port id " width="563"><figcaption></figcaption></figure>

So, SW3 selects the `G0/2` interface as its root port in the example below.

<figure><img src=".gitbook/assets/image (23).png" alt="port id demo" width="563"><figcaption></figcaption></figure>

#### Blocking Port Selection

The switch with the lowest root cost makes its port designated. If the root cost is the same, the switch with the lowest bridge ID makes its port designated. The other switch makes its port non-designated (blocking).

#### Summary

1. One switch is selected as the root bridge. All ports on the root bridge are designated ports (forwarding state). **Root bridge selection**:&#x20;
   1. Lowest bridge ID
2. Each remaining switch will select one of its interfaces to be its root port (forwarding state). Ports across from the root port are always designated ports. **Root port selection**:&#x20;
   1. Lowest root cost&#x20;
   2. Lowest neighbour bridge ID&#x20;
   3. The lowest neighbour port ID
3. Each remaining collision domain will select one interface to be a designated port (forwarding state). The other port in the collision domain will be non-designated (blocking). **Designated port selection**:&#x20;
   1. The interface on a switch with the lowest root cost&#x20;
   2. The interface on a switch with the lowest bridge ID

{% file src=".gitbook/assets/Day 20 Flashcards - STP Part 1.apkg" %}

{% file src=".gitbook/assets/Day 20 Lab - Analyzing STP.pkt" %}

{% embed url="https://youtu.be/Ev9gy7B5hx0" %}
