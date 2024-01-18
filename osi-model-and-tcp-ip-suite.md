---
description: Day 3
---

# OSI Model & TCP/IP Suite

Networking models categorize and provide a structure for networking protocols and standards. A **protocol** is a set of logical rules defining how network devices and software should work.&#x20;

### OSI Model

<figure><img src=".gitbook/assets/image (104).png" alt="" width="188"><figcaption></figcaption></figure>

OSI (Open Systems Interconnection) model is created by ISO (International Organization for Standardization) and consists of 7 layers. It is a conceptual model that categorizes and standardizes the different functions in a network.&#x20;

When data is sent through the network, it is first processed through the OSI stack, where each layer adds some information to the original data. This process is called **encapsulation**. By the time data reaches the physical layer, it is electrical signals on the wire which is then sent towards the receiver. When the receiving system catches the electrical signals, it starts the opposite process, the additions of each layer are stripped off until it reaches the application layer. This process is called **de-encapsulation**. Both processes are examples of **adjacent-layer interaction** - interaction between the different layers of the OSI model. But the communication between the application layers of two devices is called **same-layer interaction**. **PDU** (Protocol data unit) is a term used to refer to the unit of exchange during different stages of encapsulation/de-encapsulation.

#### Application layer

The application layer is the closest layer to the user which interacts with software applications. It is responsible for identifying communication partners and synchronization.

#### Presentation layer

The presentation layer is responsible for translation between the appropriate application and network formats, e.g. encryption/decryption.

#### Session layer

The session layer controls the sessions between hosts: establishes, manages, and terminates connections between local and remote applications.

#### Transport layer

The transport layer segments (breaks large pieces of data into smaller segments) and reassembles data for communication between hosts. It provides end-to-end communication. The transport layer adds a header to the original data and taken together it is called a **segment**.

#### Network layer

The network layer provides connectivity between hosts on different networks, logical addressing (IP addresses), and path selection which data takes from the source to its destination. Routers operate at Layer 3 (Network layer). The network layer also adds a header to the segment, and now it is called a **packet**.

#### Data Link layer

The data link layer provides node-to-node connectivity and data transfer. It defines how data is formatted for transmission over a physical medium. It detects and may correct Physical layer errors. Uses Layer 2 addressing, different from Layer 3 addressing. Switches operate at Layer 2 (Data Link layer). The data link layer adds a header and a trailer to the packet, and it becomes a **frame**.

#### Physical layer

The physical layer defines the physical characteristics of the medium used to transfer data between devices, e.g. voltage, max distance, and cable specs. Digital bits are converted into electrical (wired) or radio (wireless) signals. Layer 1 PDU is a bit.

### TCP/IP Suite

TCP/IP was developed by the United States Department of Defense through DARPA (Defense Advanced Research Project Agency). It is similar to the OSI model but has fewer layers.

<figure><img src=".gitbook/assets/image (74).png" alt="osi vs tcp/ip comparison"><figcaption><p>OSI vs TCP/IP</p></figcaption></figure>

There are more models representing the network but these two are mainly used. TCP/IP is the model actually used in modern networks but when referring to the Layer numbers, usually OSI model is used.

### Data Flow

Let's look at one sample network topology. Host A is connected to Host B through 2 routers. For forwarding data from host to host, the routers don't need to be aware of higher layers, so only Internet and Link layers are used. Since routers are Layer 3 devices, they de-encapsulate till Layer 3 only and encapsulate again to send the data to the next device. But when it reaches Host B, de-encapsulation is fully processed, so the application receives the data. The Transport layer segment didn't change during the whole process.

<figure><img src=".gitbook/assets/image (31).png" alt="" width="375"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 3 Flashcards - OSI Model, TCP_IP Suite.apkg" %}

{% file src=".gitbook/assets/Day 3 Lab - OSI Model.pkt" %}

{% embed url="https://youtu.be/7nmYoL0t2tU" %}
