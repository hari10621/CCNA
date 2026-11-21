@'
# EtherChannel Configuration – PAgP (Cisco Packet Tracer)

## 1. Objective

Configure and verify EtherChannel using PAgP (Port Aggregation Protocol) between two Cisco switches in Cisco Packet Tracer.

### Objectives

- Understand EtherChannel.
- Configure PAgP between two switches.
- Combine two physical links into a single logical Port-channel.
- Verify EtherChannel formation.
- Understand PAgP negotiation.
- Verify the configured EtherChannel.

---

## 2. Network Architecture

The topology consists of two Cisco switches connected through two physical links. These links are bundled into a single logical EtherChannel using PAgP. PCs are connected to both switches to verify network connectivity.

### Devices Used

| Device | Device Name | Device Type |
|---|---|---|
| Switch 1 | SW1 | Cisco 2960 |
| Switch 2 | SW2 | Cisco 2960 |
| PC 1 | PC1 | PC |
| PC 2 | PC2 | PC |

### Cable Connections

| Source Device | Source Port | Destination Device | Destination Port |
|---|---|---|---|
| PC1 | FastEthernet0 | SW1 | FastEthernet0/3 |
| SW1 | FastEthernet0/1 | SW2 | FastEthernet0/1 |
| SW1 | FastEthernet0/2 | SW2 | FastEthernet0/2 |
| PC2 | FastEthernet0 | SW2 | FastEthernet0/3 |

The two physical links between SW1 and SW2 are combined into Port-channel 1.

### Architecture Screenshot

![Network Architecture](screenshots/01%20-%20ARCHITECTURE.png)

**Screenshot 01 – Architecture**

This screenshot shows:

- PC1 connected to SW1.
- PC2 connected to SW2.
- Two physical connections between SW1 and SW2.
- The topology used for PAgP EtherChannel.

---

## 3. IP Address Configuration

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

### Configuration Commands

```cisco
enable
configure terminal
hostname SW1

interface range fastethernet0/1 - 2
switchport mode trunk
channel-group 1 mode desirable
exit

interface port-channel 1
switchport mode trunk
exit

end
write memory