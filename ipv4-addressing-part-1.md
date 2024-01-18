---
description: Day 7
---

# IPv4 Addressing (Part 1)

### IPv4&#x20;

<figure><img src=".gitbook/assets/image (38).png" alt="ipv4 header"><figcaption><p>IPv4 header</p></figcaption></figure>

IPv4 addresses are 32 bits (4 bytes) in length and each four groups of numbers represents 8 bits (**octets**), e.g. `192.168.1.254/24` (**dotted decimal format**) is represented as `11000000 10101000 00000001 11111110` in **binary**. If you are not familiar with the binary numbering system, you can read more about it [here](https://byjus.com/maths/binary-number-system/). I strongly recommend reading the article and getting some practice converting binary notation to dotted decimal and vice versa.

`/24` after an IP address is used to identify which part of an IP address represents the network and end host. `/24` means that 24 bits (first 3 octets) of a 32-bit IP address represent a network portion and the remaining 8 bits represent an end host. So, 192.168.1 is a network address and `.254` is a host portion.

Here is one more example where an orange colour represents the network and blue represents a host portion.

<figure><img src=".gitbook/assets/image (88).png" alt="ipv4 address" width="563"><figcaption></figcaption></figure>

However, Cisco devices use a bit older method of writing a prefix length. A netmask is written in a dotted decimal like an IP address where the network portion is all `1` (ones) and the host portion is all `0` (zeroes). For example, `/8` is `255.0.0.0`.

<figure><img src=".gitbook/assets/image (56).png" alt="netmask" width="563"><figcaption></figcaption></figure>

#### IPv4 Classes

The class of an IPv4 address is determined based on the first octet. Class A has a first octet beginning with `0` (zero) and it means the numeric range is 0-127 since the remaining 7 bits of the octet can give a maximum of 127, Class B - `10`, Class C - `110`, etc. Here is a table summarizing IPv4 Classes.

<figure><img src=".gitbook/assets/image (41).png" alt="ipv4 classes" width="375"><figcaption></figcaption></figure>

Class D addresses are reserved for multicast and Class E for experimental uses. Also, the 127 address range is reserved for loopback addresses. **Loopback addresses** are addresses in the range `127.0.0.0` - `127.255.255.255` and used to test the network stack on the local device. If we ping this range of IP addresses, the pings will not go anywhere, they just will be processed on the local device as if it was received from somewhere else.&#x20;

<figure><img src=".gitbook/assets/image (34).png" alt="loopback address ping"><figcaption></figcaption></figure>

Here is a chart of IPv4 Classes with prefixes used.

<figure><img src=".gitbook/assets/image (82).png" alt="ipv4 classes" width="375"><figcaption></figcaption></figure>

A **network address** is an address where the host portion is all `0` (zeroes). It is an identifier of the network itself and cannot be assigned to a host. The first usable address is one above the network address.

A **broadcast address** of the network is an address where the host portion is all `1` (ones). It is the last address of the network and cannot be assigned to a host. The last usable address is one under the broadcast address.

{% file src=".gitbook/assets/Day 7 Flashcards - IPv4 Addresses Part 1.apkg" %}
