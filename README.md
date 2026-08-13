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
| 1 | Campus switching and network services | VLANs, 802.1Q trunking, router-on-a-stick, DHCP, wireless, printers | [VLAN Segmentation and Inter-VLAN Routing](01-vlan-routing/README.md) |
| 2 | Access-layer security | Extended ACLs, port security, unused-port shutdown | [Network Security with ACLs and Port Security](02-network-security/README.md) |
| 3 | Branch connectivity and Layer 3 redesign | Static routing, DHCP relay, RIPv2, SVIs, routed ports, EIGRP | [Multi-Site Routing and Layer 3 Switching](03-multisite-routing/README.md) |



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

## Validation Summary

| Area | Status | Evidence |
|---|---|---|
| VLAN creation and port assignment | Passed | VLAN configuration and access-port membership captured |
| Pre-routing VLAN isolation | Passed | Same-VLAN ping passed and cross-VLAN ping failed |
| 802.1Q trunking | Passed | Trunk interface shown operational |
| Router-on-a-stick | Passed | Four subinterfaces shown up/up |
| Inter-VLAN routing | Passed | Cross-VLAN pings completed successfully |
| Campus DHCP | Passed | Pools, bindings, and leased addresses displayed |
| Wireless association | Passed | Laptop and tablet joined the configured SSID |
| ACL 100 and ACL 110 | Passed | Permitted and denied traffic matched the intended tests |
| Switch port security | Configured and observed | Secure status and link shutdown behavior captured |
| Unused-port shutdown | Passed | Selected interfaces shown administratively down |
| Static routing | Passed for tested paths | Main-campus and Edmonton connectivity succeeded |
| Router-based DHCP relay | Configured | Helper targets captured; branch leases not shown |
| RIPv2 | Partially validated | End-to-end pings passed; learned RIP routes not captured |
| Multilayer switching | Configured | SVIs and routed ports documented |
| Layer 3 DHCP relay | Requires correction | Edmonton helper target and branch gateway exclusions need correction |
| EIGRP | Partially validated | Branch pings passed; neighbor and learned-route evidence not captured |

## Troubleshooting Highlights

This project included several realistic configuration mistakes and corrections:

- Replaced unsupported spaces in VLAN names with underscores.
- Moved DHCP exclusion and `ip routing` commands to global configuration mode.
- Corrected DHCP helper placement and target-address selection.
- Identified printer IP addresses entered in the gateway field.
- Identified an Ottawa interface using the Edmonton LAN address.
- Corrected RIPv2 network statements and missing command keywords.
- Added the required EIGRP transit-network statements to the intended configuration.
- Distinguished successful ping tests from proof of protocol-learned routes.

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

### 1. [VLAN Segmentation and Inter-VLAN Routing](01-vlan-routing/README.md)

Campus VLANs, access-port assignments, router-on-a-stick, DHCP, wireless connectivity, and printer deployment.

### 2. [Network Security with ACLs and Port Security](02-network-security/README.md)

Dedicated access switches, extended ACLs, traffic validation, static port security, violation recovery, and unused-port shutdown.

### 3. [Multi-Site Routing and Layer 3 Switching](03-multisite-routing/README.md)

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















<details>
<summary><strong>VLAN Segmentation and Inter-VLAN Routing</strong></summary>

# Module 1: VLAN Segmentation and Inter-VLAN Routing

**Cisco 2960 | VLANs | Access Ports | 802.1Q | Router-on-a-Stick | DHCP | Wireless | Printers**

[← Return to the main project](../README.md)

## Module Overview

This module covers the campus foundation. I divided the network into departmental VLANs, assigned access ports, verified Layer 2 isolation, and then introduced router-on-a-stick so the VLANs could communicate through controlled Layer 3 gateways.

I also configured DHCP pools, added DNS options, connected wireless endpoints, and expanded the design with departmental printers. The walkthrough preserves the configuration evidence and identifies addressing or command-placement issues visible in the original lab.

## Objectives

- Create VLANs for Administration, Academics, Students, and Servers.
- Assign switch ports to the correct broadcast domains.
- Validate same-VLAN communication and pre-routing VLAN isolation.
- Configure an 802.1Q trunk and router subinterfaces.
- Provide dynamic addressing through Cisco IOS DHCP pools.
- Add wireless clients and departmental printers.
- Record successful tests and unresolved configuration issues accurately.

## Module Addressing

| VLAN | Department | Subnet | Gateway |
|---|---|---|---|
| `10` | Administration | `192.168.10.0/24` | `192.168.10.1` |
| `20` | Academics | `192.168.20.0/24` | `192.168.20.1` |
| `30` | Students | `192.168.30.0/24` | `192.168.30.1` |
| `100` | Server Room | `192.168.100.0/24` | `192.168.100.1` |

## Phase 1: Built the VLAN-Segmented Campus Network

### 1. Created and Named the Core Switch

I added a Cisco 2960 switch and renamed it **CoreSwitch** from the CLI.

```text
Switch> enable
Switch# configure terminal
Switch(config)# hostname CoreSwitch
```

<p align="center">
  <img src="../images/vlan-routing/01.png" width="750" alt="Selecting a Cisco 2960 switch in Packet Tracer">
</p>

<p align="center">
  <img src="../images/vlan-routing/02.png" width="750" alt="Renaming the switch CoreSwitch from the Cisco IOS CLI">
</p>

### 2. Created the Departmental VLANs

I created VLANs for Administration, Academics, Students, and the Server Room. The screenshot records earlier attempts to use spaces in VLAN names, which produced invalid-input messages. I then used underscore-separated names that Cisco IOS accepted.

```text
CoreSwitch(config)# vlan 10
CoreSwitch(config-vlan)# name Administration_Building
CoreSwitch(config-vlan)# vlan 20
CoreSwitch(config-vlan)# name Academics_Building
CoreSwitch(config-vlan)# vlan 30
CoreSwitch(config-vlan)# name Student_Building
CoreSwitch(config-vlan)# vlan 100
CoreSwitch(config-vlan)# name Server_Room
```

