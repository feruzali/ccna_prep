---
description: Standard ACLs
---

# Day 34

### ACLs

**ACL**s (Access Control Lists) have multiple uses but the primary one is security. ACLs function as a packet filter instructing the router to permit or discard the specific traffic based on source/destination IP, source/destination Layer 4 ports, etc. ACLs are configured globally on the router but after that, they have to be applied to an interface. ACLs are applied either inbound or outbound. ACL consists of an ordered sequence of **ACE**s (Access Control Entries). The order of these entries is very important. When a router checks a packet against ACL, it processes the ACEs in order from top to bottom. If the packet matches one of the ACEs, the router takes an action and stops processing the ACL. All entries below the matching entry are ignored. A maximum of one ACL per direction can be applied to an interface.&#x20;

If a packet doesn't match any entries, it is denied. There is an **implicit deny** (`if source IP = any, then deny`) at the end of all ACLs which tells the router to deny all traffic that doesn't match any of the ACEs.

#### Types

There are two types of ACLs:

1. Standard ACLs - match based on source IP only. Can use the number ranges 1-99 and 1300-1999. Standard ACLs should be applied as close to the destination as possible.
   * Standard Numbered ACLs
   * Standard Named ACLs
2. Extended ACLs - match based on source/destination IP, source/destination port, etc.
   * Extended Numbered ACLs
   * Extended Named ACLs

#### Configuration

The basic command to configure a standard numbered ACL entered from the global config mode is `access-list` followed by the number followed by `deny`/`permit` and IP address with a wildcard mask, e.g. `access-list 1 deny 1.1.1.1 0.0.0.255`. To add a description use the command `access-list` with the number followed by `remark` and description. To apply the ACL on an interface, use the command `ip access-group` followed by the number and `in`/`out`.

Named ACLs are configured by entering the standard named ACL config mode. To do so, the command is `ip access-list standard` followed by a name. Then each entry is entered one by one. There is an optional field you can use at the beginning of each entry to control the order of the entries. So the command begins with an optional entry number followed by `deny`/`permit` and IP address with a wildcard mask. Named ACLs are applied on an interface in the same way as numbered ACLs. A router may re-order the `/32` entries to improve the efficiency of processing the ACL but it doesn't change the effect of the ACL.

{% file src=".gitbook/assets/Day 34 Flashcards - Standard ACLs.apkg" %}

{% file src=".gitbook/assets/Day 34 Lab - Standard ACLs.pkt" %}

{% embed url="https://youtu.be/sJ8PXmiAkvs" %}
