# Current completion state:
---

## 1. Basic:

- [x] The original exercise is completed.
- [ ] ARP is in the progress of implementation, without success - will come back after looking at the p4 L2 switch exercise.
- [ ] Traceroute is not not yet implemented - will come back after finishing the traceroute example of p4-learing.
- [ ] Next hop is not not yet implemented

**Is this program enough to replace a router? What's missing?**

- It cannot replace a full-function router yet. The router does not send ARP requests to find the target MAC address for packets that egresses from it, which means it must be manually configured the MAC address.

## 2. Basic Tunneling:

- [x] The original exercise is completed.
- [x] Add the myTunnel header to an IP packet upon ingress to the network => ***Done in a rough state, will revisit later***
- [x] Remove the myTunnel header as the packet leaves to the network to an end host => ***Done in a rough state, will revisit later***

## 3. Implementing a Control Plane using P4Runtime

- [x] Basic: Implement a transit rule
- [x] Extra 1: use the P4Info helper to translate entity IDs in `mycontroller.py` into entry names. -> Ưill have a closer look at p4info_helper later

#### Questions:
1. What assumptions about the topology are baked into your implementation? How would you need to change it for a more realistic network?
    - The topology does not consider hosts that are attached to the same switch/router.

2. Why are the byte counters different between the ingress and egress counters?
   - The total difference of 24 bytes (192 bits) is due to each packet (of the 6) has a 4-byte (32-bit) Tunnel header attached.

3. What is the TTL in the ICMP replies? Why is it the value that it is? Hint: The default TTL is 64 for packets sent by the hosts.
   - The switch did not decrease the TTL after the tunneled packet passes through it, which may cause the packet to travel indefinitely if it cannot find the destination.
  
## 4. Implementing Explicit Congestion Notification (ECN)

- [x] Basic exercise

#### Food for thought

It might be possible to allow user to define the ecn threshold using table and a wrapper around P4Runtime/P4CLI

## 5. Implementing Multi-Hop Route Inspection (MRI)

