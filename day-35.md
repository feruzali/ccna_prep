---
description: Extended ACLs
---

# Day 35

### Standard ACLs

Unlike numbered ACLs, named ACLs are configured with subcommands in a separate config mode. But in modern IOS, numbered ACLs can be configured in the exact same way as named ACLs. In the running config file, however, the ACL is displayed as it is configured using the traditional method. There are some advantages of configuring ACLs in a separate config mode:

1. Individual entries in the ACL can easily be deleted using the command `no` followed by the entry number. When configured from global config mode, individual entries cannot be deleted, only the whole ACL.
2. The sequence number can be entered manually. This allows inserting new entries in between other entries.
3.  There is a resequencing function. The command is `ip access-list resequence` followed by ACL ID, starting sequence number, and increment.\


    <figure><img src=".gitbook/assets/image (135).png" alt="" width="563"><figcaption></figcaption></figure>

### Extended ACLs

Extended ACLs function almost the same as standard ACLs. They can be numbered or named just like standard ACLs. The ranges for numbered ACLs are 100-199 and 2000-2699. They are more precise than standard ACLs since they can match traffic based on more parameters. To configure numbered extended ACL, the command is `access-list` followed by a number, `permit`/`deny`, protocol, source, destination IP, etc. To configure from a separate config mode, the command is `ip access-list extended` followed by a name or a number. Then individual entries are entered as usual. In extended ACLs, to specify a `/32` source or destination address, the `host` option or wildcard mask should be used. Extended ACLs should be applied as close to the source as possible, to limit how far the packets travel in the network before being denied.

#### Matching the  port numbers

When matching TCP/UDP, source and/or destination port numbers can be specified after the address to match. For example,

* `eq 80` - equal to port 80
* `gt 80` - greater than 80
* `lt 80` - less than 80
* `neq 80` - not 80
* `range 80 100` - from port 80 to port 100

You can also enter the protocol name instead of the port number. There are many more options, e.g.:

* `ack` - match the TCP ACK flag
* `fin` - match the TCP FIN flag
* `syn` - match the TCP SYN flag
* `ttl` - match packets with a specific TTL value
* `dscp` - match packets with a specific DSCP value

{% file src=".gitbook/assets/Day 35 Flashcards - Extended ACLs.apkg" %}

{% file src=".gitbook/assets/Day 35 Lab - Extended ACLs.pkt" %}

{% embed url="https://youtu.be/1cuMzWBrEYs" %}
