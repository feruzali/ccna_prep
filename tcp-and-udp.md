---
description: Day 30
---

# TCP & UDP

### Transport Layer

The transport layer provides Layer 4 addressing (port numbers). TCP also provides some services to applications:

* reliable data transfer
* error recovery
* data sequencing
* flow control

<figure><img src=".gitbook/assets/image (128).png" alt="port number example" width="563"><figcaption></figcaption></figure>

When accessing several services simultaneously, the sessions need to be tracked. A **session** is an exchange of data between two or more communicating devices. The host should be able to handle multiple communication sessions (e.g. multiple internet tabs) at once. So, the combination of source and destination port numbers is used to distinguish between these sessions. **IANA** (Internet Assigned Numbers Authority) has designated the following ranges:

* **Well-known** port numbers: 0 - 1023
* **Registered** port numbers: 1024 - 49151
* **Ephemeral**/**private**/**dynamic** port numbers: 49152 - 65535

Well-known port numbers are used for major protocols (e.g. HTTP, FTP) and very strictly regulated. Registered port numbers require registration to use. Private ports are used when selecting a random source port.

### TCP

* TCP is connection-oriented. Before sending data to the destination host, the two hosts first communicate to establish a connection.&#x20;
* TCP provides reliable communication. The destination host must acknowledge that it received each TCP segment. If not acknowledged within a certain time, the segment is sent again. Hosts set a random initial sequence number. Forward acknowledgement is used to indicate the sequence number of the next segment the host expects to receive.&#x20;
* TCP provides sequencing. Sequence numbers in the TCP header allow destination hosts to put segments in the correct order even when data arrives out of order.
* TCP provides flow control. It helps to regulate the rate data is sent. Acknowledging every single segment is inefficient. The TCP header's **Window Size** field allows more data to be sent before an acknowledgement is required. A **sliding window** can be used to dynamically adjust the window size.

#### Header

<figure><img src=".gitbook/assets/image (129).png" alt="tcp header" width="563"><figcaption><p>TCP Header</p></figcaption></figure>

The source and destination port fields are 16 bits each so there are 65536 available port numbers. Sequence and acknowledgement number fields provide sequencing and reliable communication. `ACK`, `SYN`, and `FIN` flags are used to establish and terminate connections. The window size field is used for flow control.&#x20;

#### 3-way Handshake

<figure><img src=".gitbook/assets/image (130).png" alt="3-way handshake" width="563"><figcaption></figcaption></figure>

Before sending the data, TCP first establishes a connection by using a 3-way handshake. First, the source host sends a TCP segment with a SYN flag set. The destination host then replies with a SYN and ACK flags set. Lastly, the source host sends a TCP segment with an ACK flag set and the connection is established.&#x20;

#### 4-way Handshake

<figure><img src=".gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt="4-way handshake" width="563"><figcaption></figcaption></figure>

To terminate the connection, TCP uses a 4-way handshake. The client sends a TCP segment with a FIN flag set. The server then acknowledges it with an ACK flag set and sends its own TCP segment with a FIN flag. Finally, the client acknowledges it and the connection is terminated.

### UDP

<figure><img src=".gitbook/assets/image (9) (1) (1) (1) (1).png" alt="udp header" width="563"><figcaption><p>UDP Header</p></figcaption></figure>

* UDP is not connection-oriented. The data is sent without any prior connection.
* UDP doesn't provide a reliable communication. There is no concept of acknowledgements and re-transmission. Segments are sent **best-effort**.
* UDP doesn't provide sequencing. There is no sequence number field in the UDP header.&#x20;
* UDP doesn't provide flow control.&#x20;

So, here is a chart comparing TCP with UDP.

<figure><img src=".gitbook/assets/image (10) (1) (1).png" alt="tcp vs. udp" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 30 Flashcards - TCP _ UDP.apkg" %}

{% embed url="https://youtu.be/pJKFahkqMU8" %}
