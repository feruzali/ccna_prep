---
description: Ethernet LAN Switching (Part 1)
---

# Day 5

### LAN

**LAN** (Local Area Network) is basically a network contained within a relatively small area like an office, home network, etc. Routers are used to connect separate LANs. So, there are four LANs separated by routers in the example below.

<figure><img src=".gitbook/assets/image (64).png" alt="LANs example" width="563"><figcaption></figcaption></figure>

### Ethernet Frame

During encapsulation, the Ethernet header and trailer are added to the packet in the Data Link layer. There are five fields in the header: **Preamble**, **SFD** (Start Frame Delimiter), **Destination**, **Source**, and **Type** (or Length). And the trailer has only one field - **FCS** (Frame Check Sequence).

#### Preamble & SFD

The **Preamble** is 7 bytes (56 bits) long. It consists of alternating 1's and 0's (`10101010`). Allows devices to synchronize their receiver clocks to make sure that they are ready to receive the rest of the frame. **SFD** is 1 byte (8 bits) long. Its bit pattern is `10101011`. It indicates the end of the preamble and the beginning of the rest of the frame.

#### Destination & Source

**Destination** and **Source** fields indicate the devices sending and receiving the frame. They consist of the destination and source MAC addresses. **MAC** address is a 6-byte (48-bit) unique address of the physical device.

#### Type (Length)

**Type** (Length) is 2 byte (16-bit) field. This field can either represent the type of the encapsulated packet or its length. A value of **1500 or less** indicates the length in bytes. And a value of **1536 or more** indicates the type (usually IPv4 or IPv6). IPv4 Ethernet Type is `0800`, IPv6 Ethernet Type is `86DD`.

#### FCS

**FCS** (Frame Check Sequence) is 4 bytes (32 bits) in length. It detects corrupted data by running a "CRC" (Cyclic Redundancy Check) algorithm over the received data. [Here](https://en.wikipedia.org/wiki/Cyclic\_redundancy\_check) is the explanation of the CRC algorithm.&#x20;

### MAC address

**MAC** (Media Access Control) address is different from an IP address. It is also known as Burnt-In Address (BIA) because it's burnt into the device while it's made. It is a globally unique address. The first 3 bytes of the address are the OUI (Organizationally Unique Identifier), which is assigned to the company making the device. The last 3 bytes are unique to the device itself. These are written as 12 hexadecimal characters. If you are not familiar with the hexadecimal numbering system, you can read more about that [here](https://www.techtarget.com/whatis/definition/hexadecimal).

Let's see how the MAC address is used. Here is a sample network below. Three PCs are connected to the switch, all have MAC addresses.

<figure><img src=".gitbook/assets/image (36).png" alt="sample network" width="563"><figcaption></figcaption></figure>

When PC1 sends a frame to PC2, it uses PC2's MAC address for the destination, no IP here. It is called a **unicast** frame - a frame destined for a single target. PC1 sends the frame via SW1. And when SW1 receives the frame, it looks at the source address of the frame and learns where the PC1 is. It adds PC1's MAC address to its **MAC address table** and associates it with `F0/1` interface. It is called a **dynamically learned** MAC address (**Dynamic** MAC address). Each switch keeps a MAC address table and fills it by looking at the source address of the frames it receives. In Cisco switches, Dynamic MAC addresses are removed from the MAC address table after 5 minutes of inactivity.

<figure><img src=".gitbook/assets/image (97).png" alt="mac address table" width="186"><figcaption></figcaption></figure>

Moving on, the switch needs to forward the frame to the destination but it doesn't know where that is. It is called an **unknown unicast** frame - a frame for which the switch doesn't have an entry in its MAC address table. So, it forwards the frame out of all its interfaces except the one it received the frame (it is called **flooding**). When PC3 receives the frame, it just ignores it because the destination MAC address doesn't match its own MAC address. PC2 receives and processes the frame but until it sends the reply message, SW1 still doesn't know PC2's MAC address. Now PC2 sends a message to PC1, the source address is `AAAA.AA00.0002` and the destination is `AAAA.AA00.0001`. When SW1 receives the frame, it adds PC2's MAC address to its MAC address table and associates it with `F0/2` interface. This time however it doesn't flood the frame. This is known as a **known unicast** frame - a frame for which the switch already has an entry in its MAC address table. SW1 just forwards the frame to its destination.

{% file src=".gitbook/assets/Day 5 Flashcards - Ethernet LAN Switching Part 1.apkg" %}
