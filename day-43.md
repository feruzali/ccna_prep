---
description: FTP & TFTP
---

# Day 43

**FTP** (File Transfer Protocol) and **TFTP** (Trivial File Transfer Protocol) are industry standard protocols used to transfer files over a network. They use a client-server model. For a network engineer, the most common use of FTP/TFTP is in the process of upgrading the operating system of a network device. &#x20;

### TFTP

TFTP is simple and has only basic features compared to FTP. It only allows to copy a file to or from a server. It doesn't provide any authentication, so servers respond to all TFTP requests. It also doesn't provide any encryption, so all data is sent in plain text. It is best used in a controlled environment to transfer small files quickly. TFTP servers listen on UDP port 69.&#x20;

TFTP uses **lock-step** communication. The client and server alternately send a message and then wait for a reply. Every TFTP message is acknowledged. Timers are used, and if an expected message is not received in time, the waiting device resends its previous message.&#x20;

<figure><img src=".gitbook/assets/image (3) (1) (1) (1).png" alt="tftp reliability " width="563"><figcaption></figcaption></figure>

TFTP file transfers have three phases:

1. Connection - The TFTP client sends a request to the server and the server responds back.
2. Data Transfer - The client and server exchange TFTP messages. One sends data and the other sends acknowledgments.
3. Connection Termination - After the last data message has been sent, a final acknowledgement is sent to terminate the connection.

When the client sends the first message to the server, the destination port is UDP 69 and the source is a random ephemeral port. This random port is called a **TID** (Transfer Identifier) and identifies the data transfer. The server then also selects a random TID to use as the source port when it replies, not 69. When the client sends the next message, the destination port is the server's TID, not 69.&#x20;

On Cisco IOS, to copy files using TFTP, use the command copy followed by the source and destination, e.g. `copy tftp: flash:`. Then you will be asked for a TFTP server IP address, filename, etc.

### FTP

FTP uses TCP port 20 and 21. Usernames and passwords are used for authentication but there is no encryption. For greater security, **FTPS** (FTP over SSL/TLS) can be used - upgrade to FTP. **SFTP** (SSH File Transfer Protocol) can also be used for greater security - new protocol. FTP is more complex than TFTP and allows to navigate file directories, add and remove directories, list files, etc. The client sends FTP commands to the server to perform these operations.

An **FTP control** connection (TCP port 21) is established and used to send FTP commands and replies. When files or data are to be transferred, separate **FTP data** connections (TCP port 20) are established and terminated as needed. The default method of establishing FTP data connections is **active mode** - the server initiates the data connection. In FTP **passive mode**, the client initiates the data connection. This is often necessary when the client is behind a firewall which can block the incoming connection.

On Cisco IOS, to copy files using FTP, you have to configure the username and password first. Use the command `ip ftp` followed by `username` and the username - for username, `password` and the password - for password. Then use the `copy` command which is the same as in TFTP.

### IOS File Systems

A file system is a way of controlling how data is stored and retrieved. To view the file system, use the command `show file systems`, for flash - `show flash`. Some examples of file systems:

* `disk` - storage devices like flash memory.
* `opaque` - used for internal functions.
* `nvram` - internal NVRAM. The startup-config file is stored here.
* `network` - represents external file systems like external FTP/TFTP servers.

To upgrade Cisco IOS, enter the global config mode and use the command boot system followed by the file path. Then, save the configuration to the memory and enter `reload`. Finally, to delete the old IOS file, use the command `delete` followed by the file path.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 43 Flashcards - FTP_TFTP.apkg" %}

{% file src=".gitbook/assets/Day 43 Lab - FTP _ TFTP.pkt" %}

{% embed url="https://youtu.be/W9PLvA2wZ28" %}
