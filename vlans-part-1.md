---
description: Day 16
---

# VLANs (Part 1)

### LAN

A **LAN** is a single broadcast domain including all devices in that broadcast domain. A **broadcast domain** is a group of devices which receive a broadcast frame sent by any one of the members.

<figure><img src=".gitbook/assets/image (113).png" alt="sample network" width="563"><figcaption></figcaption></figure>

Let's take a look at the sample network above. Let's say a PC in the Engineering department sends a broadcast message intended for other PCs in the same department. The switch receives the frame and floods it out. So, all PC even from other departments receive the broadcast. This is a problem for both security and network performance purposes. But since we know how to separate those into subnets let's do so.

<figure><img src=".gitbook/assets/image (114).png" alt="divided into subnets" width="563"><figcaption></figcaption></figure>

Now, as we divided the departments into separate subnets, two departments communicate via the router. But what if the switch receives a broadcast or unknown unicast frame? It still acts the same because it is not aware of Layer 3 subnetting. Although we separated the three departments into three subnets (Layer 3), they are still in the same broadcast domain (Layer 2). This is when the **VLAN**s come in.

### VLAN

Although the devices are in the same LAN, we can use VLANs to separate the devices in Layer 2. We configure VLAN settings on the switch interfaces. And a switch will consider each VLAN as a separate LAN and will not forward the traffic between VLANs. Even if all three departments were in the same subnet, the switch wouldn't send the traffic to another VLAN. Let's assign VLANs like this.

<figure><img src=".gitbook/assets/image (116).png" alt="vlan config" width="563"><figcaption></figcaption></figure>

### VLAN Configuration

To see the VLANs which already exist on the switch, enter the `show vlan brief` command from the privileged EXEC mode. You will probably see some default VLANs which cannot be deleted. The first one is `default` with VLAN number 1. This is the VLAN all interfaces are assigned to by default. And also there are some VLANs used for old technologies. They are not used anymore.&#x20;

To assign the interface to VLAN, enter the interface(s) configuration mode. Use the `switchport mode access` command to set the interface(s) as an **access port**. An access port is a switch port which belongs to a single VLAN and usually connects to end hosts. And the last command is `switchport access vlan` followed by the VLAN number. This is the command which actually assigns the VLAN to the port. If the specified VLAN doesn't exist, it gets created automatically. To manually create a VLAN, enter `vlan` followed by the VLAN number from the global configuration mode. This command is also used to configure a VLAN. To change VLAN's name, the command for assigning the name to VLAN is `name`.

{% file src=".gitbook/assets/Day 16 Flashcards - VLANs Part 1.apkg" %}

{% file src=".gitbook/assets/Day 16 Lab - VLANs Part 1.pkt" %}

{% embed url="https://youtu.be/-tq7f3xtyLQ" %}
