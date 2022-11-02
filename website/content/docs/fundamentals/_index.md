---

title: "Fundamentals"
weight: 1

---


# Fundamentals

# Hardware Basics

A **router** is a networking device (that may be composed of many virtual network devices) that connects multiple devices, phones, computers, etc, to form a local area network (LAN). Most routers allow devices to connect wirelessly or through Ethernet.

An **access point**, often shortened to just **AP** allows devices to connect wirelessly to a Local Area Network, **LAN** and can also be used to extend the range of coverage to connect to a LAN (you can be physically farther away). The AP then also has a high-speed Ethernet cable runs to a router. (There is also such a thing as WAPs, wireless access points).

A router acts as a hub for a LAN, and an AP is a sub-device in the LAN. Routers can act as APs, but not all APs can act as routers.

A **modem** is a device that connects your LAN to a WAN (Wide Area Network). It is the thing that takes the digital signals that devices send to routers (binary data) and transforms it via modulation into analog data (electricity) that gets transmitted to the WAN. It also receives analog data and demodulates it, so the router can send it to the devices that asked for it.

It is not uncommon to see router/modem combos.

A **switch** is a networking device that connects devices together. Usually physically, via ethernet cables. The word switch usually means a device that forwards data between devices at the layer 2 level using MAC addresses. There is such a thing as layer 3 switches, which incorporate some routing functionality. Routers usually have a kind of switch built-in to them.

# Types of Networks

The internet is a network of networks.

A **Local Area Network (LAN)** is a small private network. For example, all the devices (computers, phones, tablets) in your home connected to your wifi network comprise a LAN.

A **Metropolitan Area Network (MAN)** is the network of a town or city.

A **Wide Area Network (WAN)** is a very large network owned and maintained by multiple stakeholders.

# Layers (OSI Model)

Networking is electricity on wires. And it’s data. But it is also protocols. And it is also packets. And servers. And sometime data is encrypted and sometimes it’s compressed. And different data moves differently. Point is that there’s lots of ways to talk about networking, and there’s lots of lays of abstraction. The same data can be discussed in many ways, and most people use the OSI model as a guide. So when people are saying L2, L4 – it is usually in reference to the OSI model.

OSI model stands for **Open Systems Interconnection model**, but nobody knows that or ever says it out loud.

| # | Name | things that happen |
| --- | --- | --- |
| 7 | Application | What the user interacts with, http, ftp |
| 6 | Presentation | Handler encryption, decryption, compression, decompression. |
| 5 | Session | channels, called sessions, between devices. |
| 4 | Transport | TCP, UDP |
| 3 | Network | Deciding what physical path the packets will take |
| 2 | Data Link | define the format of the data/packets |
| 1 | Physical | the physical bit, electricity on a wire kind of shit |

