---
description: Day 15
---

# Subnetting (Part 3 - VLSM)

### Subnetting Class A

The process of subnetting Class A, Class B, and Class C networks is exactly the same. For example, if we are required to subnet a `10.0.0.0/8` network creating 2000 subnets, we use the same formula. Borrowing 11 bits, we create 2048 subnets. The subnet mask is `255.255.224.0`. The prefix length used is `/19`.

Now let's find the number of usable addresses. There are 13 bits remaining. Using the same formula we always used to find the number of usable host addresses, we can figure out that there are 8190 hosts per subnet.

### VLSM

**VLSM** (Variable-Length Subnet Masks) is the process of creating subnets of different sizes, to make the use of network addresses more efficient. Until now, we learned FLSM (Fixed-Length Subnet Masks) - all subnets use the same prefix length. For example, to subnet this example network below, we have to use VLSM.

<figure><img src=".gitbook/assets/image (30).png" alt="vlsm network" width="563"><figcaption></figcaption></figure>

Using VLSM, we can assign different subnet sizes to each LAN. In VLSM, subnets are assigned in order, from the largest to the smallest. So, in our example above, we should first assign the subnet to **Tokyo LAN A**:&#x20;

* Network address: `192.168.1.0/25`
* Broadcast address: `192.168.1.127/25`
* Total number of usable addresses: 126

We divided our network into two and assigned the first half. Using VLSM, we can assign smaller subnets. The second largest LAN is **Toronto LAN B**:

* Network address: `192.168.1.128/26`
* Broadcast address: `192.168.1.191/26`
* Total number of usable addresses: 62

The third is **Toronto LAN A**:

* Network address: `192.168.1.192/27`
* Broadcast address: `192.168.1.223/27`
* Total number of usable addresses: 30

For **Tokyo LAN B**:

* Network address: `192.168.1.224/28`
* Broadcast address: `192.168.1.239/28`
* Total number of usable addresses: 14

And finally, a **point-to-point connection** between two routers:

* Network address: `192.168.1.240/30`
* Broadcast address: `192.168.1.243/30`
* Total number of usable addresses: 2

Not also we were able to provide addresses for all LANs but we even saved some address space thanks to VLSM.

{% file src=".gitbook/assets/Day 15 Lab - VLSM.pkt" %}

{% embed url="https://youtu.be/Rn_E1Qv8--I" %}
