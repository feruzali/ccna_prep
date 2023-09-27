---
description: IPv4 Header
---

# Day 10

### IPv4 Header

<figure><img src=".gitbook/assets/image (38).png" alt="ipv4 header"><figcaption></figcaption></figure>

#### Version

**Version** is 4 bits long and it identifies the version of IP used: IPv4 - 4 (`0100`) or IPv6 - 6 (`0110`). IPv6 has a different structure of the header.

#### IHL

**IHL** (Internet Header Length) is 4 bits long. The final field of the IPv4 header (**Options**) is variable in length, so this field is necessary to indicate the total length of the header. It identifies the length in 4-byte increments, e.g. if the value is 5, then the length is 20 bytes. The minimum value is 5, and the maximum is 15. So, the minimum IPv4 header length is 20 bytes, and the maximum is 60 bytes.

#### DSCP

**DSCP** (Differentiated Services Code Point) is 6 bits long. It is used for QoS (Quality of Service), to prioritize delay-sensitive data (video/audio streaming).&#x20;

#### ECN

**ECN** (Explicit Congestion Notification) is 2 bits in length. It provides end-to-end notification of network congestion without dropping packets. It is an optional field which requires both endpoints and the underlying network infrastructure to support it.

#### Total Length

**Total Length** is 16 bits long and indicated the total length of the packet in bytes. The minimum value is 20, and the maximum is 65535 (maximum 16-bit value).

#### Identification

**Identification** field is 16 bits. If a packet is fragmented because of being too large, this field helps to identify which packet the fragment belongs to. All fragments of the same packet will have their own IPv4 header with the same value in this field. Packets are fragmented if larger than the **MTU** (Maximum Transmission Unit). The MTU is usually 1500 bytes.

#### Flags

**Flags** field in 3 bits and used to control/identify fragments. The first bit is always set to 0 (zero). The second bit is **DF** (Don't Fragment) bit and is used to indicate that the packet should not be fragmented. The third bit is **MF** (More Fragments) bit and is set to 1 if there are more fragments in the packet or 0 (zero) for the last fragment or if a packet is not fragmented.

#### Fragment Offset

**Fragment Offset** is 13 bits long and is used to indicate the position of the fragment within the original packet. It allows fragmented packets to reassemble even if they arrive out of order.

#### Time To Live

**TTL** is 8 bits long field. It is used to prevent infinite loops when the packet is continuously sent around without reaching its destination. It indicates a **hop count** - each time router receives a packet, it decreases the TTL value by 1. And when it reaches 0 (zero), a router drops the packet. The recommended default value of TTL is 64.

#### Protocol

**Protocol** field length is 8 bits and it indicates the protocol of the encapsulated segment (Layer 4 PDU). Value 6 is used for **TCP**, 17 - for **UDP**, 1 - for **ICMP**, and 89 - for **OSPF** (Open Shortest Path First).&#x20;

#### Header Checksum

**Header Checksum** is 16 bits long. A calculated checksum is used to check for errors in the IPv4 header. When a router receives a packet, it calculates the header checksum and compares it to the one in the header. If there is a mismatch, the router drops the packet.

#### Source/Destination IP Addresses

An IP address is 32 bits long. Source indicates the sender, and destination - the intended receiver.

#### Options

The length of the **Options** field is 0-320 bits. This field is optional and rarely used. If the IHL field is greater than 5, Options are present.

{% file src=".gitbook/assets/Day 10 Flashcards - IPv4 Header.apkg" %}
