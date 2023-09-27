---
description: Ethernet LAN Switching (Part 2)
---

# Day 6

### Ethernet Frame

The Preamble and SFD are usually not considered a part of the Ethernet header, but they are always present. So, the size of the Ethernet header and trailer is 18 bytes. The minimum size of the Ethernet frame is 64 bytes including the packet. If the packet is less than 46 bytes, padding bytes (all `0`'s) are added.

Let's look at one network example.

<figure><img src=".gitbook/assets/image (102).png" alt="network" width="563"><figcaption></figcaption></figure>

In this network, besides the MAC address, each PC also has an IP address. When PC1 wants to send data to PC3, it specifies its IP address, not its MAC address. When the switch receives the frame, it should forward the frame to PC3. But since switches are Layer 2 devices, they operate with MAC addresses only. So first, the sender has to learn PC3's MAC address. To do so, it uses **ARP**.

### ARP

**ARP** (Address Resolution Protocol) is used to discover the Layer 2 address (MAC address) of a known Layer 3 address (IP address). It consists of 2 messages: **ARP request** and **ARP reply**. ARP request is **broadcast** - sent to all hosts on the network. ARP reply is **unicast** - sent only to one host. ARP Ethernet Type is `0806`.

#### ARP Request

Coming back to our example, the sender has to send an ARP request to learn PC3's MAC address. So, it sends this frame:

<figure><img src=".gitbook/assets/image (62).png" alt="arp request" width="375"><figcaption></figcaption></figure>

`FFFF.FFFF.FFFF` is a broadcast MAC address. When SW1 receives the frame, it first adds the source MAC address to its MAC address table. Then, it floods the frame out of all ports except the one it was received on. PC2 ignores the frame because the destination IP address doesn't match its own IP address. When SW2 receives the frame, it learns PC1's MAC address and then floods the frame. PC4 ignores the frame as well. But PC3 receives it and sends an ARP reply.

#### ARP Reply

PC3 knows PC1's MAC address so it sends the frame directly to PC1 without any broadcast. &#x20;

<figure><img src=".gitbook/assets/image (93).png" alt="arp reply" width="375"><figcaption></figcaption></figure>

SW2 receives the frame and learns PC3's MAC address, and since it knows the PC1's MAC address it directly sends the frame to SW1. SW1 does the same when receives the frame: learns PC3's MAC address and directly forwards the frame to PC1. PC1 finally receives the frame and uses the information to add an entry for PC3 in its **ARP table**.

#### ARP Table

**ARP table** is used to store the IP address to the MAC address association.

<figure><img src=".gitbook/assets/image (106).png" alt="arp table" width="375"><figcaption></figcaption></figure>

The command for viewing the ARP table on your PC is `arp -a`. If the type is `static`, it's a default entry. If the type is `dynamic`, it was learned via ARP request and reply.

### MAC Address Table

To see the MAC address table of the switch, just enter `show mac address-table` in privileged EXEC mode.

<figure><img src=".gitbook/assets/image (111).png" alt="mac address table" width="563"><figcaption></figcaption></figure>

Dynamic MAC addresses are removed from this table after 5 minutes of inactivity. It's known as **ageing**. But it is also possible to manually remove the MAC addresses from the table by using `clear mac address-table dynamic` command. If you want to remove a specific MAC address, you can just continue the previous command with `address` followed by the MAC address of your choice.  So the full command is `clear mac address-table dynamic address` followed by a MAC address. You can also specify a port to clear. The keyword for this is `interface`.&#x20;

### Ping

**Ping** is a network utility to test the reachability. It measures the RTT (round-trip time). It uses two messages: ICMP Echo Request and ICMP Echo Reply (similar to ARP messages). Command to use is `ping` followed by the IP address of the device you want to ping to.

<figure><img src=".gitbook/assets/image (112).png" alt="ping example" width="563"><figcaption></figcaption></figure>

The default Cisco IOS ping settings are:

* 5 ICMP Echo requests (and expected to get 5 ICMP Echo replies)
* size is 100 bytes each

The `.` indicates the failed ping, and `!` indicates the successful ping. It shows the success rate and RTT. The first ping failed because of the ARP, the destination MAC address was unknown. First, it had to learn the destination MAC address using ARP, and at that time the first ping failed.

{% file src=".gitbook/assets/Day 6 Flashcards - Ethernet LAN Switching Part 2.apkg" %}

{% file src=".gitbook/assets/Day 6 Lab - Ethernet LAN Switching.pkt" %}

{% embed url="https://youtu.be/Ig0dSaOQDI8" %}
