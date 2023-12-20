---
description: Wireless Security
---

# Day 57

It is essential to encrypt traffic between the wireless clients and the AP in wireless networks.&#x20;

### Authentication

All clients must be authenticated before they can associate with an AP. In corporate settings, a separate SSID with no access to the corporate network can be provided for guest users. Authentication methods:

* **Open Authentication** - the client sends an authentication request and the AP accepts it. After the client is authenticated and associated with the AP, it's possible to require the user to authenticate via other methods before access to the network is granted.
* **WEP** (Wired Equivalent Privacy) - provides both authentication and encryption (RC4 algorithm) of wireless traffic. WEP is a shared-key protocol, requiring the sender and receiver to have the same key. WEP keys can be 40 bits or 104 bits in length. The above keys are combined with a 24-bit **IV** (Initialization Vector) to bring the total length to 64 or 128 bits. WEP encryption is **not secure**.
*   **EAP** (Extensible Authentication Protocol) - authentication framework. It defines a standard set of authentication functions that are used by the various EAP methods. EAP is integrated with 802.1X which provides port-based network access control. 802.1X is used to limit network access for clients connected to a LAN or WLAN until they authenticate. There are three main entities in 802.1X: **supplicant** - the device that wants to connect to the network, **authenticator** - the device that provides access to the network, **AS** (Authentication Server) - the device that receives client credentials and permits/denies access.\


    <figure><img src=".gitbook/assets/image (8).png" alt="EAP auth demo" width="563"><figcaption></figcaption></figure>
*   **LEAP** (Lightweight EAP) - developed by Cisco as an improvement over WAP. Clients must provide a username and password to authenticate. In addition, mutual authentication is provided by both the client and server sending a challenge phrase to each other. Dynamic WEP keys (frequently changing WEP keys) are used. LEAP is considered vulnerable.\


    <figure><img src=".gitbook/assets/image (1) (1).png" alt="LEAP auth demo" width="563"><figcaption></figcaption></figure>
*   **EAP-FAST** (EAP Flexible Authentication via Secure Tunneling) - developed by Cisco. Consists of 3 phases:

    1. **PAC** (Protected Access Credential) is generated and passed from the server to the client.
    2. A secure TLS tunnel is established between the client and the authentication server.
    3. Inside the secure TLS tunnel, the client and server communicate further to authenticate the client.

    <figure><img src=".gitbook/assets/image (2) (1).png" alt="EAP-FAST auth demo" width="563"><figcaption></figcaption></figure>
*   **PEAP** (Protected EAP) - also establishes a secure TLS tunnel but instead of PAC, the server has a digital certificate. The certificate is used to authenticate the server and establish a TLS tunnel. The client must be authenticated within the secure tunnel, ie using MS-CHAP (Microsoft Challenge-Handshake Authentication Protocol).\


    <figure><img src=".gitbook/assets/image (3) (1).png" alt="PEAP auth demo" width="563"><figcaption></figcaption></figure>
*   **EAP-TLS** - the most secure method. It requires a certificate on the AS and every single client. There is no need to authenticate the client within the TLS tunnel but it is still used to exchange encryption key information.\


    <figure><img src=".gitbook/assets/image (4) (1).png" alt="EAP-TLS auth demo" width="563"><figcaption></figcaption></figure>

### Encryption and Integrity

All devices on the WLAN use the same protocol but each client uses a unique encryption/decryption key so other devices can't read its traffic. A **group key** is used by the AP to encrypt traffic that it wants to send to all of its clients. All clients in the network keep this group key.

**MIC** (Message Integrity Check) is added to messages to identify whether the integrity was compromised.

Encryption and Integrity methods:

* **TKIP** (Temporal Key Integrity Protocol) - based on WEP with some security features added. MIC is added to protect the integrity and includes the sender's MAC address and timestamp. A **key mixing algorithm** is used to create a unique WEP key for every frame. The initialization vector is doubled from 24 to 48 bits. A TKIP sequence number is used to keep track of frames sent from each source MAC address. TKIP is used in WPA.
* **CCMP** (Counter/CBC-MAC Protocol) - more secure than TKAP, used in WAP2. The device's hardware must support CCMP to use it. CCMP consists of **AES** (Advanced Encryption Standard) counter-mode encryption and **CBC-MAC** (Cipher Block Chaining Message Authentication Code) which is used as a MIC to ensure the integrity.
* **GCMP** (Galois/Counter Mode Protocol) - more secure and efficient than CCMP, used in WAP3. It allows for higher data throughput. It consists of AES counter-mode encryption and **GMAC** (Galois Message Authentication Code) which is used as a MIC.

### WPA

The Wi-Fi Alliance has developed three **WPA** (Wi-Fi Protected Access) certifications:

1. WEP:
   * TKIP (based on WEP) provides encryption/MIC
   * 802.1X authentication (enterprise mode) or PSK (personal mode)
2. WPA2:
   * CCMP provides encryption/MIC
   * 802.1X authentication (enterprise mode) or PSK (personal mode)
3. WPA3:
   * GCMP provides encryption/MIC
   * 802.1X authentication (enterprise mode) or PSK (personal mode)
   * **PMF** (Protected Management Frames) protecting 802.11 management frames from eavesdropping/forging
   * **SAE** (Simultaneous Authentication of Equals) protects the four-way handshake when using personal mode authentication
   * **Forward secrecy** prevents data from being decrypted sometime later after it has been transmitted over the air

All of the above support two authentication modes:

* **Personal mode**: A **PSK** (Pre-Shared Key) is used for authentication. When you are connecting to your home Wi-Fi and enter the password, that is personal mode. A four-way handshake is used for authentication and the PSK is used to generate encryption keys.
* **Enterprise mode**: 802.1X is used with an authentication server (ie RADIUS server). All authentication methods are supported.

{% file src=".gitbook/assets/Day 57 Flashcards - Wireless Security.apkg" %}
