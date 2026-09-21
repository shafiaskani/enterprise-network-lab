# Enterprise Network HQ — Cisco Packet Tracer Lab

## Project Overview

This project is a realistic enterprise network lab built in **Cisco Packet Tracer** to practice and demonstrate hands-on networking skills.

I designed and configured the network myself, including VLANs, trunking, EtherChannel, inter-VLAN routing, DHCP, STP, port security, SSH, static routing, and ACL-based traffic restrictions.

## Network Configuration

### VLANs

* VLAN 10 — Management
* VLAN 20 — Sales
* VLAN 30 — HR
* VLAN 40 — IT
* VLAN 50 — Guest

### Technologies Configured

* VLAN creation and segmentation
* Access ports
* 802.1Q trunking
* Router-on-a-stick inter-VLAN routing
* DHCP pools for multiple VLANs
* LACP EtherChannel
* Spanning Tree Protocol (STP)
* Port Security with sticky MAC addresses
* BPDU Guard and PortFast
* SSH remote management
* Static routing between routers
* Extended ACLs for department-level access control
* Switch management IP and default gateway

## Troubleshooting Experience

After completing the configuration, DHCP was initially not working correctly.

I independently checked the DHCP pools, IP addressing, DHCP bindings, router interfaces, VLAN configuration, EtherChannel status, and trunk configuration to identify the problem.

During troubleshooting, I used **ChatGPT as a troubleshooting assistant** to help interpret command output and narrow down the issue.

The root cause was identified as the connection between **SW1 and R1** not operating as an actual trunk. SW1's `GigabitEthernet0/1` was configured in dynamic auto/access behavior instead of static trunk mode.

I corrected the interface by configuring it as an 802.1Q trunk and allowing the required VLANs:

```cisco
interface gigabitEthernet 0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
 no shutdown
```

I then verified the interface using:

```cisco
show interfaces gigabitEthernet 0/1 switchport
```

This troubleshooting process helped me understand how to trace a DHCP failure through the complete path:

**PC → Access Port → VLAN → EtherChannel → SW1 → Trunk → R1 → DHCP Pool**

## Key Learning

This lab was not only about configuring devices, but also about troubleshooting when the expected result did not occur.

I learned to verify each layer of the network instead of assuming that a configuration was working simply because the commands were accepted.

The troubleshooting process strengthened my understanding of:

* VLAN propagation
* Trunk operation
* DHCP discovery
* Router-on-a-stick
* EtherChannel
* Interface verification
* Reading Cisco IOS command output
* Systematic network troubleshooting

## Tools

* Cisco Packet Tracer
* Cisco IOS CLI
* ChatGPT — used as a troubleshooting assistant during debugging

## My Contribution

**Network design and configuration:** Completed independently.

**Troubleshooting:** Configuration and investigation were performed by me, with ChatGPT used as an assistant to interpret outputs and identify possible causes.