<p align="center">
  <img src="../images/vlan-routing/03.png" width="750" alt="Creating VLANs 10, 20, 30, and 100 and correcting VLAN names in Cisco IOS">
</p>

### 3. Assigned Access Ports to the VLANs

I assigned groups of FastEthernet ports to each VLAN and saved the configuration.

```text
CoreSwitch(config)# interface range fa0/2-5
CoreSwitch(config-if-range)# switchport access vlan 10
CoreSwitch(config)# interface range fa0/6-9
CoreSwitch(config-if-range)# switchport access vlan 20
CoreSwitch(config)# interface range fa0/10-14
CoreSwitch(config-if-range)# switchport access vlan 30
CoreSwitch(config)# interface range fa0/15-18
CoreSwitch(config-if-range)# switchport access vlan 100
CoreSwitch(config)# do write
```

<p align="center">
  <img src="../images/vlan-routing/04.png" width="750" alt="Assigning FastEthernet port ranges to campus VLANs">
</p>

I then connected two endpoints to each VLAN and organized the topology by department.

<p align="center">
  <img src="../images/vlan-routing/05.png" width="750" alt="Initial campus topology with Administration, Academics, Student, and Server VLANs">
</p>

### 4. Validated VLAN Isolation

A ping between two hosts in VLAN 10 succeeded, confirming same-VLAN Layer 2 communication.

<p align="center">
  <img src="../images/vlan-routing/06.png" width="750" alt="Successful ping between two hosts in VLAN 10">
</p>

A ping from VLAN 10 to VLAN 20 failed before routing was configured, confirming that the VLANs were isolated.

<p align="center">
  <img src="../images/vlan-routing/07.png" width="750" alt="Failed cross-VLAN ping before inter-VLAN routing was configured">
</p>

## Phase 2: Configured Router-on-a-Stick Inter-VLAN Routing

### 1. Configured the 802.1Q Trunk

I converted CoreSwitch FastEthernet0/1 into a trunk so one physical link could carry traffic for multiple VLANs to the router.

```text
CoreSwitch(config)# interface fa0/1
CoreSwitch(config-if)# switchport mode trunk
CoreSwitch(config-if)# do write
```

<p align="center">
  <img src="../images/vlan-routing/08.png" width="750" alt="Configuring FastEthernet0/1 as an 802.1Q trunk">
</p>

### 2. Renamed and Enabled the Main-Campus Router Interface

I renamed the router **MC_router** and enabled GigabitEthernet0/1 as the parent interface for the VLAN subinterfaces.

<p align="center">
  <img src="../images/vlan-routing/09.png" width="750" alt="Renaming the router MC_router">
</p>

```text
MC_router(config)# interface GigabitEthernet0/1
MC_router(config-if)# no shutdown
```

<p align="center">
  <img src="../images/vlan-routing/10.png" width="750" alt="Enabling the router GigabitEthernet0/1 interface">
</p>

### 3. Created VLAN Subinterfaces

I created one 802.1Q subinterface per VLAN and assigned each subinterface the default-gateway address for its subnet.

```text
MC_router(config)# interface GigabitEthernet0/1.10
MC_router(config-subif)# encapsulation dot1q 10
MC_router(config-subif)# ip address 192.168.10.1 255.255.255.0

MC_router(config)# interface GigabitEthernet0/1.20
MC_router(config-subif)# encapsulation dot1q 20
MC_router(config-subif)# ip address 192.168.20.1 255.255.255.0

MC_router(config)# interface GigabitEthernet0/1.30
MC_router(config-subif)# encapsulation dot1q 30
MC_router(config-subif)# ip address 192.168.30.1 255.255.255.0

MC_router(config)# interface GigabitEthernet0/1.100
MC_router(config-subif)# encapsulation dot1q 100
MC_router(config-subif)# ip address 192.168.100.1 255.255.255.0
MC_router(config-subif)# end
MC_router# write memory
```

<p align="center">
  <img src="../images/vlan-routing/11.png" width="750" alt="Configuring the VLAN 10 router subinterface">
</p>

<p align="center">
  <img src="../images/vlan-routing/12.png" width="750" alt="Configuring the VLAN 20 router subinterface">
</p>

<p align="center">
  <img src="../images/vlan-routing/13.png" width="750" alt="Configuring the VLAN 30 router subinterface">
</p>

<p align="center">
  <img src="../images/vlan-routing/14.png" width="750" alt="Configuring the VLAN 100 router subinterface">
</p>

### 4. Verified the Trunk and Routed Interfaces

The router showed all four subinterfaces in an up/up state.

<p align="center">
  <img src="../images/vlan-routing/15.png" width="750" alt="Verifying router subinterfaces with show ip interface brief">
</p>

The switch reported FastEthernet0/1 as an active 802.1Q trunk carrying VLANs 10, 20, 30, and 100.

<p align="center">
  <img src="../images/vlan-routing/16.png" width="750" alt="Verifying the 802.1Q trunk with show interfaces trunk">
</p>

### 5. Tested Inter-VLAN Connectivity

I added the appropriate default gateway to each endpoint.

<p align="center">
  <img src="../images/vlan-routing/17.png" width="750" alt="Assigning a VLAN default gateway to a campus endpoint">
</p>

Pings between the user VLANs and the Server VLAN then succeeded. The first packet loss visible in one test is consistent with initial address-resolution activity; the repeated tests completed successfully.

<p align="center">
  <img src="../images/vlan-routing/18.png" width="750" alt="Successful inter-VLAN pings after router-on-a-stick configuration">
</p>

<p align="center">
  <img src="../images/vlan-routing/19.png" width="750" alt="Successful ping between a server and an endpoint in another VLAN">
</p>

## Phase 3: Deployed DHCP for the Campus VLANs

### 1. Established the Pre-Configuration Baseline

Before the DHCP pools were fully configured, a client request failed and the host assigned itself an APIPA address. This screenshot provides a useful before-state for the later DHCP validation.

