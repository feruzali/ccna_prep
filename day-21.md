---
description: Spanning Tree Protocol (Part 2)
---

# Day 21

### Spanning Tree Port States

There are four Spanning Tree port states: blocking, listening, learning, and forwarding. Blocking and forwarding stay in a **stable** state until the network gets changed. Listening and Learning are **transitional** states which are passed through when an interface is activated, or when a Blocking port must transition to a Forwarding state due to a change in the network topology.

#### Blocking&#x20;

Non-designated ports are in a Blocking state. Interfaces in a Blocking state are effectively disabled to prevent loops. Interfaces in a Blocking state:

* don't send/receive regular network traffic
* receive STP BPDUs&#x20;
* don't forward STP BPDUs
* don't learn MAC addresses

#### Listening&#x20;

After the Blocking state, interfaces with the Designated or Root role enter the Listening state. Only Designated or Root ports enter the Listening state (Non-designated ports are always Blocking). The Listening state is 15 seconds long by default. This is determined by the **Forward delay timer**. An interface in the Listening state:

* only forwards/receives STP BPDUs
* doesn't send/receive regular traffic
* doesn't learn MAC addresses from regular traffic that arrives on the interface

#### Learning&#x20;

After the Listening state, a Designated or Root port will enter the Learning state. The Learning state is 15 seconds long by default. This is determined by the **Forward delay timer** (the same timer is used for both the Listening and Learning states). An interface in the Learning state:

* only sends/receives STP BPDUs&#x20;
* doesn't send/receive regular traffic
* learns MAC addresses from regular traffic that arrives on the interface

#### Forwarding&#x20;

Root and Designated ports are in a Forwarding state. A port in the Forwarding state&#x20;

* operates as normal
* sends/receives BPDUs
* sends/receives normal traffic
* learns MAC addresses

<figure><img src=".gitbook/assets/image (122).png" alt="Spanning Tree Port States" width="563"><figcaption><p>Spanning Tree Port States</p></figcaption></figure>

### Spanning Tree timers&#x20;

There are 3 Spanning Tree timers: Hello, forward delay, and max age. These timers are created to prevent loops. The STP timers on the root bridge determine the STP timers for the entire network even if they are configured differently on other switches.

#### Hello&#x20;

The hello timer determines how often the root bridge sends Hello BPDUs. By default, it sends them every 2 seconds. The root bridge sends Hello BPDUs and other switches forward them on their designated ports only.

#### Forward delay&#x20;

The forward delay timer is the length of listening and learning transitional states. It is the length of each state, not both combined. By default, it is 15 seconds.

#### Max age

The max age timer indicates how long to wait before changing the STP topology after ceasing to receive Hello BDPUs. By default, it is 20 seconds (10 times of Hello timer). When a switch receives a BPDU message, it starts the timer. Every time a BPDU message is received, the timer is reset. But if a BPDU message is not received within the max age timer, the switch reconsiders its STP choices.

### STP Toolkit

STP Toolkits are features that can be enabled to improve the functionality of STP.

#### Portfast

Portfast allows a port to move to a Forwarding state bypassing Listening and Learning states. It is used to save some time when connecting to an end host. When used, it must be enabled only on ports connected to end hosts. To enable Portfast, enter `spanning-tree portfast` from the interface config level. Another way to enable Portfast is by entering `spanning-tree portfast default` from the global config mode. This enables Portfast on all access ports.

#### BPDU Guard

If an interface with BPDU Guard enabled receives a BPDU from another switch, the interface will be shut down to prevent it from forming a loop. To enable it, enter `spanning-tree bpduguard enable` from the interface config level. Also, you can enter `spanning-tree portfast bpduguard default` from the global config mode. This enables BPDU Guard on all Portfast-enabled interfaces.

### STP Configuration

#### Mode

To configure the STP mode, enter `spanning-tree mode` followed by `mst`/`pvst`/`rapid-pvst` from the global config mode. Modern Cisco switches run rapid PVST by default.

<figure><img src=".gitbook/assets/image (123).png" alt="stp mode config" width="563"><figcaption></figcaption></figure>

#### Root Bridge

You can configure a root bridge by manipulating the bridge priority of the switch. You can also configure the secondary root bridge which will be the second in line to become the root bridge if the main one fails. To configure the root bridge, enter `spanning-tree vlan` followed by VLAN number followed by `root primary` from the global config mode. It sets the priority number to 24576. If another switch already has a priority lower than that, it sets this switch's priority to 4096 less than the current lowest priority. The command to set the secondary root bridge is `spanning-tree vlan` followed by the VLAN number followed by `root secondary`. It sets the STP priority to 28672.

#### Port Settings

To configure the STP port cost or priority, enter `spanning-tree vlan` followed by the VLAN number followed by `cost` for cost or `port-priority` for priority and value.

{% file src=".gitbook/assets/Day 21 Flashcards - STP Part 2.apkg" %}

{% file src=".gitbook/assets/Day 21 Lab - Configuring Spanning Tree.pkt" %}

{% embed url="https://youtu.be/5rpaeJNig2o" %}
