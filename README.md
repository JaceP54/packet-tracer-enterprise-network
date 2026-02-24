# packet-tracer-enterprise-network
Multi-VLAN enterprise network in Cisco Packet Tracer implementing router-on-a-stick inter-VLAN routing, per-VLAN DHCP, extended ACL segmentation (guest isolation and server protection), WAN /30 connectivity, and NAT overload (PAT).

Enterprise Network (Cisco Packet Tracer)
Overview

This project simulates a small enterprise network designed with proper segmentation, security controls, and WAN connectivity.

The environment implements VLAN-based network segmentation, router-on-a-stick inter-VLAN routing, DHCP services per subnet, extended ACL-based security policies, and NAT overload (PAT) to a simulated ISP.

The goal of this lab was to design and validate a realistic small-business network architecture while enforcing traffic control and security policies.

Topology Summary

1 Core Router (R1)

1 Access Switch (S1)

1 Simulated ISP Router

5 VLANs (IT, Sales, HR, Guest, Server)

WAN /30 link to ISP

NAT overload for internet access

VLAN & IP Addressing Design
VLAN	Department	Subnet	Default Gateway
10	IT	192.168.10.0/24	192.168.10.1
20	Sales	192.168.20.0/24	192.168.20.1
30	HR	192.168.30.0/24	192.168.30.1
40	Guest	192.168.40.0/24	192.168.40.1
50	Server	192.168.50.0/24	192.168.50.1

WAN Link:

200.1.1.0/30

R1: 200.1.1.1

ISP: 200.1.1.2

Simulated Internet Host:

8.8.8.8 (ISP Loopback)

Core Technologies Implemented
Layer 2

VLAN creation and segmentation

Access port assignments

802.1Q trunking between switch and router

MAC address table verification

Layer 3

Router-on-a-stick inter-VLAN routing

Subinterfaces with dot1Q encapsulation

Default static route toward ISP

DHCP Services

Dedicated DHCP pool per VLAN

Excluded address ranges

Verified lease bindings

Security (Extended ACLs)

Guest VLAN (40) Policy:

Denied access to all internal 192.168.0.0/16 networks

Permitted internet-only access

Server VLAN (50) Policy:

Accessible only from IT VLAN (10)

Blocked from Sales, HR, and Guest VLANs

ACL behavior validated using hit counters.

WAN & NAT

/30 point-to-point WAN link

NAT overload (PAT) translating internal networks to 200.1.1.1

Verified NAT translations with active session entries

Traffic Flow Validation

The following scenarios were tested and verified:

IT VLAN → Server VLAN (Allowed)

Sales/HR/Guest → Server VLAN (Blocked)

Guest VLAN → Internal VLANs (Blocked)

Guest VLAN → 8.8.8.8 (Allowed)

All internal VLANs → Internet (Allowed via NAT)

NAT translations confirmed with show ip nat translations

ACL hit counters verified with show access-lists
