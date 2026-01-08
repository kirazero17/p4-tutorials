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

- [x] Basic exercise
- [ ] Food for thought

#### Food for thought
Switch queue depth and rate by default:
- s1:
  - depth: 0
- s2:
  - depth: 0

How does the qdepth header change with different queue depths and rates?
- I could not make the qdepth header change, will return later.

## 6. Source Routing

- [x] Basic exercise
- [ ] Food for thought

#### Food for thought

1. ***Can we change the program to handle both IPv4 forwarding and source routing at the same time?***
   - It is possible, and the source routing should be in higher priority in the logic of this case

2. ***How would you enhance your program to let the first switch add the path, so that source routing would be transparent to end-hosts?***
   - This should be done via table that will put an array of ports into a header key.

## 7. Calculator:

This is not practical enough, will come back later.

## 8. Load Balancing:

- [x] Basic exercise => I managed to make ecmp work by switching from an old Ubuntu 20.04 P4 VM to a 24.04 one. Sometimes, it may route the packet to only one switch for multiple consecutive packets, which makes it seems not to work. But be patient.

## 9. Quality-of-service:

- [x] Basic exercise
- [ ] Get QoS into use => will come back later

#### Self-note on the exercise:

***Food for thought:*** How can we let the user use other protocols?

- Some actions (mostly assured forwarding actions) are defined but unused, they can be assigned later if new upper layer protocols or specific packet criteria are defined.

- Queues and mechanisms to count the turn between different them is needed to show QoS-based priority. Use exercise 5 for queue reference.

## 10. Implementing Multicast

- [x] Basic exercise on the P4 file - The hosts cannot ping h4 (connected to switch port 4) yet
- [x] Add port 4 to the multicast group in file sig-topo/s1-runtime.json - This makes h4 pingable.

#### Food for thought:

- [ ] How would you enhance your program to respond to ARP requests?
   - Answer: (learn fron exercise 1)
- [ ] How would you enhance your program to support MAC learning from the controller?
   - Answer: program a packet type that acquire the IP - MAC mapping from the ARP packets, then put that into a new packet that is sent to the controller. On the controller side, save it in a table and send that table entry back to the switch.

## 11. Firewall
