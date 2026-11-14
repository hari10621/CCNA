# VLAN Trunking Protocol (VTP) and Trunking Lab

**Lab platform:** Cisco Packet Tracer  
**Main topic:** VTP Server, Client and Transparent modes with 802.1Q trunk links  
**Devices:** 4 × Cisco 2960-24TT switches

## 1. Objective

Build a four-switch network to configure and examine VTP Server, Client and Transparent modes. Configure trunk links between the switches, create VLANs on the VTP Server, and verify how VLAN information is distributed to VTP Clients through the Transparent switch.

The lab also provides a basis for testing how a VTP domain mismatch affects VLAN synchronization.

## 2. Network topology

The switches are connected in a linear topology:

```text
SW1 (VTP Server) ---- SW2 (VTP Client) ---- SW3 (VTP Transparent) ---- SW4 (VTP Client)
```

![Four-switch VTP topology](Screenshots/01-VTP-Network-Architecture.png)

## 3. Device roles and fixed port connections

| Switch | Model | Hostname | VTP mode |
|---|---|---|---|
| Switch 1 | Cisco 2960-24TT | SW1 | Server |
| Switch 2 | Cisco 2960-24TT | SW2 | Client |
| Switch 3 | Cisco 2960-24TT | SW3 | Transparent |
| Switch 4 | Cisco 2960-24TT | SW4 | Client |

### Inter-switch cabling

| Link | First switch/interface | Second switch/interface |
|---|---|---|
| SW1–SW2 | SW1 Fa0/1 | SW2 Fa0/1 |
| SW2–SW3 | SW2 Fa0/2 | SW3 Fa0/1 |
| SW3–SW4 | SW3 Fa0/2 | SW4 Fa0/1 |

Use Copper Cross-Over cables (or Packet Tracer automatic connections) for the switch-to-switch links. The interface assignments above are the fixed design for this lab.

## 4. VTP and VLAN parameters

| Parameter | Value |
|---|---|
| VTP domain shown in the submitted configurations | `CCNA` |
| VTP version | 2 |
| VTP password | Not configured |
| VLAN 10 | ADMIN |
| VLAN 20 | HR |
| VLAN 30 | IT |

> **Configuration note:** The actual CLI screenshots use the VTP domain `CCNA`. Keep this exact domain consistently on all four switches. Do not change it to `CCNA-LAB` unless you intentionally reconfigure every switch.

## 5. Switch configuration

The following configuration blocks document the intended final configuration. They follow the fixed device names, roles and port assignments.

### SW1 – VTP Server

```cisco
enable
configure terminal
hostname SW1
vtp domain CCNA
vtp version 2
vtp mode server

interface fastEthernet 0/1
 switchport mode trunk
 no shutdown
exit

vlan 10
 name ADMIN
exit
vlan 20
 name HR
exit
vlan 30
 name IT
exit

end
write memory
```

**Evidence**

![SW1 server configuration](Screenshots/02-SW1-Server-Configuration.png)

![SW1 VLAN creation and save](Screenshots/03-SW1-VLAN-Creation-and-Save.png)

![SW1 VTP status](Screenshots/04-SW1-VTP-Status.png)

### SW2 – VTP Client

```cisco
enable
configure terminal
hostname SW2
vtp domain CCNA
vtp version 2
vtp mode client

interface fastEthernet 0/1
 switchport mode trunk
 no shutdown
exit

interface fastEthernet 0/2
 switchport mode trunk
 no shutdown
exit

end
write memory
```

**Evidence**

![SW2 client configuration](Screenshots/05-SW2-Client-Configuration.png)

![SW2 VTP status](Screenshots/06-SW2-VTP-Status.png)

> **Verification note:** The supplied SW2 configuration screenshot shows Fa0/1 configured as a trunk. It does not show the Fa0/2 trunk configuration. Run the Fa0/2 commands above and capture `show interfaces trunk` to document both SW2 links.

### SW3 – VTP Transparent

