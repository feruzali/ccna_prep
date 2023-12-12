---
description: SSH
---

# Day 42

By default, no password is required to access the Cisco IOS CLI via the console port. To configure a password on the console line:&#x20;

1. Enter the line config mode - `line console 0`. The number is always 0.
2. Configure the password - `password` followed by the password.
3. Make the device require a user to enter the password before accessing the CLI - `login`.

You can also configure the device to require users to log in using one of the configured usernames on the device:

1. Specify the username and password - from the global config mode, enter the command `username` followed by the username, `secret` followed by the password.
2. Enable authorization on the console line - `login local`.&#x20;
3. Configure the inactivity timer - from the line config mode, enter the command `exec-timeout` followed by the number of minutes and seconds.

Layer 2 switches don't perform packet routing. However, you can assign an IP address to an SVI to allow remote connections to the CLI:&#x20;

1. Configure the IP address on the SVI in the same way as on a multilayer switch and enable the interface.
2. Specify the default gateway - from the global config mode, enter the command `ip default-gateway` followed by the IP address.&#x20;

### Telnet

**Telnet** (Teletype Network) is a protocol used to remotely access the CLI of a remote host. It is largely replaced by SHH which is more secure. Telnet sends data in plain text without any encryption. The Telnet server listens on TCP port 23. To configure Telnet on a device:

1. Enable password/secret - `enable` `password`/`secret` followed by the password. If not enabled, you won't be able to access privileged exec mode.
2. Configure the username and password on the device.
3. You can also configure an ACL to limit which devices can connect to the VTY lines.
4. Enter the VTY lines config mode - `line vty` followed by the number of lines. There are 16 lines available, so up to 16 users can be connected at once. To configure all at once - `line vty 0 15`.
5. Enable authorization - `login local`.
6. Configure the inactivity timer - `exec-timeout` followed by the number of minutes and seconds.
7. Enable Telnet - `transport input` followed by one of the options.
8. Apply the configured ACL to the VTY lines - `access-class` followed by the ACL number and direction.

### SSH

**SSH** (Secure Shell) was developed to replace less secure protocols like Telnet. There are 2 versions of SSH: SSHv1 and SSHv2. If a device supports both versions, it is said to run **version 1.99**. SSH provides some security features like data encryption and authentication. The SSH server listens on TCP port 22. To check whether the device supports SSH, enter the command `show version`. IOS images that support SSH have `K9` in their name.

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt="show version demo" width="563"><figcaption></figcaption></figure>

Cisco exports **NPE** (No Payload Encryption) IOS images to countries that have restrictions on encryption technologies. NPE IOS images do not support cryptographic features like SSH.

To view information about the current SSH configuration, enter the command `show ip ssh`.&#x20;

To enable and use SSH, RSA public and private key pair must be generated first. The keys are used for data encryption/decryption, authentication, etc. The **FQDN** (Fully Qualified Domain Name) of the device is used to name the RSA keys. to configure the domain name, use the command `ip domain name` followed by the domain name. Then, to generate the keys, use the command `crypto key generate rsa` followed by the length. The length must be 768 bits or greater for SSHv2. SSH is configured the same as Telnet. To choose the version of SSH, from the global config mode enter the command `ip ssh version` followed by the version number.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt="summary" width="563"><figcaption><p>Summary</p></figcaption></figure>

{% file src=".gitbook/assets/Day 42 Flashcards - SSH.apkg" %}

{% file src=".gitbook/assets/Day 42 Lab - SSH.pkt" %}

{% embed url="https://youtu.be/QnHq7iCOtTc" %}
