---

title: "Switches, Links, & Bridges"
weight: 2

---

# Switches, Links, & Bridges

A switch is a specialized computer that 

- allows it to receive and send bits/frames
- that arrive over links.

Links are physically connected to switches at attachment ports or switch ports (usually just called ports). 

Networks built out of such components are usually just called receive and forward networks.

The fundamental idea of packet **switching** is to allow multiple flows of data over a single physical link, AKA multiplexing.

## Circuit Switching

Now telephone networks use something called circuit switching opposed to the internet’s packet switching. 

Circuit switches don’t require the frames to contain any special info on how to forward frames, but in packet switching they do.

There are 2 phases in circuit switching:

1. A setup phase where some state is configured along a path from source to destination
2. And then the transfer phase where the frames are actually sent

Inefficiencies with circuit switching: 

- tends to waste bandwidth if the workload uses a variable bit length

## Packet Switching

In packet switching the frames have a bit of extra information in the which tells the switch how to forward it. This is called the **header**.

This header uniquely identifies the destination of the packet.

There are a few ways that the switch decides what to do. 2 common and one less common.

1. datagram or connectionless approach
2. virtual circuit or connection-oriented approach
3. source routing (less common but has some useful applications)

### Datagram approach

Every packet contains the complete destination address of the packet.

The switch consults a forwarding table, also called a routing table (although there is a distinction between the two) so that it knows what port to send it off to.

Usually also contains receiver address, to make sending packets back easier.

The interesting part is how the routing table is made. this is done in the background using something called a routing protocol.

A host can send a packet anywhere at anytime but has no way of knowing if they have been successfully received.

Each packet is forwarded independently of the other packets that it is related to so they may come out of order (if they take different routes to their destination).

A switch or link failure is not that big of a deal in the grand scheme of things.

### Source Routing

Contains the full route that a packet must take to get to its destination. 

It is a complete sequence of switches or, more helpfully, per-switch network hops to each packet which means that no lookups are necessary. 

It requires the sender to participate in a routing protocol to learn the topology of a network. 

The name derives from the fact that all the information about network topology that is required to switch a packet across the network is provided by the source host.

### Virtual Circuit Routing

Hybrid between datagram routing and source routing.

The VC method is a connection oriented protocol. You can think of it as having two stages.

1. connection setup stage
2. transfer stage

To accomplish the first stage, it is necessary to get the source and the destination hosts to come to a “connection state” via all the switches in the route from one to the other.

This is done via a “VC table” in each of the switches along the way. 

Each entry in a VC table has:

- a virtual circuit identifier, VCI, that uniquely identifies the connection **at this switch**
- an incoming interface on which packets will arrive at this switch
- an outgoing interface on which packets will leave from this switch
- a potentially different VCI for outgoing packets

(but interface we mean a reference to a port)

Now instead of using the destination from the header like in datagram routing, we use the VC table to route the packets.

A VC can be manually set up by a network administrator, then it would have to be manually taken down so this is called a “permanent” VC, a PVC.

Or it can be created dynamically by one of the hosts initiating connection via “signalling”. An SVC.

One of the most common applications of virtual circuits for many years was the construction of virtual private networks (VPNs), but even that application is now mostly supported using Internet-based technologies today.

## LAN switches

There is a class of switches used for forwarding packets between hosts on different Local Area Networks, such as Ethernets. They are usually called **LAN switches** but historically they have also been called **bridges**. 

If you want to connect a pair of ethernets together, you could just put a node between them, with connections to both. (That is why its called a bridge). This device operates in promiscuous mode, accepting all frames transmitted on either of the Ethernets, and forwarding them to the other.

A collection of LANs connected by one or more bridges is called an **extended LAN**.

### Learning Bridges

The idea that a bridge “learns” by building a cache of what stations are down stream of which port.

It builds this cache by looking at the source address of all the packets it receives

Huge problem with loops of course, things can go in circles forever.

The trick is to find a loop free path in the bridge topology.

This is done using a distributed spanning tree algorithm.

This sounds really simple and obvious, BUT, switches do not have the luxury of seeing the entire network topology, so how do they compute the spanning tree? 

It shares information with its neighbours and together they figure out whats what.

## Virtual LANs

Extended LANs do not scale (in practice, it is only practical to use maybe tens of bridges at once) because of broadcasting and the limitations of the distributed spanning tree algorithm (which scales linearly.

We can alternatively use Virtual LANs, VLANs.

VLANs allow a single extended LAN to be partitioned into several seemingly separate LANs. Each virtual LAN is assigned an identifier (sometimes called a color), and packets can only travel from one segment to another if both segments have the same identifier)