<p align="center">
  <img src="../images/vlan-routing/20.png" width="750" alt="Client showing DHCP failure and an APIPA address before DHCP configuration">
</p>

### 2. Created DHCP Pools

I configured DHCP pools for VLANs 10, 20, and 30.

```text
MC_router(config)# ip dhcp pool VLAN10
MC_router(dhcp-config)# network 192.168.10.0 255.255.255.0
MC_router(dhcp-config)# default-router 192.168.10.1
MC_router(dhcp-config)# exit

MC_router(config)# ip dhcp pool VLAN20
MC_router(dhcp-config)# network 192.168.20.0 255.255.255.0
MC_router(dhcp-config)# default-router 192.168.20.1
MC_router(dhcp-config)# exit

MC_router(config)# ip dhcp pool VLAN30
MC_router(dhcp-config)# network 192.168.30.0 255.255.255.0
MC_router(dhcp-config)# default-router 192.168.30.1
MC_router(dhcp-config)# end
MC_router# write memory
```

<p align="center">
  <img src="../images/vlan-routing/21.png" width="750" alt="Creating DHCP pools for VLANs 10, 20, and 30">
</p>

### 3. Verified DHCP Bindings and Pool Utilization

`show ip dhcp binding` displayed dynamically leased client addresses.

<p align="center">
  <img src="../images/vlan-routing/22.png" width="750" alt="Verifying dynamically assigned addresses with show ip dhcp binding">
</p>

`show ip dhcp pool` displayed the configured scopes and lease statistics.

<p align="center">
  <img src="../images/vlan-routing/23.png" width="750" alt="Verifying DHCP pool utilization and address ranges">
</p>

### 4. Retested Routed Connectivity

DHCP-addressed endpoints successfully reached devices in other VLANs after inter-VLAN routing was in place.

<p align="center">
  <img src="../images/vlan-routing/24.png" width="750" alt="Successful cross-VLAN ping from a DHCP-addressed endpoint">
</p>

<p align="center">
  <img src="../images/vlan-routing/25.png" width="750" alt="Second successful cross-VLAN ping after DHCP configuration">
</p>

### 5. Added a DNS Option and Documented Address Exclusions

I added `8.8.8.8` as the DNS option for the campus DHCP pools. The client screenshot confirms that the DNS value was received, but the topology does not include simulated internet connectivity or a DNS query test.

```text
MC_router(config)# ip dhcp pool VLAN10
MC_router(dhcp-config)# dns-server 8.8.8.8
```

<p align="center">
  <img src="../images/vlan-routing/26.png" width="750" alt="DHCP client receiving the configured DNS server address">
</p>

The source document specifies that addresses `.1` through `.9` should be excluded from the VLAN 10, 20, and 30 pools.

```text
MC_router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.9
MC_router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.9
MC_router(config)# ip dhcp excluded-address 192.168.30.1 192.168.30.9
```

<p align="center">
  <img src="../images/vlan-routing/27.png" width="750" alt="Campus endpoint addressing shown alongside the documented DHCP exclusion task">
</p>

## Phase 4: Added Wireless and Printer Endpoints

### 1. Added a Wireless Router

I added a Packet Tracer wireless router to VLAN 10 and configured its internet-facing connection to receive an address automatically.

<p align="center">
  <img src="../images/vlan-routing/28.png" width="750" alt="Selecting a wireless router for the Administration VLAN">
</p>

The device received `192.168.10.2` and its internal DHCP service was left enabled for the wireless clients.

<p align="center">
  <img src="../images/vlan-routing/29.png" width="750" alt="Wireless router receiving an address and providing a local DHCP scope">
</p>

I configured the SSID **AdminWifi** with WPA2-PSK authentication and AES encryption.

<p align="center">
  <img src="../images/vlan-routing/30.png" width="750" alt="Configuring AdminWifi with WPA2-PSK and AES">
</p>

### 2. Connected the Laptop and Tablet

<p align="center">
  <img src="../images/vlan-routing/31.png" width="750" alt="Laptop connected to AdminWifi">
</p>

<p align="center">
  <img src="../images/vlan-routing/32.png" width="750" alt="Tablet connected to AdminWifi">
</p>

### 3. Added Departmental Printers

<p align="center">
  <img src="../images/vlan-routing/33.png" width="750" alt="VLAN 10 printer configured with 192.168.10.5">
</p>

<p align="center">
  <img src="../images/vlan-routing/34.png" width="750" alt="VLAN 20 printer configuration">
</p>

<p align="center">
  <img src="../images/vlan-routing/35.png" width="750" alt="VLAN 30 printer configuration">
</p>

<p align="center">
  <img src="../images/vlan-routing/36.png" width="750" alt="Expanded campus topology">
</p>

## Module Validation Summary

| Test | Result | Evidence |
|---|---|---|
| VLAN creation and access-port assignment | Passed | VLAN and interface configuration captured |
| Same-VLAN connectivity | Passed | VLAN 10 hosts exchanged ICMP replies |
| Cross-VLAN isolation before routing | Passed | Inter-VLAN ping failed as expected |
| 802.1Q trunk | Passed | FastEthernet0/1 shown operating as a trunk |
| Router subinterfaces | Passed | Four gateway subinterfaces shown up/up |
| Inter-VLAN routing | Passed | User and server VLANs exchanged traffic |
| Campus DHCP | Passed | Pool statistics and client bindings displayed |
| DNS option delivery | Passed | Client received `8.8.8.8`; name resolution was not tested |
| Wireless association | Passed | Laptop and tablet joined `AdminWifi` |
| Printer addressing | Partially configured | VLAN 20 and VLAN 30 captures require correction |

## Technical Notes

- Cisco IOS rejected VLAN names containing spaces, so underscores were used.
- DHCP exclusion commands belong in global configuration mode.
- A production wireless design should avoid overlapping DHCP services.
- The VLAN 20 and VLAN 30 printers should use `.5` as the interface address and `.1` as the gateway.

