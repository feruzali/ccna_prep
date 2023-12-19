---
description: IPv6 Part 2
---

# Day 32

### EUI-64

Modified EUI-64 (Extended Unique Identifier) is a method of converting a MAC address (48 bits) into a 64-bit interface identifier of a host portion of a `/64` IPv6 address. To convert a MAC address:&#x20;

1. Divide the MAC address in half
2. Insert `fffe` in the middle
3. Invert the 7th bit

E.g. `1234:5678:90ab` becomes `1034:56ff:ffe78:90ab`. Here are a few more examples:

<figure><img src=".gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt="eui-64 process example" width="563"><figcaption></figcaption></figure>

To configure the EUI-64, just add `eui-64` after the network prefix when configuring an IPv6 address on the interface.

### IPv6 Types

#### Global Unicast

Global Unicast IPv6 addresses are public addresses which can be used over the internet. They must be registered to be globally unique. It was originally defined to use the `2000::/3` block. But later defined as all addresses which are not reserved for other purposes. The first 48 bits are a **global routing prefix** assigned by the ISP. The next 16 bits are a **subnet identifier**, used by the enterprise for subnetting. The last 64 bits are an **interface identifier** (host portion).

#### Unique Local

Unique local IPv6 addresses are private addresses which cannot be used over the internet. The address block is `fc00::/7`. They don't require registration and can be used within internal networks. They don't need to be globally unique and can't be routed over the internet. The first two digits must be `fd`. The next 40 bits are called a **global ID** which should be randomly generated.

#### Link-Local

Link-local IPv6 addresses are automatically generated on an IPv6-enabled interface. To enable an IPv6 on an interface, the command `ipv6 enable` is used. The address block is `fe80::/10`. However, according to the standard, the 54 bits after `fe80` should be all 0 (zero). The interface ID is generated using EUI-64. These addresses are used for communication within a single link and are not routed. Primarily used for routing protocol peerings, as next-hop addresses for static routes, and for NDP (IPv6's analogue of ARP).&#x20;

#### Multicast

Multicast addresses are one-to-many communication addresses. IPv6 uses range `ff00::/8` for multicast. IPv6 doesn't use broadcast. Here is a chart of some important multicast addresses:

<figure><img src=".gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt="important multicast addresses" width="563"><figcaption></figcaption></figure>

IPv6 defines multiple multicast **scopes** which indicate how far the packet should be forwarded:

<figure><img src=".gitbook/assets/image (7) (1) (1) (1) (1).png" alt="multicast scopes" width="563"><figcaption></figcaption></figure>

* **Interface-local** (`ff01`) - the packet doesn't leave the local device. It can be used to send traffic to a service within the device itself.
* **Link-local** (`ff02`) - the packet remains in the local subnet and is not routed between subnets.
* **Site-local** (`ff05`) - the packet is forwarded by routers but should be limited to a single physical location.
* **Organization-local** (`ff08`) - wider in scope than site-local (entire company).
* **Global** (`ff0e`) - no boundaries, possible to be routed over the internet.

#### Anycast

Anycast is a new feature of IPv6 and it is one-to-one-of-many communication. Multiple routers are configured with the same address and routers send the packet to the nearest destination (based on the metric) with that IP address configured. For this purpose, a regular unicast address is used and specified as anycast. To configure it, just add the command `anycast` after configuring an IP address on an interface.

#### Other IPv6 addresses

The unspecified IPv6 address - the address with all 0s (zeros). Written as `::`. It can be used when a device doesn't know its IPv6 address yet. IPv4 equivalent is `0.0.0.0`. IPv6 default routes are configured to `::/0`.&#x20;

The loopback address - `::1`. It is used to test the protocol device on the local device. IPv4 equivalent is `127.0.0.0/8`.

{% file src=".gitbook/assets/Day 32 Flashcards - IPv6 (Part 2).apkg" %}

{% file src=".gitbook/assets/Day 32 Lab - IPv6 Configuration Part 2.pkt" %}

{% embed url="https://youtu.be/Zfhpd7dl6QI" %}
