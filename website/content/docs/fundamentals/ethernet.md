---

title: Ethernet
weight: 3

---


# Ethernet and Shared Media Access

And then when there are more than two computers trying to communicate over a medium (”link”), we have to deal with *sharing*.  

This is the *media access* or *channel access* problem.

Protocols to solve this are called MAC (media access control) protocols. 

There are centralized and decentralized MAC protocols.

# Aloha

The Ethernet has its roots in an early packet radio network, called **Aloha**, developed at the University of Hawaii to support computer communication across the Hawaiian Islands.

# Unicast, Broadcast, Multicast

Each frame transmitted on an Ethernet is received by every adaptor connected to that Ethernet. 

Each adaptor recognizes those frames addressed to its address and passes only those frames on to the host. Unicast is one-to-one is a transmission.

A adaptor can also be programmed to run in promiscuous mode, in which case it delivers all received frames to the host, but this is not the normal mode.)

In addition to these unicast addresses, an Ethernet address consisting of all 1s is treated as a broadcast address; all adaptors pass frames addressed to the broadcast address up to the host.

An address that has the first bit set to 1 but is not the broadcast address is called a multicast address. Multicast addresses are used to send messages to some subset of the hosts on an Ethernet (e.g., all file servers).

