---
description: IPv6 Part 1
---

# Day 31

### IPv6

An IPv6 address is 128 bits long. It uses the slash (`/`) notation to indicate the prefix length.

IPv6 addresses can be abbreviated:

* Leading 0s (zeros) can be removed, e.g. `2001:0db8:000c:002b:201b:0020:0080:34bd` becomes `2001:db8:c:2b:201b:20:80:34bd`&#x20;
* Consecutive quarters of all 0s (zeros) can be replaced with a double colon (`::`), e.g. `2001:0db8:0000:0000:0000:0000:0080:34bd` becomes `2001:0db8::0080:34bd`. And if both methods are combined it becomes `2001:db8::80:34bd`. But it can be used only once per address. &#x20;

Here are a few more examples:

<figure><img src=".gitbook/assets/image (131).png" alt="shortened IPv6 address examples" width="563"><figcaption></figcaption></figure>

#### Prefix

The enterprise requesting an IPv6 address from the ISP receives a `/48` block address. IPv6 subnets use a `/64` prefix length. So, the enterprise has 16 bits to make subnets. The remaining 64 bits can be used for the host portion. Even if the prefix length is not `/64`, if it is a multiple of 4, it is easy to find the prefix length because each hexadecimal character is 4 bits.  Here is an example of how to find a network address of the host using the prefix length other than `/64:`

<figure><img src=".gitbook/assets/image (132).png" alt="/56 address network portion" width="563"><figcaption></figcaption></figure>

But if the prefix length is not a multiple of 4, you have to go through some extra steps to find a network portion.

<figure><img src=".gitbook/assets/image (133).png" alt="/93 network portion example" width="563"><figcaption></figcaption></figure>

Here are a few more examples:

<figure><img src=".gitbook/assets/image (134).png" alt="host address - prefix examples" width="563"><figcaption></figcaption></figure>

#### Configuration

First, to enable IPv6 routing on the router, enter the command `ipv6 unicast-routing` from the global config mode. Then, to assign an IPv6 address on an interface, enter the interface config mode and use the command `ipv6 address` followed by an address and a prefix length. A shortened version of the address can also be entered. To check the IPv6-enabled interfaces, use the command `show ipv6 interfaces brief`. Each interface is also automatically assigned a **link-local address** when an IPv6 is enabled on the interface.

{% file src=".gitbook/assets/Day 31 Flashcards - IPv6 Part 1.apkg" %}

{% file src=".gitbook/assets/Day 31 Lab - IPv6 Configuration Part 1.pkt" %}

{% embed url="https://youtu.be/BdsIahtrWIA" %}