## Module Outcome

This stage established the campus switching, routing, and addressing foundation. It demonstrated the difference between Layer 2 segmentation and Layer 3 communication, then extended the environment with automatically addressed wired and wireless endpoints.



</details>
























<details>
<summary><strong>Network Security with ACLs and Port Security</strong></summary>

# Module 2: Network Security with ACLs and Port Security

**Extended ACLs | Traffic Filtering | Port Security | Violation Recovery | Interface Hardening**

[← Return to the main project](../README.md)

## Module Overview

This module strengthens the campus access layer. I added dedicated switches for the main user departments, applied extended access control lists to enforce traffic restrictions, secured server-facing interfaces with static MAC addresses, and disabled unused switch ports.

The validation includes both permitted and denied traffic, the directional effect of an ACL, and the observed shutdown and recovery of a protected server port.

## Security Requirements

| Control | Intended Result |
|---|---|
| ACL 100 | Prevent VLAN 30 from reaching VLAN 100 while allowing approved departmental access |
| ACL 110 | Block ICMP echo from VLAN 20 to VLAN 10 while permitting other IP traffic |
| Static port security | Restrict server-facing ports to approved MAC addresses |
| Shutdown violation mode | Disable a secured port when an unauthorized device is connected |
| Unused-port shutdown | Reduce the number of exposed access interfaces |

## Phase 5: Expanded and Secured the Access Layer

### 1. Added Dedicated Access Switches

I added a Cisco 2960 access switch for the Administration building and repeated the design for the Academics and Student buildings.

<p align="center">
  <img src="../images/security/01.png" width="750" alt="Selecting a Cisco 2960 access switch">
</p>

<p align="center">
  <img src="../images/security/02.png" width="750" alt="Renaming the Administration access switch">
</p>

```text
AccessSwitch-AdministrationBuilding(config)# vlan 10
AccessSwitch-AdministrationBuilding(config-vlan)# name AdministrationBuilding
AccessSwitch-AdministrationBuilding(config)# interface range fa0/1-24
AccessSwitch-AdministrationBuilding(config-if-range)# switchport mode access
AccessSwitch-AdministrationBuilding(config-if-range)# switchport access vlan 10
AccessSwitch-AdministrationBuilding(config-if-range)# do write
```

<p align="center">
  <img src="../images/security/03.png" width="750" alt="Configuring the Administration switch for VLAN 10">
</p>

<p align="center">
  <img src="../images/security/04.png" width="750" alt="Configuring the Academics switch for VLAN 20">
</p>

<p align="center">
  <img src="../images/security/05.png" width="750" alt="Configuring the Student switch for VLAN 30">
</p>

### 2. Removed Unused VLAN Assignments

```text
CoreSwitch(config)# interface range fa0/3-5
CoreSwitch(config-if-range)# no switchport access vlan 10
CoreSwitch(config)# interface range fa0/7-9
CoreSwitch(config-if-range)# no switchport access vlan 20
CoreSwitch(config)# interface range fa0/11-14
CoreSwitch(config-if-range)# no switchport access vlan 30
CoreSwitch(config)# do write
CoreSwitch# show vlan brief
```

<p align="center">
  <img src="../images/security/06.png" width="750" alt="Removing obsolete VLAN assignments">
</p>

<p align="center">
  <img src="../images/security/07.png" width="750" alt="Verifying VLAN port assignments">
</p>

### 3. Applied ACL 100 to Protect the Server VLAN

```text
MC_router(config)# access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.100.0 0.0.0.255
MC_router(config)# access-list 100 permit ip 192.168.10.0 0.0.0.255 192.168.100.0 0.0.0.255
MC_router(config)# access-list 100 permit ip 192.168.20.0 0.0.0.255 192.168.100.0 0.0.0.255
MC_router(config)# interface GigabitEthernet0/1.100
MC_router(config-subif)# ip access-group 100 out
MC_router(config-subif)# do write
```

<p align="center">
  <img src="../images/security/08.png" width="750" alt="Creating and applying ACL 100">
</p>

<p align="center">
  <img src="../images/security/09.png" width="750" alt="Verifying ACL 100">
</p>

> **Scope note:** ACL 100 ends with an implicit deny. Any source that is not explicitly permitted will also be denied access to VLAN 100.

### 4. Validated ACL 100

A host in VLAN 10 successfully reached server `192.168.100.10`.

<p align="center">
  <img src="../images/security/10.png" width="750" alt="Successful VLAN 10-to-server ping">
</p>

A host in VLAN 20 also reached the server.

<p align="center">
  <img src="../images/security/11.png" width="750" alt="Successful VLAN 20-to-server ping">
</p>

Traffic from VLAN 30 to the server was denied.

<p align="center">
  <img src="../images/security/12.png" width="750" alt="Blocked VLAN 30-to-server ping">
</p>

### 5. Applied ACL 110 to Restrict ICMP

```text
MC_router(config)# access-list 110 deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 echo
MC_router(config)# access-list 110 permit ip any any
MC_router(config)# interface GigabitEthernet0/1.10
MC_router(config-subif)# ip access-group 110 out
MC_router(config-subif)# do write
```

<p align="center">
  <img src="../images/security/13.png" width="750" alt="Creating and applying ACL 110">
</p>

The VLAN 20-to-VLAN 10 ping failed as intended.

<p align="center">
  <img src="../images/security/14.png" width="750" alt="Blocked VLAN 20-to-VLAN 10 ping">
</p>

The reverse-direction test succeeded.

<p align="center">
  <img src="../images/security/15.png" width="750" alt="Successful reverse-direction ping">
</p>

### 6. Configured Static Port Security

```text
CoreSwitch(config)# interface fa0/16
CoreSwitch(config-if)# switchport mode access
CoreSwitch(config-if)# switchport port-security
CoreSwitch(config-if)# switchport port-security mac-address <SERVER_MAC_ADDRESS>
CoreSwitch(config-if)# switchport port-security violation shutdown
CoreSwitch(config-if)# do write
```

