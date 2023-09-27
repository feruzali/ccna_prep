---
description: Subnetting (Part 1)
---

# Day 13

### Subnetting

The IANA (Internet Assigned Numbers Authority) assigns IPv4 addresses/networks to companies based on their size. For example, large companies may receive a Class A or Class B network, while a small company might receive a Class C network. But it led to many wasted IP addresses. E.g. when using a point-to-point network - a network connecting only two points ( two offices, branches, cities, etc), only 2 addresses are assigned to these two points, one for the network, and one for the broadcast; even if we use Class C network we waste 252 addresses.&#x20;

The IETF (Internet Engineering Task Force) introduced **CIDR** (Classless Inter-Domain Routing) in 1993 to replace the classful addressing system. With CIDR, larger networks were allowed to be split into smaller networks, allowing greater efficiency. These smaller networks are called **subnetworks** or **subnets**.&#x20;

### Class C subnetting

#### /25

<figure><img src=".gitbook/assets/image (85).png" alt="/25" width="563"><figcaption></figcaption></figure>

The network portion of the address is extended into the first bit of the last octet. And the mask in dotted decimal is now `255.255.255.128`. There are now 7 bits in the host portion of the address, so the number of usable addresses is `2^7-2=126`.

#### /26

<figure><img src=".gitbook/assets/image (43).png" alt="/26" width="563"><figcaption></figcaption></figure>

The mask in dotted decimal is written as `255.255.255.192`. The number of usable addresses is 62.

#### /27

<figure><img src=".gitbook/assets/image (45).png" alt="/27" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.224`. The number of usable addresses is 30.

#### /28

<figure><img src=".gitbook/assets/image (68).png" alt="/28" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.240`. The number of usable addresses is 14.

#### /29

<figure><img src=".gitbook/assets/image (61).png" alt="/29" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.248`. The number of usable addresses is 6.

#### /30

<figure><img src=".gitbook/assets/image (98).png" alt="/30" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.252`. The number of usable addresses is 2 - perfect for point-to-point networks. `203.0.113.0/30` includes the address range of `203.0.113.0` - `203.0.113.3` first address being the network address, the next two are usable addresses, and the last one is a broadcast address. The remaining addresses in the `203.0.113.0/24` address block are available to be used in other subnets.

#### /31

<figure><img src=".gitbook/assets/image (55).png" alt="/31" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.254`. The number of usable addresses is 0. However, this subnet mask can be used for point-to-point networks because it consists of only 2 addresses and there is no need for the network and broadcast addresses. For any other cases, this would be a problem since it leaves no usable addresses after subtracting the network and broadcast addresses.&#x20;

#### /32

<figure><img src=".gitbook/assets/image (60).png" alt="/32" width="563"><figcaption></figcaption></figure>

The mask is `255.255.255.255`. This mask cannot be used here and usually is not used at all for configuration. However, there are some use cases, e.g. when creating a static route to one specific host.

Here is a chart summarizing dotted decimal subnet masks and their equivalent in CIDR notation.

<figure><img src=".gitbook/assets/image (32).png" alt="dotted decimal to cidr notation" width="375"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 13 Flashcards - Subnetting.apkg" %}
