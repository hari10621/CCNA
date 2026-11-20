# RSTP (Rapid Spanning Tree Protocol) — CCNA Lab

## 1. Objective

The objective of this lab is to configure and verify Rapid Spanning Tree Protocol (RSTP) in a redundant Layer 2 switching topology using four Cisco switches and four PCs.

This lab demonstrates:

- RSTP configuration using Rapid PVST+
- Root Bridge election
- Spanning Tree port roles and states
- Edge and point-to-point link identification
- Loop prevention through redundant link management
- Network connectivity verification

---

## 2. Network Architecture

The lab consists of four interconnected switches arranged in a redundant ring topology. Each switch is connected to one PC.

### Architecture Diagram

![RSTP Architecture Diagram](screenshots/01%20-%20architecture%20diagram.png)

The redundant connection between switches provides multiple paths through the network. RSTP prevents Layer 2 loops by placing a redundant path into a non-forwarding state.

---

## 3. PC IP Configuration

All PCs are configured within the same subnet, allowing communication between them without requiring a router.

| Device | IP Address | Subnet Mask |
|---|---|---|
| PC1 | 192.168.10.11 | 255.255.255.0 |
| PC2 | 192.168.10.12 | 255.255.255.0 |
| PC3 | 192.168.10.13 | 255.255.255.0 |
| PC4 | 192.168.10.14 | 255.255.255.0 |

### IP Configuration Evidence

![PC IP Configuration](screenshots/02-%20%20PC%20ip%20config.png)

---

## 4. Switch Configuration

RSTP is configured using Rapid PVST+ (`rapid-pvst`).

SW1 is configured with the lowest bridge priority to ensure that it is elected as the Root Bridge.

### SW1 Configuration

![SW1 Configuration](screenshots/03%20-%20switch%201%20config.png)

### SW2 Configuration

![SW2 Configuration](screenshots/04%20-%20switch%202%20config.png)

### SW3 Configuration

![SW3 Configuration](screenshots/05%20-%20switch%203%20config.png)

### SW4 Configuration

![SW4 Configuration](screenshots/06%20-%20switch%204%20config.png)

---

## 5. Root Bridge Verification

The Root Bridge is identified using the following command:

```cisco
show spanning-tree vlan 1
```

SW1 is configured with a lower bridge priority, making it the preferred Root Bridge during the election process.

### SW1 Root Bridge Verification

![SW1 Verification](screenshots/07%20-%20switch1%20confirm.png)

### SW2 Root Bridge Verification

![SW2 Verification](screenshots/08%20-%20switch2%20confirm.png)

### SW3 Root Bridge Verification

![SW3 Verification](screenshots/09%20-%20switch3%20confirm.png)

### SW4 Root Bridge Verification

![SW4 Verification](screenshots/10%20-%20switch4%20confirm.png)

---

## 6. RSTP Concepts Demonstrated

### Root Bridge

The Root Bridge is the central reference point used by Spanning Tree Protocol to determine the best paths throughout the Layer 2 network.

SW1 is configured as the Root Bridge using a lower bridge priority.

### Port Roles

RSTP assigns port roles based on the topology and the path to the Root Bridge.

- **Root Port:** The port providing the best path towards the Root Bridge.
- **Designated Port:** The port selected to forward traffic on a segment.
- **Alternate Port:** A backup path towards the Root Bridge that is not currently forwarding.
- **Edge Port:** A port connected to an end device, such as a PC.

### Link Types

- **Edge:** Typically connects a switch to an end device.
- **Point-to-point:** Typically connects two switches through a full-duplex link.

### Loop Prevention

The redundant switch connections provide alternative paths. RSTP prevents Layer 2 loops by selecting a loop-free forwarding topology and maintaining redundant paths in alternate states where necessary.

---

## 7. Verification Commands

The following commands are used to verify RSTP operation:

```cisco
show spanning-tree vlan 1
show spanning-tree summary
show spanning-tree detail
show interfaces status
show vlan brief
```

---

## 8. Conclusion

This lab demonstrates the configuration and verification of Rapid Spanning Tree Protocol in a redundant switching topology.

The four-switch ring topology provides redundant Layer 2 paths. RSTP determines the Root Bridge, assigns port roles, identifies link types and prevents switching loops while maintaining redundancy.

SW1 is configured as the Root Bridge, and the spanning tree configuration is verified using Cisco IOS commands.
