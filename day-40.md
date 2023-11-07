---
description: SNMP
---

# Day 40

**SNMP** (Simple Network Management Protocol) is an industry-standard framework and protocol that was originally released in 1988. SNMP can be used to monitor the status of the devices, make configuration changes, etc. There are two main types of devices in SNMP:

1. **Managed devices** - the devices being managed using SNMP. Like routers, switches, etc. They listen on UDP port 161.
2. **NMS** (Network Management Station) - SNMP server. This is the device managing the managed devices. It listens on UDP port 162.

There are three main operations used in SNMP:

1. Managed devices can notify the NMS of events.
2. The NMS can ask the managed devices for information about their current status.
3. The NMS can tell the managed devices to change their configuration settings.

Here are the main SNMP components:

<figure><img src=".gitbook/assets/image (136).png" alt="snmp components" width="563"><figcaption></figcaption></figure>

The **SNMP Manager** is the software on the NMS that interacts with the managed devices. It receives notifications, sends requests for information, sends configuration changes, etc. The **SNMP Application** provides an interface for the network admin to interact with. It displays alerts, stats, charts, etc.

The **SNMP Agent** is the SNMP software running on the managed devices that interacts with the SNMP Manager on the NMS. It communicates with the NMS. **MIB** (Management Information Base) is the structure that contains the variables that are managed by SNMP. Each variable is identified with an **OID**(Object ID). SNMP OIDs are organized in a hierarchical structure.&#x20;

<figure><img src=".gitbook/assets/image (137).png" alt="oid demo" width="563"><figcaption></figcaption></figure>

#### Versions

* **SNMPv1** is the original version of SNMP.
* **SNMPv2c** - allows the NMS to retrieve large amounts of data in a single request. `c` refers to **community strings** used as passwords in SNMPv1, removed in SNMPv2, added back in SNMPv2c.
* **SNMPv3** - a much more secure version of SNMP that supports strong encryption and authentication.&#x20;

#### SNMP Messages

<table><thead><tr><th width="174">Message Class</th><th width="395.3333333333333">Description</th><th>Messages</th></tr></thead><tbody><tr><td><strong>Read</strong></td><td>Sent by the NMS to read information from the managed devices</td><td>Get<br>GetNext<br>GetBulk</td></tr><tr><td><strong>Write</strong></td><td>Sent by the NMS to change information on the managed devices</td><td>Set</td></tr><tr><td><strong>Notification</strong></td><td>Sent by the managed devices to alert the NMS of a particular event</td><td>Trap<br>Inform</td></tr><tr><td><strong>Response</strong></td><td>Sent in response to a previous message</td><td>Response</td></tr></tbody></table>

#### Configuration

* Configure contact information - `snmp-server contact` followed by the contact information.
* Configure location information - `snmp-server location` followed by the location.
* Configure a community string - `snmp-server community` followed by the password and `ro` (for read-only) or `rw` (for read-write).
* Configure the NMS address specifying the version and community string - `snmp-server host` followed by the NMS IP address, keyword `version`, version number, and password.
* Configure the trap types to send to the NMS - `snmp-server enable traps` followed by the trap types.

{% file src=".gitbook/assets/Day 40 Flashcards - SNMP.apkg" %}

{% file src=".gitbook/assets/Day 40 Lab - SNMP.pkt" %}

{% embed url="https://youtu.be/v8WxIytUdS4" %}
