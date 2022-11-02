---

title: "Interworking"
weight: 2

---

# Interworking

So far we have been talking about fairly homogenous systems. So what about systems with different types of protocols?

This brings us to “internetworking” different networks together.

An internet is a logical network built out of a collection of physical networks.

To define a internetwork, you need a service model, that is, the host-to-host services you want to provide.

The IP service model can be thought of as having two parts: an addressing scheme, which provides a way to identify all hosts in the internetwork,
and a datagram (connectionless)model of data delivery.

One of the biggest issues in a heterogeneous network is that each network tends to have its own idea of how big a packet should be. So we need to talk about fragmentation and reassembly.

The central idea here is that every network type has a maximum transmission unit (MTU), which is the largest IP datagram that it can carry in a frame.

So fragmentation occurs when the path of a packet goes through a network with a smaller MTU than the one it is currently in.

To enable these fragments to be reassembled at the receiving host, they all carry the same identifier in the `Ident` field.

Ethernet addresses are **flat**, they give no information of the network topology.

In contrast, IP addresses are **hierarchical**, by which we mean that they are made up of several parts that correspond to some sort of hierarchy in the internetwork. Specifically, IP addresses consist of two parts, usually referred to as a **network** part and a **host** part.

1. Class A addresses
2. Class B addresses
3. Class C addresses


The original idea was that the Internet would consist of 

- a small number of wide area networks (these would be class A networks),
- a modest number of campus-sized networks (these would be class B networks),
- and a large number of LANs (these would be class C networks).

**Forwarding** is the process of taking a packet from an input and sending it out on the appropriate output. 

**Routing** is the process of building up the tables that allow the correct output for a packet to be determined.