```cisco
enable
configure terminal
hostname SW3
vtp domain CCNA
vtp version 2
vtp mode transparent

interface fastEthernet 0/1
 switchport mode trunk
 no shutdown
exit

interface fastEthernet 0/2
 switchport mode trunk
 no shutdown
exit

end
write memory
```

**Evidence**

![SW3 transparent configuration](Screenshots/07-SW3-Transparent-Configuration.png)

![SW3 VTP status](Screenshots/08-SW3-VTP-Status.png)

### SW4 – VTP Client

```cisco
enable
configure terminal
hostname SW4
vtp domain CCNA
vtp version 2
vtp mode client

interface fastEthernet 0/1
 switchport mode trunk
 no shutdown
exit

end
write memory
```

**Evidence**

![SW4 client configuration](Screenshots/09-SW4-Client-Configuration.png)

![SW4 VTP status](Screenshots/10-SW4-VTP-Status.png)

## 6. Verification commands

Run these commands on the relevant switches and save the outputs as evidence.

| Command | Purpose |
|---|---|
| `show vtp status` | Check VTP domain, version, operating mode and revision |
| `show vlan brief` | Inspect the local VLAN database |
| `show interfaces trunk` | Verify operational trunk interfaces |
| `show running-config` | Review the switch configuration |
| `show interfaces fa0/1 switchport` | Inspect the Fa0/1 switchport mode |
| `show interfaces fa0/2 switchport` | Inspect the Fa0/2 switchport mode where used |

### Expected VTP roles

| Switch | VTP domain | Version | Operating mode |
|---|---|---:|---|
| SW1 | CCNA | 2 | Server |
| SW2 | CCNA | 2 | Client |
| SW3 | CCNA | 2 | Transparent |
| SW4 | CCNA | 2 | Client |

### Expected VLAN behavior

- SW1 is the VTP Server and is configured with VLANs 10, 20 and 30.
- SW2 is a VTP Client and should learn the server's VLAN information.
- SW3 is Transparent: it maintains its own VLAN database and does not synchronize that database with the server. In VTP Version 2, it forwards received VTP advertisements over trunk links.
- SW4 is a VTP Client and should be able to receive the VTP advertisements forwarded by SW3, provided the domain and trunk path are correct.

**Evidence limitation:** The screenshots currently supplied show the VTP status and configuration commands. They do not include `show vlan brief` or `show interfaces trunk` outputs for every switch. Capture those outputs before claiming that every VLAN and trunk has been fully verified.

## 7. Additional evidence to capture

- `11-SW1-VLAN-Database.png` — SW1 `show vlan brief`.
- `12-SW1-Trunk-Status.png` — SW1 `show interfaces trunk`.
- `13-SW2-VLAN-Database.png` — SW2 `show vlan brief`.
- `14-SW2-Trunk-Status.png` — SW2 `show interfaces trunk`, confirming Fa0/1 and Fa0/2.
- `15-SW3-VLAN-Database.png` — SW3 `show vlan brief`.
- `16-SW3-Trunk-Status.png` — SW3 `show interfaces trunk`, confirming Fa0/1 and Fa0/2.
- `17-SW4-VLAN-Database.png` — SW4 `show vlan brief`.
- `18-SW4-Trunk-Status.png` — SW4 `show interfaces trunk`.

## 8. Learning outcomes

- Configured VTP Server, Client and Transparent modes.
- Configured trunk links between Cisco switches.
- Created VLANs on a VTP Server.
- Reviewed VTP domain, version, operating mode and configuration revision.
- Learned that Transparent mode maintains its own VLAN database while forwarding VTP advertisements in VTP Version 2.
- Practised verifying VLAN databases and trunk interfaces.

## 9. Packet Tracer project

Save the completed Packet Tracer project in this folder as:

`VTP-Trunk-Lab.pkt`

The `.pkt` project must be saved from Cisco Packet Tracer and added to the repository separately.
