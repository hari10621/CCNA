# Inter-VLAN Routing Using Switch Virtual Interfaces (SVI)

**Lab platform:** Cisco Packet Tracer  
**Main topic:** SVI-based inter-VLAN routing using a Layer 3 switch  
**Devices:** 1 Cisco 3560-24PS multilayer switch, 1 Cisco 2911 router, 6 PCs

## 1. Objective

Create three separate VLANs and use Switch Virtual Interfaces (SVIs) on a multilayer switch as the default gateways. Enable Layer 3 routing on the switch so hosts in different VLANs can communicate. The router is connected to the multilayer switch as an upstream Layer 3 device.

## 2. Topology

The topology contains six PCs connected directly to the 3560 multilayer switch:

- VLAN 10: PC0 and PC1
- VLAN 20: PC2 and PC3
- VLAN 30: PC4 and PC5
- Router0: connected to the multilayer switch using a routed point-to-point link

See [`screenshots/01-network-topology.png`](screenshots/01-network-topology.png).

## 3. VLAN and IP addressing plan

| VLAN ID | VLAN name | Network | SVI / default gateway |
|---:|---|---|---|
| 10 | VLAN10 | 192.168.10.0/24 | 192.168.10.1 |
| 20 | VLAN20 | 192.168.20.0/24 | 192.168.20.1 |
| 30 | VLAN30 | 192.168.30.0/24 | 192.168.30.1 |

Subnet mask for all three VLANs: `255.255.255.0`.

## 4. PC addressing and switch-port mapping

| PC | Switch port | VLAN | IPv4 address | Subnet mask | Default gateway |
|---|---|---:|---|---|---|
| PC0 | Fa0/1 | 10 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC1 | Fa0/2 | 10 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC2 | Fa0/3 | 20 | 192.168.20.11 | 255.255.255.0 | 192.168.20.1 |
| PC3 | Fa0/4 | 20 | 192.168.20.12 | 255.255.255.0 | 192.168.20.1 |
| PC4 | Fa0/5 | 30 | 192.168.30.11 | 255.255.255.0 | 192.168.30.1 |
| PC5 | Fa0/6 | 30 | 192.168.30.12 | 255.255.255.0 | 192.168.30.1 |

The PC addressing values above are transcribed from the submitted Packet Tracer screenshots.

## 5. Configuration summary

| Device | Interface / feature | Configuration purpose |
|---|---|---|
| L3-SWITCH | VLAN 10, 20, 30 | Create the three VLANs |
| L3-SWITCH | Fa0/1–Fa0/2 | Access ports for VLAN 10 |
| L3-SWITCH | Fa0/3–Fa0/4 | Access ports for VLAN 20 |
| L3-SWITCH | Fa0/5–Fa0/6 | Access ports for VLAN 30 |
| L3-SWITCH | VLAN 10 SVI | Gateway 192.168.10.1/24 |
| L3-SWITCH | VLAN 20 SVI | Gateway 192.168.20.1/24 |
| L3-SWITCH | VLAN 30 SVI | Gateway 192.168.30.1/24 |
| L3-SWITCH | `ip routing` | Enables inter-VLAN routing |
| L3-SWITCH | Routed uplink | Point-to-point connection to router |
| Router0 | Routed uplink | 10.0.0.1/30 (recommended final addressing) |
| Router0 | Static routes | Return paths to the three VLAN networks |

## 6. Verification evidence currently included

| Evidence file | What it demonstrates |
|---|---|
| 01-network-topology.png | Physical topology and VLAN grouping |
| 02-pc-ip-addressing.png | Static IPv4 settings for all six PCs |
| 03-vlan-creation.png | VLAN creation commands |
| 04-access-port-vlan-assignment.png | Access-port membership commands |
| 05-svi-vlan-10-configuration.png | VLAN 10 SVI address and no shutdown |
| 06-svi-vlan-20-configuration.png | VLAN 20 SVI address and no shutdown |
| 07-svi-vlan-30-configuration.png | VLAN 30 SVI address and no shutdown |
| 08-router-configuration-evidence.png | Router CLI screenshot supplied |
| 09-ping-vlan-30-gateway.png | PC successfully pings 192.168.30.1 |

**Important evidence limitation:** The supplied ping screenshot proves reachability to the VLAN 30 gateway SVI. By itself, it does not prove end-to-end communication between different VLAN hosts. Capture additional cross-VLAN pings (for example, PC0 to 192.168.20.11 and PC0 to 192.168.30.11) after completing and verifying `ip routing`.

## 7. Additional screenshots to capture for complete proof

- `10-ip-routing-enabled.png` — switch CLI showing `show running-config | include ip routing` or the `ip routing` configuration.
- `11-svi-and-uplink-status.png` — `show ip interface brief`, with all three SVIs and the routed uplink up/up.
- `12-switch-routing-table.png` — `show ip route`, showing the three connected VLAN networks.
- `13-cross-vlan-ping-tests.png` — successful PC-to-PC pings across VLAN 10, VLAN 20 and VLAN 30.
- `14-router-routes.png` — router `show ip route`, showing static routes to all VLAN subnets.

## 8. Learning outcomes

- Created and assigned VLANs.
- Configured SVIs as VLAN default gateways.
- Understood the role of `ip routing` on a multilayer switch.
- Distinguished SVI-based routing from Router-on-a-Stick.
- Practised routed switch-to-router connectivity and static routing.
- Verified interface status and IP connectivity.

## 9. Packet Tracer project

Save the completed Packet Tracer file in this folder as:

`inter-vlan-routing-using-svi.pkt`

The Packet Tracer `.pkt` file was not part of the supplied uploads, so it must be added locally after saving the lab.
