---
description: Wireless Architectures
---

# Day 56

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt="802.11 frame"><figcaption></figcaption></figure>

802.11 frames have a different format than 802.3 Ethernet frames. Depending on the 802.11 version and the message type, some of the fields might not be present in the frame.&#x20;

* **Frame Control** - provides information on message type and subtype.
* **Duration/ID** - depending on the message type, can indicate the time (in microseconds) the channel will be dedicated for transmission of the frame or can be an identifier for the connection.
* **Addresses** - up to four addresses can be present in an 802.11 frame. Depending on the message type, different addresses might be present:
  * **DA** (Destination Address) - final recipient of the frame
  * **SA** (Source Address) - original sender of the frame
  * **RA** (Receiver Address) - immediate recipient of the frame
  * **TA** (Transmitter Address) - immediate sender of the frame
* **Sequence Control** - used to reassemble fragments and eliminate duplicate frames.
* **QoS Control** - used in QoS to prioritize certain traffic.
* **HT (High Throughput) Control** - added in 802.11n to enable High Throughput operations. 802.11n is aka High Throughput Wi-Fi and 802.11ac is aka Very High Throughput Wi-Fi.
* FCS (Frame Check Sequence) - same as in an Ethernet frame, used to check for errors.

### Association Process

APs bridge traffic between wireless stations and other devices. For a station to send traffic through the AP, it must be associated with the AP. There are 3 connection states:

1. Not authenticated, not associated: A station sends a probe request and an AP responds with a probe response. There are two ways a station can scan for a BSS: **active scanning** - the station sends probe requests and listens for a probe response from an AP, **passive scanning** - the station listens for **beacon messages** (beacon messages are periodically sent by APs to advertise the BSS).
2. Authenticated, not associated: The station sends an authentication request (ie. password) and the AP responds with an authentication response.
3. Authenticated and associated: The association request and response messages are exchanged.

There are 3 message types:

* **Management** - used to manage the BSS (beacon, probe request, probe response, etc.)
* **Control** - used to control access to the medium. Assists with the delivery of management and data frames (RTS - Request To Send, CTS - Clear To Send, ACK)
* **Data** - used to send actual data packets

### Deployment methods

There are 3 main wireless AP deployment methods:

#### Autonomous APs

**Autonomous AP**s - self-contained systems that don't rely on a WLC. They are configured individually by CLI (telnet/SSH, console cable) or GUI (web browser). An IP address for remote management should be configured. The RF parameters must be manually configured (transmit power, channel, etc.). Security policies are handled individually by each AP. QoS rules are configured individually on each AP. There is no central monitoring or management of APs. Autonomous APs connect to the wired network with a trunk link. Data traffic from wireless clients has a very direct path to the wired network or other wireless clients connected to the same AP. Each VLAN has to stretch across the entire network. They can be used in small networks but not in medium to large networks.

<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt="autonomous APs" width="563"><figcaption></figcaption></figure>

#### Lightweight APs

**Lightweight AP**s - they handle real-time operations like transmitting/receiving RF traffic, encryption/decryption of traffic, sending out beacons/probes, etc. Other functions are carried out by a **WLC** (Wireless LAN Controller), e.g. RF management, security/QoS management, client authentication, client association/roaming management, etc. This is called **split-MAC architecture**. The WLC is also used to centrally configure the lightweight APs and can be located in the same or a different subnet/VLAN. The WLC and the lightweight APs authenticate each other using digital certificates installed on each device (X.509 standard certificates). This ensures that only authorized APs can join the network. They use the **CAPWAP** (Control And Provisioning Of Wireless Access Points) protocol to communicate. Two tunnels are created between each AP and the WLC: **control tunnel** (UDP port 5246) -  used to configure the APs, all traffic is encrypted by default, **data tunnel** (UDP port 5247) - all traffic from wireless clients is sent through this tunnel to the WLC, traffic is not encrypted by default, but **DTLS** (Datagram Transport Layer Security) protocol can be used for encryption. Because all traffic from wireless clients is tunnelled to the WLC with CAPWAP, APs connected to switch access ports, not trunk ports. However, a trunk link is needed between the WLC and the wired network because the data is sent to the WLC via a tunnel and if the destination is outside the LAN, the WLC forwards it to the wired network.

<figure><img src=".gitbook/assets/image (8) (1).png" alt="lightweight APs" width="563"><figcaption></figcaption></figure>

Lightweight APs can be configured to operate in various modes:

* **Local** - the default mode where the AP offers a BSS for clients to associate with.
* **FlexConnect** - the same as the local mode but it allows the AP to locally switch traffic between the wired and wireless networks if the tunnels to the WLC go down.
* **Sniffer** - the AP doesn't offer a BSS for clients. It is dedicated to capturing 802.11 frames and sending them to a device running software like Wireshark.
* **Monitor** - the AP doesn't offer a BSS for clients. It is dedicated to receiving 802.11 frames to detect rogue devices. If a client is found to be a rogue device, an AP can send a de-authentication messages to disconnect the rogue device from the AP.
* **Rogue Detector** - the AP doesn't even use its radio. It listens to traffic on the wired network but it receives a list of suspected rogue clients and AP MAC addresses from the WLC. By listening to ARP messages on the wired network and correlating it with the information it receives from the WLC, it can detect rogue devices.&#x20;
* **SE-Connect** (Spectrum Expert Connect) - the AP doesn't offer BSS for clients. It is dedicated to RF spectrum analysis on all channels. It can send information to software such as Cisco Spectrum Expert on a PC to collect and analyze the data.
* **Bridge/Mesh** - like the autonomous AP's Outdoor Bridge, the lightweight AP can be a dedicated bridge between sites. A mesh can be made between the APs.
* **Flex plus Bridge** - adds FlexConnect functionality to the Bridge/Mesh mode. Allows the APs to localy forward traffic even if connectivity to the WLC is lost.

#### Cloud-Based APs

**Cloud-Based AP** architecture is in between autonomous AP and split-MAC architecture - autonomous APs that are centrally managed in the cloud. Cisco Meraki is a popular cloud-based Wi-Fi solution. The Meraki dashboard can be used to configure APs, monitor the network, generate performance reports, etc. However, data traffic is not sent to the cloud. It is sent directly to the wired network.&#x20;

<figure><img src=".gitbook/assets/image (9).png" alt="Cloud-based APs" width="563"><figcaption></figcaption></figure>

### WLC Deployments

In a split-MAC architecture, there are 4 main WLC delpoyment models:

* **Unified** - the WLC is a hardware appliance in a central location of the network. One WLC can support 6000 APs.
* **Cloud-based** - the WLC is a VM running on a server, typically in a private cloud. One WLC can support 3000 APs.
* **Embedded** - the WLC is embedded within a switch. One WLC can support 200 APs.&#x20;
* **Mobility Express** - the WLC is embedded within an AP. One WLC can support 100 APs.

{% file src=".gitbook/assets/Day 56 Flashcards - Wireless Architectures.apkg" %}
