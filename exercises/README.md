# Current completion state:

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

# 3. Implementing a Control Plane using P4Runtime

TBA