Although the OSI model gets all the attention, there’s actually other models. TCP/IP, the protocol that runs the internet, actually has it’s own model defined in [RFC 1122](https://datatracker.ietf.org/doc/html/rfc1122)/[RFC 1123](https://datatracker.ietf.org/doc/html/rfc1123). It is a simpler model with only 4 layers.

| # | Name | OSI Layers |
| --- | --- | --- |
| 4 | Application | Application (7) + Presentation (6) + Session (5) |
| 3 | Transport | Transport (4) |
| 2 | Internet | Network (3) |
| 1 | Link | Link (2) |

Personally, this makes more sense to because I don’t know enough about the details of OSI layers 5 through 7 to consider them separate layers.

# IP Addresses, IPv4, IPv6

IP addresses are strings of numbers that correspond to a unique device on *some* network.

IPv4 addresses are made of 32 bits which usually organized into 4 bytes (also sometimes, thought rarely, called octets).

IPv6 addresses are made of 128 bits and usually written in hex.

If you have lots of zeros, you may omit them.

Pairs of equivalent IPv6 addresses:

```
2001:0db8:c9d2:0012:0000:0000:0000:0051
2001:db8:c9d2:12::51

2001:0db8:ab00:0000:0000:0000:0000:0000
2001:db8:ab00::

0000:0000:0000:0000:0000:0000:0000:0001
::1
```

The address `::1` is the *loopback address*. It always means *this machine I’m running on now*.

In IPv4, the loopback address is `127.0.0.1`.

There’s an IPv4-compatibility mode for IPv6 addresses. To represent the IPv4 address `192.0.2.33` as an IPv6 address you write it like this: `::ffff:192.0.2.33`

# Packets, Frames, Etc.

Data is bytes.

To share data through a network, there needs to be a common protocol that everyone agrees on, and data bytes must be in a specific format.

The most used data units in networks are the **packet**, **frame**, and **datagram**.

The word packet is often used as a catchall term for all the previously mention data units as well as others, but when you say packet and you want to refer to a specify type of packet called a packet, you probably mean an internet packet (IP).

Internet Packets are used for connection-oriented protocols.

Data is divided into packets, sent over the internet, then recombined to recreate the original data at its destination.

Packets are data units with the network layer (L3) of OSI.

There are limits to the size of IP packets. It is defined by something called MTU, a Maximum Transmitted Unit. If packets are bigger than the MTU of a network, then they are broken up into smaller pieces of data called fragments. The network layer (L3) is also responsible for fragmentation.

Packets have `DF` flag, “Don’t Fragment.” If the `DF` flag is set to 1, and the size of the packet is bigger than the MTU of the packet, the packet is discarded.

Next there are frames.

The main difference between a packet and a frame is its association with the OSI layers. While a packet is used in the network layer, a frame is a unit of data in the data link layer. Frames are used by Ethernet.

A frame contains more information about the transmitted message than a packet. Like some flags, MAC addresses, etc.

Datagrams are used for connectionless protocols like UDP.

# Sockets

**Sockets are the endpoints of communication.**

Socket is a big word. Like packets, its a bit of a catch-all. However in networking we are usually we are talking about Internet Sockets.

A socket allows programs to communicate to each other by using **Unix file descriptors**, sometimes over a network.

A **file descriptor** is just an integer associated with an open file.

That file can be anything: a network connection, a pipe a terminal, a picture of a cat, whatever. This comes from the Unix philosophy that *everything in Unix is a file*. When Unix systems do any kind of I/O the do so by reading or writing to a file descriptor.

Internet sockets are also called DARPA Internet addresses. But no one says that.

There are also many types of internet sockets, but we are going to talk about two kinds: **Stream Sockets** and **Datagram Sockets**. (Another interesting, and very powerful type of internet socket is a **Raw Socket**).

**Stream sockets** are reliable **two-way** connected internet streams. Things get output the same order they were input. Stream sockets use a protocol called **Transmission Control Protocol, TCP**. TCP makes ensures data arrive sequentially and error-free.

TCP is often heard when saying **TCP/IP**. IP stands for Internet Protocol and primarily deals with internet routing and is not concerned with data integrity.

**Datagram sockets** don’t care about order. They don’t care if they arrive where they are supposed to or not. If it does arrive though, the data in the packet will be error-free. Datagrams also use IP for routing, but they don’t use TCP, they use UDP.

> Wanna hear a joke about UDP? …nevermind you probably wouldn’t get it.
>

A **socket address** is usually a combination of a file descriptor, an IP address and a port number. TCP/IP creates socket addresses that is unique throughout all Internet networks. Those socket addresses are used to read data on one machine and write it on another, and transmit that data via packets.

# WiFi Networks & Security

First of all, WiFi stands for nothing. Annoying.

WPA stands for Wifi Protected Access. WPA, WPA2, and WPA3 are security certification programs developed by the wifi alliance to secure wireless computer networks. Routers use WPA* to communicate wirelessly with devices and then send that data off into the WAN. WPA is broken, we mostly use WPA2 now.

TLS stand for Transport Layer Security. It is the newer version and successor of (the now depreciated) Secure Sockets Layer (SSL). It is used, most commonly, in securing HTTPS. (HTTPS means HTTP over SSL/TLS). We are now at TLS 1.3, released in 2018. TLS 1.2 was released in 2008, TLS 1.1 in 2006, and TLS 1.0 in 1999.

TLS/SSL use certificates to provide privacy/confidentiality, integrity, and authenticity. It runs in the application layer and it composed of two layers itself the TLS record and the TLS handshake protocols.

TLS certificates are a type of digital certificate issued by a CA (Certificate Authority). Digital certificates (aka identity certificates or public key certificates) are digital files used to certify the ownership of a public key. Each TLS certificate consists of a key pair made of a public key and private key. The server shares its TLS/SSL certificate and its public key with the client to establish a secure connection and a unique session key.

TTLS stands for tunnelled TLS.

Tunnelling in networking refers to the encapsulation of packets: wrapping packets inside of other packets. Tunnelling can be used to set up secure connections between networks, enable the usage of unsupported protocols, and sometimes bypass firewalls.

Packets can be split into 2 parts: the header and the payload. The header indicates the packets destination (among other things) and the payload is the actual content. To encapsulate packet A into packet B, the header and payload of packet A become the payload of packet B.

A VPN (virtual private network) is a secure, encrypted connection over a public network. Basically you send data over an insecure network (anyone can connect and listen in) and encapsulate your packets and encrypt their payloads. Spilt tunnelling is when you route some of your data through your VPN and some through some other network.

Secure Shell Tunnel.

The difference between VPN and SSH tunnels is that in VPN tunnelling, the security comes from altering the data that you want to send and sending through an insecure medium. In SSH, you create a private network (via a public network) and then send your data through a secure channel, so your data doesn’t necessarily need to be encrypted. Another difference is that VPN runs in the transport layer, while SSH runs in the application layer.

# Network Performance

Network performance is usually measured in two fundamental ways, bandwidth and latency. Also called throughput and delay.

Bandwidth is # of bits over time.

Latency is how long it takes to transmit each bit of data.

Latency has 3 components:

- the speed of light,
- the time to transmit data (a function of the amount of data and the bandwidth size),
- and queuing of the data as it moves through the network.

```
Latency = Propagation + Transmit + Queue
Propagation = Distance/SpeedOfLight
Transmit = Size/Bandwidth
```

# Types of Links

| full-duplex | bidirectional (at the same time) |
| --- | --- |
| half-duplex | bidirectional (not at the same time) |
| simplex | unidirectional  |: