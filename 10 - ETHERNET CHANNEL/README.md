<<<<<<< HEAD
@'
=======
>>>>>>> a68384e (update reamdme.md)
# EtherChannel Configuration – PAgP (Cisco Packet Tracer)

## 1. Objective

Configure and verify EtherChannel using PAgP (Port Aggregation Protocol) between two Cisco switches in Cisco Packet Tracer.

### Objectives

<<<<<<< HEAD
- Understand EtherChannel.
- Configure PAgP between two switches.
- Combine two physical links into a single logical Port-channel.
- Verify EtherChannel formation.
- Understand PAgP negotiation.
- Verify the configured EtherChannel.
=======
- Understand EtherChannel and its purpose.
- Configure PAgP between two switches.
- Combine two physical interfaces into a single logical interface.
- Configure PAgP Desirable and Auto modes.
- Verify EtherChannel formation on both switches.
>>>>>>> a68384e (update reamdme.md)

---

## 2. Network Architecture

<<<<<<< HEAD
The topology consists of two Cisco switches connected through two physical links. These links are bundled into a single logical EtherChannel using PAgP. PCs are connected to both switches to verify network connectivity.

### Devices Used

| Device | Device Name | Device Type |
|---|---|---|
| Switch 1 | SW1 | Cisco 2960 |
| Switch 2 | SW2 | Cisco 2960 |
| PC 1 | PC1 | PC |
| PC 2 | PC2 | PC |
=======
The network consists of two Cisco 2960 switches connected using two physical Ethernet links. These links are combined into a single logical EtherChannel using PAgP. Two PCs are connected to the switches.

### Devices Used

| Device | Name | Device Type |
|---|---|---|
| Switch 1 | SW1 | Cisco 2960 |
| Switch 2 | SW2 | Cisco 2960 |
| PC 1 | PC1 | PC-PT |
| PC 2 | PC2 | PC-PT |
>>>>>>> a68384e (update reamdme.md)

### Cable Connections

| Source Device | Source Port | Destination Device | Destination Port |
|---|---|---|---|
| PC1 | FastEthernet0 | SW1 | FastEthernet0/3 |
| SW1 | FastEthernet0/1 | SW2 | FastEthernet0/1 |
| SW1 | FastEthernet0/2 | SW2 | FastEthernet0/2 |
| PC2 | FastEthernet0 | SW2 | FastEthernet0/3 |

<<<<<<< HEAD
The two physical links between SW1 and SW2 are combined into Port-channel 1.

### Architecture Screenshot

![Network Architecture](screenshots/01%20-%20ARCHITECTURE.png)

**Screenshot 01 – Architecture**

This screenshot shows:

- PC1 connected to SW1.
- PC2 connected to SW2.
- Two physical connections between SW1 and SW2.
- The topology used for PAgP EtherChannel.
=======
The two physical links between SW1 and SW2 are combined into a single logical interface, Port-channel 1.

### Network Architecture Screenshot

![Network Architecture](screenshots/01%20-%20ARCHITECTURE.png)

**Screenshot 01 – Network Architecture**

This screenshot shows PC1 connected to SW1, PC2 connected to SW2, and the two physical links connecting both switches.
>>>>>>> a68384e (update reamdme.md)

---

## 3. IP Address Configuration

<<<<<<< HEAD
Both PCs are configured with static IP addresses in the same network.

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| PC1 | FastEthernet0 | 192.168.10.1 | 255.255.255.0 | Not Required |
| PC2 | FastEthernet0 | 192.168.10.2 | 255.255.255.0 | Not Required |

### Configuration Procedure

1. Click PC1.
2. Open Desktop.
3. Select IP Configuration.
4. Select Static.
5. Configure the IP address and subnet mask.
6. Repeat the same procedure for PC2.

### IP Configuration Screenshot

![PC IP Configuration](screenshots/02%20-%20IP%20CONFIG.png)

**Screenshot 02 – IP Configuration**

This screenshot documents the IP address configuration of the end devices used in the EtherChannel connectivity test.

---

## 4. SW1 Configuration

SW1 is configured to initiate PAgP negotiation using the Desirable mode.
=======
Both PCs are configured with static IPv4 addresses in the same subnet.

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| PC1 | FastEthernet0 | 192.168.10.1 | 255.255.255.0 | 0.0.0.0 |
| PC2 | FastEthernet0 | 192.168.10.2 | 255.255.255.0 | 0.0.0.0 |

### Configuration Procedure

1. Open the PC.
2. Navigate to **Desktop**.
3. Open **IP Configuration**.
4. Select **Static**.
5. Enter the IPv4 address and subnet mask for each PC.

### IP Configuration Screenshot

![IP Configuration](screenshots/02%20-%20IP%20CONFIG.png)

**Screenshot 02 – PC IP Configuration**

This screenshot documents the IP configuration of both PCs:

- PC1: `192.168.10.1/24`
- PC2: `192.168.10.2/24`

Both PCs belong to the network `192.168.10.0/24`.

---

## 4. SW1 Configuration – PAgP Desirable

SW1 is configured using PAgP Desirable mode to actively initiate EtherChannel negotiation.
>>>>>>> a68384e (update reamdme.md)

### Configuration Commands

```cisco
enable
configure terminal
<<<<<<< HEAD
hostname SW1
=======
>>>>>>> a68384e (update reamdme.md)

interface range fastethernet0/1 - 2
switchport mode trunk
channel-group 1 mode desirable
exit

interface port-channel 1
switchport mode trunk
exit

end
<<<<<<< HEAD
write memory
=======
```

### Command Explanation

| Command | Description |
|---|---|
| `enable` | Enters privileged EXEC mode |
| `configure terminal` | Enters global configuration mode |
| `interface range fastethernet0/1 - 2` | Selects Fa0/1 and Fa0/2 |
| `switchport mode trunk` | Configures the selected physical interfaces as trunk ports |
| `channel-group 1 mode desirable` | Initiates PAgP negotiation and assigns the interfaces to EtherChannel group 1 |
| `interface port-channel 1` | Accesses the logical EtherChannel interface |
| `switchport mode trunk` | Configures Port-channel 1 as a trunk |
| `end` | Exits configuration mode |

### SW1 Configuration Screenshot

![SW1 Configuration](screenshots/03%20-%20SW1%20CONFIG.png)

**Screenshot 03 – SW1 Configuration**

This screenshot documents the SW1 configuration, including the interface range, trunk configuration, and PAgP Desirable mode.

The initial suspended messages can occur while PAgP has not yet been enabled on the corresponding remote switch ports.

---

## 5. SW2 Configuration – PAgP Auto

SW2 is configured using PAgP Auto mode to respond to the negotiation initiated by SW1.

### Configuration Commands

```cisco
enable
configure terminal

interface range fastethernet0/1 - 2
switchport mode trunk
channel-group 1 mode auto
exit

interface port-channel 1
switchport mode trunk
exit

end
```

### Command Explanation

| Command | Description |
|---|---|
| `enable` | Enters privileged EXEC mode |
| `configure terminal` | Enters global configuration mode |
| `interface range fastethernet0/1 - 2` | Selects Fa0/1 and Fa0/2 |
| `switchport mode trunk` | Configures the selected physical interfaces as trunk ports |
| `channel-group 1 mode auto` | Enables PAgP Auto mode on EtherChannel group 1 |
| `interface port-channel 1` | Accesses the logical EtherChannel interface |
| `switchport mode trunk` | Configures Port-channel 1 as a trunk |
| `end` | Exits configuration mode |

### SW2 Configuration Screenshot

![SW2 Configuration](screenshots/04%20-%20SW2%20CONFIG.png)

**Screenshot 04 – SW2 Configuration**

This screenshot documents the SW2 configuration, including the interface range, trunk configuration, and PAgP Auto mode.

---

## 6. EtherChannel Verification on SW1

After configuring both switches, EtherChannel status is verified on SW1.

### Verification Command

```cisco
show etherchannel summary
```

### Expected Output

```text
Group  Port-channel  Protocol  Ports
1      Po1(SU)      PAgP      Fa0/1(P) Fa0/2(P)
```