<p align="center">
  <img src="../images/security/16.png" width="750" alt="Configuring switch port security">
</p>

<p align="center">
  <img src="../images/security/17.png" width="750" alt="Verifying port-security status">
</p>

### 7. Triggered and Recovered from a Violation

I moved the servers to each other’s ports and generated traffic. The affected links changed to a down state.

<p align="center">
  <img src="../images/security/18.png" width="750" alt="Server link down after a port-security violation">
</p>

```text
CoreSwitch(config)# interface fa0/16
CoreSwitch(config-if)# shutdown
CoreSwitch(config-if)# no shutdown
```

<p align="center">
  <img src="../images/security/19.png" width="750" alt="Resetting the secured interface">
</p>

<p align="center">
  <img src="../images/security/20.png" width="750" alt="Server link restored">
</p>

### 8. Disabled Unused Ports

<p align="center">
  <img src="../images/security/21.png" width="750" alt="Reviewing switch interface status">
</p>

```text
CoreSwitch(config)# interface range fa0/3-5
CoreSwitch(config-if-range)# shutdown
CoreSwitch(config)# interface range fa0/7-9
CoreSwitch(config-if-range)# shutdown
CoreSwitch(config)# interface range fa0/11-14
CoreSwitch(config-if-range)# shutdown
CoreSwitch(config)# interface range fa0/17-24
CoreSwitch(config-if-range)# shutdown
```

<p align="center">
  <img src="../images/security/22.png" width="750" alt="Shutting down unused interfaces">
</p>

<p align="center">
  <img src="../images/security/23.png" width="750" alt="Verifying administratively disabled ports">
</p>

## Module Validation Summary

| Control | Result | Evidence |
|---|---|---|
| Dedicated access switches | Configured | VLAN-specific switch configuration captured |
| ACL 100 permitted traffic | Passed | VLANs 10 and 20 reached the server network |
| ACL 100 denied traffic | Passed | VLAN 30 could not reach the server network |
| ACL 110 directional restriction | Passed | VLAN 20-to-VLAN 10 echo failed while the reverse test passed |
| Port-security configuration | Configured | Secure-up state and one secure address displayed |
| Port-security behavior | Observed | Link shutdown and recovery captured |
| Port-security violation counter | Not captured | No post-test output showed a nonzero counter |
| Unused-port shutdown | Passed | Selected interfaces shown administratively down |

## Technical Notes

- ACL 100 ends with an implicit deny.
- Extended ACL placement should reflect the intended traffic direction.
- Each secured port must use a unique server MAC address.
- A post-violation `show port-security interface` capture would provide stronger evidence.
- Unused ports should also be placed in an unused VLAN before shutdown.

## Module Outcome

This stage introduced controls at both Layer 3 and Layer 2. The ACL tests demonstrated selective network access, while port security and interface shutdown reduced the risk of unauthorized access through the switching infrastructure.



</details>

























<details>
<summary><strong>Multi-Site Routing and Layer 3 Switching</strong></summary>

# Module 3: Multi-Site Routing and Layer 3 Switching

**Static Routing | DHCP Relay | RIPv2 | Multilayer Switching | Routed Ports | EIGRP**

[← Return to the main project](../README.md)

## Module Overview

This module expands the campus network to Edmonton and Ottawa. I first connected the branches through serial point-to-point links, configured static routes, and placed the branch DHCP scopes on the main-campus router. I then removed the static routes and tested RIPv2 before redesigning the topology with Cisco 3560 multilayer switches and EIGRP.

Because this stage contains several migrations and troubleshooting steps, the walkthrough separates intended configurations from what the screenshots conclusively verify.

## Multi-Site Addressing

| Network or Link | Subnet | Interface Addresses |
|---|---|---|
| Edmonton LAN | `192.168.60.0/24` | Gateway `192.168.60.1` |
| Ottawa LAN | `192.168.70.0/24` | Gateway `192.168.70.1` |
| Main Campus to Edmonton | `172.16.10.0/30` | Main Campus `.1`, Edmonton `.2` |
| Main Campus to Ottawa | `172.16.11.0/30` | Main Campus `.1`, Ottawa `.2` |

## Routing Evolution

| Stage | Purpose | Evidence Status |
|---|---|---|
| Static routes | Establish campus-to-branch and inter-branch paths | Passed for tested paths |
| RIPv2 | Replace manual routes with dynamic advertisements | Partially validated |
| Layer 3 switching | Move routing functions to multilayer switches | Configured |
| EIGRP AS 100 | Exchange campus and branch routes dynamically | Partially validated |

## Phase 6: Connected the Edmonton and Ottawa Branches

### 1. Built the Edmonton Branch

<p align="center">
  <img src="../images/multisite-routing/01.png" width="750" alt="Edmonton branch topology">
</p>

```text
Edmonton-Router(config)# interface FastEthernet0/0
Edmonton-Router(config-if)# ip address 192.168.60.1 255.255.255.0
Edmonton-Router(config-if)# no shutdown
Edmonton-Router(config-if)# do write
```

<p align="center">
  <img src="../images/multisite-routing/02.png" width="750" alt="Configuring the Edmonton gateway">
</p>

<p align="center">
  <img src="../images/multisite-routing/03.png" width="750" alt="Configuring the first Edmonton PC">
</p>

<p align="center">
  <img src="../images/multisite-routing/04.png" width="750" alt="Configuring the second Edmonton PC">
</p>

### 2. Added the Edmonton WAN Link

<p align="center">
  <img src="../images/multisite-routing/05.png" width="750" alt="Installing the main-campus serial module">
</p>

<p align="center">
  <img src="../images/multisite-routing/06.png" width="750" alt="Installing the Edmonton serial module">
</p>

<p align="center">
  <img src="../images/multisite-routing/07.png" width="750" alt="Connecting Edmonton to the main campus">
</p>

