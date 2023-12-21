---
description: Network Automation
---

# Day 59

Network automation provides many key benefits:

* Human error (ie typos) is reduced.
* Networks become more scalable. New deployments and network-wide changes can be implemented much faster.
* Network-wide policy compliance is assured.
* The improved network operation efficiency reduces the network's opex (operating expenses).

### Logical Planes

The various functions of network devices can be logically categorized into planes: data plane, control plane, and management plane.

*   **Data plane** - all tasks forwarding user data/traffic from one interface to another are part of the data plane (aka **forwarding plane**). A router/switch receives a message and forwards it out of the appropriate interface. It also de-encapsulates the original header and re-encapsulates it with a new header. NAT, deciding to forward or discard messages due to ACLs, port security, etc. is also a part of the data plane.\


    <figure><img src=".gitbook/assets/image (164).png" alt="data plane" width="563"><figcaption></figcaption></figure>
*   **Control plane** - functions that build routing tables, MAC address tables, ARP tables, STP, etc. are part of the control plane. The control plane controls what the data plane does. The control plane performs overhead work, e.g. OSPF itself doesn't forward user data packets but it tells the data plane how packets should be forwarded.\


    <figure><img src=".gitbook/assets/image (165).png" alt="control plane" width="563"><figcaption></figcaption></figure>
*   **Management plane** - performs overhead work. It doesn't directly affect the forwarding process of messages. It consists of protocols that are used to manage devices, e.g. SSH/Telnet, Syslog, SNMP, NTP, etc.\


    <figure><img src=".gitbook/assets/image (166).png" alt="management plane" width="563"><figcaption></figcaption></figure>

The operation of the management and control planes are managed by the CPU. However, the CPU is relatively slow for data plane operations. **ASIC** (Application-Specific Integrated Circuit) chips are built for this purpose. When a switch receives a frame, the ASIC is responsible for switching logic and the MAC address table (aka **CAM table**) is stored in a kind of memory called **TCAM** (Ternary Content-Addressable Memory).

### SDN

**SDN** (Software-Defined Networking) is aka **SDA** (Software-Defined Architecture) or **Controller-Based Networking**. It is an approach to networking that centralizes the control plane into an application called a **controller**. The controller can interact programmatically with the network devices using **API**s (Application Programming Interface).

<figure><img src=".gitbook/assets/image (167).png" alt="SDN demo" width="563"><figcaption></figcaption></figure>

#### SBI

The **SBI** (SouthBound Interface) is used for communication between the controller and the network device it controls. It consists of a communication protocol and API. APIs facilitate data exchanges between programs. Examples of SBIs include OpenFlow, Cisco OpFlex, Cisco onePK, and NETCONF. Using the SBI, the controller communicates with managed devices and gathers information like the devices in the network, the topology, the available interface on each device, their configurations, etc.

#### NBI

The **NBI** (NorthBound Interface) is what allows us to interact with the controller, access the data it gathers about the network, program it, and make changes in the network via the SBI. A **REST** (Representational State Transfer) API is used on the controller as an interface for apps to interact with it. Data is sent in a structured format such as JSON or XML.

<figure><img src=".gitbook/assets/image (168).png" alt="SBI and NBI demo" width="563"><figcaption></figcaption></figure>

{% file src=".gitbook/assets/Day 59 Flashcards - Network Automation.apkg" %}
