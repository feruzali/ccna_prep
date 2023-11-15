---
description: NAT (Part 1)
---

# Day 44

RFC 1918 specifies the following IPv4 address ranges as private:

* `10.0.0.0/8` (10.0.0.0 to 10.255.255.255)
* `172.16.0.0/12` (172.16.0.0 - 172.31.255.255)
* `192.168.0.0/16` (192.168.0.0 - 192.168.255.255)

Private IP addresses can't be used over the internet.

**NAT** (Network Address Translation) is used to modify the source and/or the destination IP addresses of packets. One of the reasons to use NAT is to allow hosts with private addresses to communicate with other hosts over the internet.&#x20;

<figure><img src=".gitbook/assets/image (140).png" alt="nat demo" width="563"><figcaption></figcaption></figure>

#### Static NAT

**Static NAT** involves statically configuring one-to-one mappings of private IP addresses to public IP addresses. It allows devices with private addresses to communicate over the internet. However, it doesn't help to preserve IP addresses. An inside local IP address is mapped to an inside global IP address.&#x20;

* An **inside local** address is the IP address of the inside host from the perspective of the local network - the IP address actually configured on the interface (usually a private address).&#x20;
* An **inside global** address is the IP address of the inside host from the perspective of outside hosts - the IP address of the inside host after NAT (usually a public address).&#x20;
* An **outside local** address is the IP address of the outside host from the perspective of the local network.
* An **outside global** address is the IP address of the outside host from the perspective of the outside network.

#### Configuration

To configure static NAT on Cisco IOS:

1. Define the inside and outside interfaces and from the interface config mode enter the command `ip nat` followed by `inside` - for the internal network, `outside` - for the external network.&#x20;
2. Configure the one-to-one IP address mappings - `ip nat inside source static` followed by the inside local and the inside global IP addresses.

To view the active NAT translations, use the command `show ip nat translations`. To clear the NAT translation table, use the command `clear ip nat translation *`. This deletes all entries for dynamic NAT translations. Static NAT entries remain the same. To view the NAT statistics, enter the command `show ip nat statistics`.

<figure><img src=".gitbook/assets/image (141).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 44 Flashcards - NAT (Part 1).apkg" %}

{% file src=".gitbook/assets/Day 44 Lab - Static NAT.pkt" %}

{% embed url="https://youtu.be/vir6n_NVZFw" %}