```text
MC_router(config)# interface Serial0/0/0
MC_router(config-if)# ip address 172.16.10.1 255.255.255.252
MC_router(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/08.png" width="750" alt="Configuring the main-campus Edmonton link">
</p>

```text
Edmonton-Router(config)# interface Serial0/0/0
Edmonton-Router(config-if)# ip address 172.16.10.2 255.255.255.252
Edmonton-Router(config-if)# clock rate 64000
Edmonton-Router(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/09.png" width="750" alt="Configuring the Edmonton serial link">
</p>

### 3. Verified Edmonton Connectivity

<p align="center">
  <img src="../images/multisite-routing/10.png" width="750" alt="Edmonton PC reaching its gateway">
</p>

<p align="center">
  <img src="../images/multisite-routing/11.png" width="750" alt="Testing the Edmonton point-to-point link">
</p>

### 4. Added Static Routes for Edmonton

```text
MC_router(config)# ip route 192.168.60.0 255.255.255.0 172.16.10.2
```

<p align="center">
  <img src="../images/multisite-routing/12.png" width="750" alt="Adding the Edmonton static route">
</p>

```text
Edmonton-Router(config)# ip route 192.168.10.0 255.255.255.0 172.16.10.1
Edmonton-Router(config)# ip route 192.168.20.0 255.255.255.0 172.16.10.1
Edmonton-Router(config)# ip route 192.168.100.0 255.255.255.0 172.16.10.1
Edmonton-Router(config)# do write
```

<p align="center">
  <img src="../images/multisite-routing/13.png" width="750" alt="Adding Edmonton return routes">
</p>

<p align="center">
  <img src="../images/multisite-routing/14.png" width="750" alt="Successful main-campus-to-Edmonton ping">
</p>

<p align="center">
  <img src="../images/multisite-routing/15.png" width="750" alt="Successful Edmonton-to-main-campus ping">
</p>

### 5. Configured DHCP Relay for Edmonton

```text
MC_router(config)# ip dhcp pool EDMONTON
MC_router(dhcp-config)# network 192.168.60.0 255.255.255.0
MC_router(dhcp-config)# default-router 192.168.60.1
MC_router(dhcp-config)# do write
```

<p align="center">
  <img src="../images/multisite-routing/16.png" width="750" alt="Creating the Edmonton DHCP pool">
</p>

```text
Edmonton-Router(config)# interface FastEthernet0/0
Edmonton-Router(config-if)# ip helper-address 172.16.10.1
Edmonton-Router(config-if)# do write
```

<p align="center">
  <img src="../images/multisite-routing/17.png" width="750" alt="Configuring Edmonton DHCP relay">
</p>

### 6. Built the Ottawa Branch

<p align="center">
  <img src="../images/multisite-routing/18.png" width="750" alt="Ottawa branch topology">
</p>

```text
Ottawa-Router(config)# interface FastEthernet0/0
Ottawa-Router(config-if)# ip address 192.168.70.1 255.255.255.0
Ottawa-Router(config-if)# no shutdown
Ottawa-Router(config-if)# do write
```

<p align="center">
  <img src="../images/multisite-routing/19.png" width="750" alt="Configuring the Ottawa gateway">
</p>

<p align="center">
  <img src="../images/multisite-routing/20.png" width="750" alt="Configuring the first Ottawa PC">
</p>

<p align="center">
  <img src="../images/multisite-routing/21.png" width="750" alt="Configuring the second Ottawa PC">
</p>

### 7. Added the Ottawa WAN Link

<p align="center">
  <img src="../images/multisite-routing/22.png" width="750" alt="Installing the Ottawa serial module">
</p>

<p align="center">
  <img src="../images/multisite-routing/23.png" width="750" alt="Expanded multi-site topology">
</p>

```text
MC_router(config)# interface Serial0/0/1
MC_router(config-if)# ip address 172.16.11.1 255.255.255.252
MC_router(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/24.png" width="750" alt="Configuring the main-campus Ottawa link">
</p>

```text
Ottawa-Router(config)# interface Serial0/0/1
Ottawa-Router(config-if)# ip address 172.16.11.2 255.255.255.252
Ottawa-Router(config-if)# clock rate 64000
Ottawa-Router(config-if)# no shutdown
Ottawa-Router(config-if)# do write
```

<p align="center">
  <img src="../images/multisite-routing/25.png" width="750" alt="Configuring the Ottawa serial link">
</p>

### 8. Added Ottawa and Inter-Branch Static Routes

```text
MC_router(config)# ip route 192.168.70.0 255.255.255.0 172.16.11.2
```

<p align="center">
  <img src="../images/multisite-routing/26.png" width="750" alt="Adding the Ottawa static route">
</p>

```text
Ottawa-Router(config)# ip route 192.168.10.0 255.255.255.0 172.16.11.1
Ottawa-Router(config)# ip route 192.168.20.0 255.255.255.0 172.16.11.1
Ottawa-Router(config)# ip route 192.168.30.0 255.255.255.0 172.16.11.1
Ottawa-Router(config)# ip route 192.168.60.0 255.255.255.0 172.16.11.1
Ottawa-Router(config)# do write
```

<p align="center">
  <img src="../images/multisite-routing/27.png" width="750" alt="Adding Ottawa return routes">
</p>

```text
Edmonton-Router(config)# ip route 192.168.70.0 255.255.255.0 172.16.10.1
```

<p align="center">
  <img src="../images/multisite-routing/28.png" width="750" alt="Adding the Edmonton-to-Ottawa route">
</p>

### 9. Configured DHCP Relay for Ottawa

```text
MC_router(config)# ip dhcp pool OTTAWA
MC_router(dhcp-config)# network 192.168.70.0 255.255.255.0
MC_router(dhcp-config)# default-router 192.168.70.1
MC_router(dhcp-config)# do write
```

<p align="center">
  <img src="../images/multisite-routing/29.png" width="750" alt="Creating the Ottawa DHCP pool">
</p>

```text
Ottawa-Router(config)# interface FastEthernet0/0
Ottawa-Router(config-if)# ip helper-address 172.16.11.1
Ottawa-Router(config-if)# do write
```

<p align="center">
  <img src="../images/multisite-routing/30.png" width="750" alt="Configuring Ottawa DHCP relay">
</p>

## Phase 7: Migrated from Static Routing to RIPv2

### 1. Removed the Static Routes

<p align="center">
  <img src="../images/multisite-routing/31.png" width="750" alt="Removing static routes from the main-campus router">
</p>

<p align="center">
  <img src="../images/multisite-routing/32.png" width="750" alt="Removing static routes from Edmonton">
</p>

<p align="center">
  <img src="../images/multisite-routing/33.png" width="750" alt="Removing static routes from Ottawa">
</p>

### 2. Configured RIPv2

```text
MC_router(config)# router rip
MC_router(config-router)# version 2
MC_router(config-router)# network 192.168.10.0
MC_router(config-router)# network 192.168.20.0
MC_router(config-router)# network 192.168.30.0
MC_router(config-router)# network 172.16.10.0
MC_router(config-router)# network 172.16.11.0
MC_router(config-router)# no auto-summary
```

<p align="center">
  <img src="../images/multisite-routing/34.png" width="750" alt="Configuring RIPv2 on the main-campus router">
</p>

```text
Edmonton-Router(config)# router rip
Edmonton-Router(config-router)# version 2
Edmonton-Router(config-router)# network 172.16.10.0
Edmonton-Router(config-router)# network 192.168.60.0
Edmonton-Router(config-router)# no auto-summary
```

<p align="center">
  <img src="../images/multisite-routing/35.png" width="750" alt="Configuring RIPv2 on Edmonton">
</p>

```text
Ottawa-Router(config)# router rip
Ottawa-Router(config-router)# version 2
Ottawa-Router(config-router)# network 172.16.11.0
Ottawa-Router(config-router)# network 192.168.70.0
Ottawa-Router(config-router)# no auto-summary
```

<p align="center">
  <img src="../images/multisite-routing/36.png" width="750" alt="Configuring RIPv2 on Ottawa">
</p>

### 3. Tested RIP-Stage Reachability

<p align="center">
  <img src="../images/multisite-routing/37.png" width="750" alt="Successful Ottawa-to-main-campus ping">
</p>

<p align="center">
  <img src="../images/multisite-routing/38.png" width="750" alt="Successful Edmonton-to-main-campus ping">
</p>

<p align="center">
  <img src="../images/multisite-routing/39.png" width="750" alt="Successful Edmonton-to-Ottawa ping">
</p>

The tests confirm reachability, but no `show ip route rip` or `show ip protocols` output was captured.

## Phase 8: Redesigned the Network with Layer 3 Switches and EIGRP

### 1. Replaced the Router with a Multilayer Switch

<p align="center">
  <img src="../images/multisite-routing/40.png" width="750" alt="Selecting a Cisco 3560 multilayer switch">
</p>

<p align="center">
  <img src="../images/multisite-routing/41.png" width="750" alt="Renaming the multilayer switch MC_Switch">
</p>

### 2. Recreated the Campus VLANs

<p align="center">
  <img src="../images/multisite-routing/42.png" width="750" alt="Verifying VLANs on MC_Switch">
</p>

```text
MC_Switch(config)# interface fa0/2
MC_Switch(config-if)# switchport access vlan 10
MC_Switch(config)# interface fa0/3
MC_Switch(config-if)# switchport access vlan 20
MC_Switch(config)# interface fa0/4
MC_Switch(config-if)# switchport access vlan 30
MC_Switch(config)# interface fa0/5
MC_Switch(config-if)# switchport access vlan 50
MC_Switch(config)# interface range fa0/6-7
MC_Switch(config-if-range)# switchport access vlan 100
MC_Switch(config-if-range)# do write
```

<p align="center">
  <img src="../images/multisite-routing/43.png" width="750" alt="Assigning MC_Switch access ports">
</p>

<p align="center">
  <img src="../images/multisite-routing/44.png" width="750" alt="Verifying VLAN membership">
</p>

### 3. Created Switched Virtual Interfaces

```text
MC_Switch(config)# ip routing

MC_Switch(config)# interface vlan 10
MC_Switch(config-if)# ip address 192.168.10.1 255.255.255.0

MC_Switch(config)# interface vlan 20
MC_Switch(config-if)# ip address 192.168.20.1 255.255.255.0

MC_Switch(config)# interface vlan 30
MC_Switch(config-if)# ip address 192.168.30.1 255.255.255.0

MC_Switch(config)# interface vlan 50
MC_Switch(config-if)# ip address 192.168.50.1 255.255.255.0

MC_Switch(config)# interface vlan 100
MC_Switch(config-if)# ip address 192.168.100.1 255.255.255.0
```

<p align="center">
  <img src="../images/multisite-routing/45.png" width="750" alt="Creating VLAN interfaces on MC_Switch">
</p>

### 4. Recreated the Campus DHCP Pools

<p align="center">
  <img src="../images/multisite-routing/46.png" width="750" alt="Creating DHCP pools on MC_Switch">
</p>

### 5. Converted Branch Links to Routed Ports

<p align="center">
  <img src="../images/multisite-routing/47.png" width="750" alt="Layer 3 branch topology">
</p>

```text
MC_Switch(config)# interface GigabitEthernet0/1
MC_Switch(config-if)# no switchport
MC_Switch(config-if)# ip address 172.16.10.1 255.255.255.252
MC_Switch(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/48.png" width="750" alt="Configuring the Edmonton link on MC_Switch">
</p>

```text
Edmonton-Switch(config)# interface GigabitEthernet0/1
Edmonton-Switch(config-if)# no switchport
Edmonton-Switch(config-if)# ip address 172.16.10.2 255.255.255.252
Edmonton-Switch(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/49.png" width="750" alt="Configuring the Edmonton routed uplink">
</p>

<p align="center">
  <img src="../images/multisite-routing/50.png" width="750" alt="Configuring the Edmonton LAN interface">
</p>

```text
MC_Switch(config)# interface GigabitEthernet0/2
MC_Switch(config-if)# no switchport
MC_Switch(config-if)# ip address 172.16.11.1 255.255.255.252
MC_Switch(config-if)# no shutdown
```

<p align="center">
  <img src="../images/multisite-routing/51.png" width="750" alt="Configuring the Ottawa link on MC_Switch">
</p>

<p align="center">
  <img src="../images/multisite-routing/52.png" width="750" alt="Configuring the Ottawa routed uplink">
</p>

<p align="center">
  <img src="../images/multisite-routing/53.png" width="750" alt="Reviewing the Ottawa LAN interface">
</p>

The intended Ottawa LAN configuration is:

```text
Ottawa-Switch(config)# interface FastEthernet0/1
Ottawa-Switch(config-if)# no switchport
Ottawa-Switch(config-if)# ip address 192.168.70.1 255.255.255.0
Ottawa-Switch(config-if)# no shutdown
```

### 6. Added the Branch DHCP Pools

```text
MC_Switch(config)# ip dhcp pool OTTAWA
MC_Switch(dhcp-config)# network 192.168.70.0 255.255.255.0
MC_Switch(dhcp-config)# default-router 192.168.70.1
```

<p align="center">
  <img src="../images/multisite-routing/54.png" width="750" alt="Creating the Ottawa DHCP pool">
</p>

<p align="center">
  <img src="../images/multisite-routing/55.png" width="750" alt="Displaying branch DHCP pools">
</p>

```text
MC_Switch(config)# ip dhcp excluded-address 192.168.60.1
MC_Switch(config)# ip dhcp excluded-address 192.168.70.1
```

### 7. Reviewed Layer 3 DHCP Relay

<p align="center">
  <img src="../images/multisite-routing/56.png" width="750" alt="Reviewing Edmonton DHCP relay">
</p>

```text
Edmonton-Switch(config)# interface FastEthernet0/1
Edmonton-Switch(config-if)# ip helper-address 172.16.10.1
```

<p align="center">
  <img src="../images/multisite-routing/57.png" width="750" alt="Correcting Ottawa DHCP relay">
</p>

### 8. Configured EIGRP AS 100

<p align="center">
  <img src="../images/multisite-routing/58.png" width="750" alt="Configuring EIGRP on MC_Switch">
</p>

```text
MC_Switch(config)# ip routing
MC_Switch(config)# router eigrp 100
MC_Switch(config-router)# network 192.168.10.0 0.0.0.255
MC_Switch(config-router)# network 192.168.20.0 0.0.0.255
MC_Switch(config-router)# network 192.168.30.0 0.0.0.255
MC_Switch(config-router)# network 192.168.50.0 0.0.0.255
MC_Switch(config-router)# network 192.168.100.0 0.0.0.255
MC_Switch(config-router)# network 172.16.10.0 0.0.0.3
MC_Switch(config-router)# network 172.16.11.0 0.0.0.3
```

```text
Edmonton-Switch(config)# ip routing
Edmonton-Switch(config)# router eigrp 100
Edmonton-Switch(config-router)# network 192.168.60.0 0.0.0.255
Edmonton-Switch(config-router)# network 172.16.10.0 0.0.0.3
```

<p align="center">
  <img src="../images/multisite-routing/59.png" width="750" alt="Configuring EIGRP on Edmonton-Switch">
</p>

```text
Ottawa-Switch(config)# ip routing
Ottawa-Switch(config)# router eigrp 100
Ottawa-Switch(config-router)# network 192.168.70.0 0.0.0.255
Ottawa-Switch(config-router)# network 172.16.11.0 0.0.0.3
```

<p align="center">
  <img src="../images/multisite-routing/60.png" width="750" alt="Configuring EIGRP on Ottawa-Switch">
</p>

### 9. Tested Branch-to-Branch Reachability

<p align="center">
  <img src="../images/multisite-routing/61.png" width="750" alt="Successful Ottawa-to-Edmonton ping">
</p>

<p align="center">
  <img src="../images/multisite-routing/62.png" width="750" alt="Successful Edmonton-to-Ottawa ping">
</p>

## Module Validation Summary

| Area | Result | Evidence and Limitation |
|---|---|---|
| Edmonton LAN and point-to-point link | Passed | Local gateway and transit pings succeeded |
| Edmonton static routing | Passed for tested paths | Main-campus and VLAN 10 paths succeeded |
| Ottawa static routing | Configured | Route commands were captured |
| Router-based DHCP relay | Configured | Correct helper targets captured; branch leases not shown |
| RIPv2 | Partially validated | Pings passed, but no RIP route table was captured |
| Campus SVIs | Configured | Gateway interfaces and addresses captured |
| Routed switch links | Configured | Both transit links documented |
| Ottawa Layer 3 LAN interface | Requires correction | Capture shows `192.168.60.1` instead of `192.168.70.1` |
| Branch DHCP exclusions | Requires correction | Gateway addresses remain inside the allocatable ranges |
| Edmonton Layer 3 DHCP relay | Requires correction | Helper targets the local `.2` address |
| EIGRP | Partially validated | Branch pings passed; neighbor and learned-route evidence was not captured |

## Required Final Corrections

- Correct the Ottawa client-facing interface to `192.168.70.1/24`.
- Exclude `192.168.60.1` and `192.168.70.1` from the branch DHCP pools.
- Point Edmonton’s helper address to `172.16.10.1`.
- Confirm that MC_Switch advertises both transit networks in EIGRP.
- Capture `show ip eigrp neighbors`, `show ip route eigrp`, and `show ip protocols`.
- Save a final clean running configuration after every correction.

## Module Outcome

This stage demonstrated the operational difference between static and dynamic routing and showed how a router-based campus can migrate to multilayer switching. Connectivity tests confirmed that the sites could communicate, while the review identified the additional protocol evidence and addressing corrections required for a fully validated final design.



</details>
