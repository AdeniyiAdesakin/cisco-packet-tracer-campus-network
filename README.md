# Cisco Packet Tracer Multi-Site Campus Network

**VLANs | Inter-VLAN Routing | DHCP | ACLs | Port Security | Static Routing | RIPv2 | Layer 3 Switching | EIGRP**

## Project Overview

This capstone follows the development of a Cisco Packet Tracer network from a small VLAN-segmented campus into a secured, multi-site environment connecting the main campus, Edmonton, and Ottawa.

The work was completed in three stages. I first built the campus switching and addressing foundation, then applied access-layer security controls, and finally added branch routing before redesigning the network with multilayer switches. Each stage includes the original Cisco IOS commands, configuration evidence, connectivity tests, and troubleshooting notes.



## Business Scenario

The organization requires separate networks for Administration, Academics, Students, Guests, and Servers at its main campus. It also needs routed connectivity to Edmonton and Ottawa, centralized IP address assignment, controlled access to server resources, and protection against unauthorized devices connecting to switch ports.

The network was designed to meet those needs while demonstrating how an environment can progress from basic Layer 2 segmentation to dynamic routing across multiple sites.



## Project Architecture

| Stage | Focus | Main Technologies | Detailed Walkthrough |
|---|---|---|---|
| 1 | Campus switching and network services | VLANs, 802.1Q trunking, router-on-a-stick, DHCP, wireless, printers | [VLAN Segmentation and Inter-VLAN Routing](https://github.com/AdeniyiAdesakin/01-vlan-routing) |
| 2 | Access-layer security | Extended ACLs, port security, unused-port shutdown | [Network Security with ACLs and Port Security](https://github.com/AdeniyiAdesakin/02-network-security) |
| 3 | Branch connectivity and Layer 3 redesign | Static routing, DHCP relay, RIPv2, SVIs, routed ports, EIGRP | [Multi-Site Routing and Layer 3 Switching](https://github.com/AdeniyiAdesakin/03-multisite-routing) |



## Network at a Glance

```text
Main Campus
├── VLAN 10  Administration   192.168.10.0/24
├── VLAN 20  Academics        192.168.20.0/24
├── VLAN 30  Students         192.168.30.0/24
├── VLAN 50  Guest            192.168.50.0/24
└── VLAN 100 Server Room      192.168.100.0/24
    │
    ├── 172.16.10.0/30 ── Edmonton ── 192.168.60.0/24
    └── 172.16.11.0/30 ── Ottawa   ── 192.168.70.0/24
```

### Addressing Plan

| Network | Subnet | Default Gateway |
|---|---|---|
| Administration, VLAN 10 | `192.168.10.0/24` | `192.168.10.1` |
| Academics, VLAN 20 | `192.168.20.0/24` | `192.168.20.1` |
| Students, VLAN 30 | `192.168.30.0/24` | `192.168.30.1` |
| Guest, VLAN 50 | `192.168.50.0/24` | `192.168.50.1` |
| Server Room, VLAN 100 | `192.168.100.0/24` | `192.168.100.1` |
| Edmonton LAN | `192.168.60.0/24` | `192.168.60.1` |
| Ottawa LAN | `192.168.70.0/24` | `192.168.70.1` |
| Main Campus to Edmonton | `172.16.10.0/30` | `.1` main campus, `.2` Edmonton |
| Main Campus to Ottawa | `172.16.11.0/30` | `.1` main campus, `.2` Ottawa |

## Lab Environment

| Component | Role |
|---|---|
| Cisco Packet Tracer | Network design, configuration, and simulation |
| Cisco 2960 switches | Initial core and access-layer switching |
| Cisco router | Router-on-a-stick, DHCP, ACL enforcement, and campus routing |
| Cisco 2811 routers | Edmonton and Ottawa branch routing |
| HWIC-2T modules | Serial point-to-point WAN connections |
| Cisco 3560 multilayer switches | Final Layer 3 campus and branch design |
| PCs and servers | Addressing, routing, DHCP, and ACL testing |
| Wireless router, laptop, and tablet | Wireless connectivity testing |
| Network printers | Departmental endpoint deployment |

## What I Implemented

- Created departmental VLANs and assigned access ports.
- Configured an 802.1Q trunk and router-on-a-stick inter-VLAN routing.
- Deployed Cisco IOS DHCP pools with default-gateway and DNS options.
- Added wireless clients, printers, servers, and additional access switches.
- Applied extended ACLs to restrict traffic between user and server networks.
- Configured static switch port security and tested shutdown-mode behavior.
- Disabled unused switch interfaces to reduce unnecessary exposure.
- Connected Edmonton and Ottawa using point-to-point routed links.
- Tested static routing, centralized DHCP relay, and RIPv2.
- Replaced the router-based design with multilayer switches, SVIs, and routed ports.
- Configured EIGRP autonomous system 100 and tested branch-to-branch reachability.
- Documented configuration errors, corrections, and incomplete validation honestly.

## Selected Project Evidence

### Campus Segmentation

The first design separated campus users and servers into departmental VLANs.

<p align="center">
  <img src="https://i.imgur.com/XIG4Yb0.png" width="800" alt="Initial VLAN-segmented campus topology">
</p>

The switch trunk carried VLANs 10, 20, 30, and 100 to the router.

<p align="center">
  <img src="https://i.imgur.com/j592VbL.png" width="800" alt="Verified 802.1Q trunk on the core switch">
</p>

After the router subinterfaces and endpoint gateways were configured, inter-VLAN communication succeeded.

<p align="center">
  <img src="https://i.imgur.com/COEIiAC.png" width="800" alt="Successful inter-VLAN connectivity test">
</p>

### DHCP and Endpoint Expansion

DHCP bindings and pool utilization confirmed that campus clients were receiving dynamic addresses.

<p align="center">
  <img src="https://i.imgur.com/oHPL4Kl.png" width="800" alt="Cisco IOS DHCP pool validation">
</p>

The campus was expanded with wireless clients, printers, servers, and dedicated access switches.

<p align="center">
  <img src="https://i.imgur.com/5DqxjUw.png" width="800" alt="Expanded campus topology">
</p>

### Security Controls

ACL 100 restricted the Student VLAN from reaching the Server VLAN while permitting approved departmental networks.

<p align="center">
  <img src="https://i.imgur.com/p6BwuzR.png" width="800" alt="Extended ACL protecting the Server VLAN">
</p>

Static port security was applied to server-facing switch interfaces and verified in secure-up status.

<p align="center">
  <img src="https://i.imgur.com/NOFM80U.png" width="800" alt="Verified switch port-security status">
</p>

### Multi-Site Expansion

The campus was connected to Edmonton and Ottawa through separate point-to-point links.

<p align="center">
  <img src="https://i.imgur.com/iPR9Ko6.png" width="800" alt="Main campus connected to Edmonton and Ottawa">
</p>

Branch-to-branch communication succeeded during the dynamic-routing stage.

<p align="center">
  <img src="https://i.imgur.com/0RoZyQk.png" width="800" alt="Successful Edmonton-to-Ottawa connectivity test">
</p>

### Layer 3 Redesign

The final design replaced the router-based campus core with Cisco 3560 multilayer switches and routed point-to-point links.

<p align="center">
  <img src="https://i.imgur.com/OO4iQQ0.png" width="800" alt="Layer 3 switch design connecting the main campus and branches">
</p>

End-to-end pings succeeded in both directions between Edmonton and Ottawa. The available evidence confirms reachability, although additional routing-table and neighbor outputs would be needed to prove the final EIGRP state conclusively.

<p align="center">
  <img src="https://i.imgur.com/asTOEFO.png" width="800" alt="Successful Edmonton-to-Ottawa ping in the Layer 3 design">
</p>




## Repository Structure

```text
cisco-packet-tracer-campus-network/
├── README.md
├── 01-vlan-routing/
│   └── README.md
├── 02-network-security/
│   └── README.md
├── 03-multisite-routing/
│   └── README.md
└── images/
    ├── vlan-routing/
    ├── security/
    └── multisite-routing/
```

## Detailed Walkthroughs

### 1. [VLAN Segmentation and Inter-VLAN Routing](https://github.com/AdeniyiAdesakin/01-vlan-routing)

Campus VLANs, access-port assignments, router-on-a-stick, DHCP, wireless connectivity, and printer deployment.

### 2. [Network Security with ACLs and Port Security](https://github.com/AdeniyiAdesakin/02-network-security)

Dedicated access switches, extended ACLs, traffic validation, static port security, violation recovery, and unused-port shutdown.

### 3. [Multi-Site Routing and Layer 3 Switching](https://github.com/AdeniyiAdesakin/03-multisite-routing)

Edmonton and Ottawa branches, static routing, DHCP relay, RIPv2, multilayer switching, routed ports, and EIGRP.

## Recommended Production Improvements

- Use a dedicated management VLAN and restrict administration with SSH, AAA, and management ACLs.
- Use named ACLs with remarks describing the business purpose of each rule.
- Place unused access ports in an unused VLAN before shutting them down.
- Enable PortFast and BPDU Guard on eligible access ports.
- Add DHCP snooping, Dynamic ARP Inspection, and IP Source Guard where supported.
- Separate staff and guest wireless traffic with dedicated SSIDs and VLANs.
- Add redundant links, gateways, DHCP services, and distribution devices.
- Back up configurations and maintain a tested rollback plan.
- Validate routing with neighbor tables, protocol status, and route tables in addition to ping.

## Project Outcome

This project gave me practical experience building, securing, expanding, and troubleshooting a Cisco network across several stages. I configured the switching and routing foundation, introduced access controls, connected remote branches, and evaluated the migration to a Layer 3 design.

The strongest results were verified VLAN isolation, successful inter-VLAN and inter-branch communication, working ACL restrictions, DHCP address allocation, and switch-port hardening. The project also reinforced an important operational lesson: a successful ping confirms reachability, but complete validation requires interface state, protocol neighbors, routing tables, and final configuration evidence.