### SW1 Verification Screenshot

![SW1 EtherChannel Verification](screenshots/05%20-%20PAgp%20sw1.png)

**Screenshot 05 – SW1 EtherChannel Verification**

This screenshot shows the EtherChannel verification output on SW1.

It verifies the group number, logical Port-channel, PAgP protocol, member interfaces, and their bundled status.

---

## 7. EtherChannel Verification on SW2

EtherChannel status is independently verified on SW2.

### Verification Command

```cisco
show etherchannel summary
```

### Expected Output

```text
Group  Port-channel  Protocol  Ports
1      Po1(SU)      PAgP      Fa0/1(P) Fa0/2(P)
```

### SW2 Verification Screenshot

![SW2 EtherChannel Verification](screenshots/06%20-%20PAgp%20sw2.png)

**Screenshot 06 – SW2 EtherChannel Verification**

This screenshot shows the EtherChannel verification output on SW2 and confirms the status of Port-channel 1 and its member interfaces.

---

## 8. Verification Output Analysis

### Output Interpretation

| Symbol | Meaning |
|---|---|
| `S` | Layer 2 EtherChannel |
| `U` | Port-channel is in use |
| `P` | Physical interface is successfully bundled into the Port-channel |

### Verification Result

| Switch | EtherChannel | Protocol | Member Ports | Status |
|---|---|---|---|---|
| SW1 | Po1 | PAgP | Fa0/1(P), Fa0/2(P) | SU |
| SW2 | Po1 | PAgP | Fa0/1(P), Fa0/2(P) | SU |

Both switches display Port-channel 1 in the `SU` state, and both physical interfaces are marked `(P)`, confirming that the EtherChannel is successfully formed.

---

## 9. PAgP Configuration Summary

| Switch | Physical Interfaces | EtherChannel Group | PAgP Mode |
|---|---|---|---|
| SW1 | Fa0/1, Fa0/2 | Group 1 | Desirable |
| SW2 | Fa0/1, Fa0/2 | Group 1 | Auto |

### Logical Interface

| Logical Interface | Protocol | Member Interfaces |
|---|---|---|
| Port-channel 1 | PAgP | Fa0/1, Fa0/2 |

---

## 10. Working Principle

EtherChannel combines multiple physical Ethernet connections into one logical connection between switches.

In this lab:

1. SW1 is configured using PAgP Desirable mode.
2. SW2 is configured using PAgP Auto mode.
3. SW1 actively initiates PAgP negotiation.
4. SW2 responds to the negotiation.
5. Both switches negotiate the formation of EtherChannel group 1.
6. Fa0/1 and Fa0/2 are bundled into Port-channel 1.
7. The logical Port-channel operates as a trunk between the switches.

### PAgP Modes

| Mode | Description |
|---|---|
| Desirable | Actively initiates PAgP negotiation |
| Auto | Passively waits for PAgP negotiation |

Desirable and Auto modes are compatible because Desirable initiates negotiation while Auto responds.

---

## 11. Benefits of EtherChannel

- **Increased aggregate bandwidth:** Combines multiple physical links into a logical link.
- **Redundancy:** Provides alternative physical paths within the bundle.
- **Improved network resiliency:** Helps maintain connectivity if one bundled physical link fails.
- **Simplified management:** Multiple physical links are managed as a single logical interface.
- **Load distribution:** Traffic can be distributed across bundled links according to the switch's hashing algorithm.

---

## 12. Conclusion

PAgP EtherChannel was configured between SW1 and SW2 using two physical Ethernet interfaces.

SW1 was configured with PAgP Desirable mode, while SW2 was configured with PAgP Auto mode. Both physical interfaces were successfully bundled into Port-channel 1.

The EtherChannel configuration was verified independently on both switches using `show etherchannel summary`. The verification output showed Port-channel 1 in the `SU` state and both physical interfaces marked `(P)`.

This lab demonstrates the configuration, negotiation, formation, and verification of PAgP EtherChannel in Cisco Packet Tracer.
>>>>>>> a68384e (update reamdme.md)
