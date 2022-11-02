---

title: "Transmission"
weight: 1

---

# Transmission

# Encoding

First of all,  the physical layer transmits signals, not bits. So we need to translate back and forth. This is done via modulation and demodulation.

## Clock recovery
   
Clock recovery means being able to recover and deduce the senders clock, since the sender sends information triggered by clock cycles. 

Intuitively, clock recovery is easier by sending frequent `0-1` and `1-0` transmissions.

## Scheme 1 - NRZ

The simplest scheme.

Bit `1` may be sent as a high voltage signal and bit `0` as a low one.

NRZ = Non-Return to Zero.

Main issue is that consecutive identical voltages are hard to distinguish by the receiver. For example, cannot distinguish a zero from no signal and too many consecutive ones cause the baseline signal to deviate from the true average.

## Scheme 1 - NRZI

NRZI = Non-Return to Zero Inverted. 

Here the sender stays the same to signal a zero and changes to signal a 1. Does not solve the consecutive zeros problem, but does solve the consecutive 1s problem.

## Manchester Encoding

The sender transitions from low to high in order to encode a `0`, and a high to low transition to encode a `1`. Ensures transmission on every bit so clock recovery is easy. The problem is that it is somewhat inefficient because it requires that more bits be transmitted than those in the original signal.    

## 4B/5B

Solves the inefficiency of Manchester encoding by converting every sequence of 4 bits to 5, and encodes the four bits in NRZI. This way no consecutive sequence of 3 or more zeros to ever appear.


# Framing

Assuming that we solved encoding, now we are concerned with sending really big files across.

One way is just a bit or byte stream and continually send bits/bytes across. 

Another approach would be to “packetize” or make frames of smaller sizes and ship them across. This is *framing*.

Examples of framing protocols: 

- PPP, point-to-point protocol. byte oriented.
- And HDLC, high-level data link control. bit oriented.
- SONET, clock-based framing.

The idea is that the sender demarcates the sequence of bits with a BEGIN marker, (`01111110` in the case of HLDC) and the bits in between correspond to a frame.

The link layer sends the frame via one of the modulation methods, and then at the receiver, the link layer delivers them to the app that request it.

Each protocol has a 

- peer interface
- and a service interface.

Service interface is how objects on the same computer interact with it.

A peer interface is how to talk to other machines


# Error Detection

## Parity

A parity bit, or check bit, is a bit added to a string of binary code.

Accordingly, there are two variants of parity bits: **even parity** and **odd parity**. 

Even parity → for a given set of bits, the bits whose value is 1 are counted. 

If that count is odd, the parity bit value is set to 1, making the total count of occurrences of 1s in the whole set (including the parity bit) an even number.

If even, set to 0.

2D Parity does this for 6 bytes, then has a parity byte.

where the `ith` bit is the parity of the `ith` column created by the `ith` elements in each previous byte.

## Check Sums

Add up all the words that are transmitted and then transmit that sum.

## CRC - cyclic redundancy check

ah… later

# Reliable Transmission (error correction)

## Stop and Wait

ARQ (Automatic Repeat reQuest).

Sender sends a packet (or frame) and waits to receive and ACK before it sends the next packet. Aka the Stop-and-Wait scheme.

Main draw back is that it only allows for one outstanding packet in each roundtrip time RTT. So it doesn’t “fill the pipe” between send and receiver. 

## Sliding Window

Assuming bandwidth *B* and RTT *d*, supposed the quantity if bits we can fit into the “pipe” is *P*.

If the pipe is full then B is fully utilized.

If no data is lost, then at best throughput is *P/d* for the receiver.  

Pipe size / the round trip time. 

So to utilize bandwidth the right pipe size is, *B x d.*

This is often called the bandwidth delay product of the network between sender and receiver. 

Ideally the sender want B x d bytes in the pipe before checking what’s been received.

(unless the size of the packet is too big for that)

So we can do this with a window based protocol. 

Sending a windows worth of packets and waiting for an ACK for all of them will also sometimes under utilize the pipe, so we actually use sliding window protocols. 

Which means ACK as set as packets are received. Every time an ACK is received, the window slides and is sent again. So data will be sent multiple times, but this is actually the most efficient thing to do because the pipe is always full.

**Exponential Backoff** - if collision is detected, waits and tries again. If collides again, doubles wait time and tries again, over and over again.

