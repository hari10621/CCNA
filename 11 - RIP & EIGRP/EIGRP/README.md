# CCNA Lab 11 – EIGRP Dynamic Routing Configuration

## 1. Project Overview

This project demonstrates the configuration and implementation of **Enhanced Interior Gateway Routing Protocol (EIGRP)** using Cisco Packet Tracer.

The lab consists of four Cisco 2911 routers connected in a square topology, with one end device (PC0) connected to Router R4.

EIGRP is configured on all four routers to establish dynamic routing and enable communication between different networks.

The primary objective is to understand EIGRP configuration, neighbor relationships, dynamic route advertisement, routing table updates, and end-to-end network connectivity.

## 2. Objectives

- Understand the fundamentals of EIGRP dynamic routing.
- Configure IPv4 addresses on Cisco routers.
- Establish EIGRP routing using Autonomous System (AS) 100.
- Establish EIGRP neighbor relationships between routers.
- Exchange routing information dynamically.
- Verify EIGRP-learned routes using routing tables.
- Understand the EIGRP DUAL algorithm.
- Configure passive interfaces.
- Verify network connectivity between routers and end devices.

## 3. Network Architecture

The network consists of four Cisco 2911 routers arranged in a square topology.

### Network Topology

- R1 connects to R2 and R3.
- R2 connects to R1 and R4.
- R3 connects to R1 and R4.
- R4 connects to R2 and R3.
- PC0 is connected to R4 through GigabitEthernet 0/2.

### Architecture Diagram

![EIGRP Network Architecture](./screenshots/01%20-%20ARCHITECTURE.png)

## 4. Hardware and Software Requirements

| Component | Specification |
|---|---|
| Network Simulator | Cisco Packet Tracer |
| Router Model | Cisco 2911 |
| Number of Routers | 4 |
| End Device | 1 PC |
| Routing Protocol | EIGRP |
| EIGRP AS Number | 100 |
| IP Version | IPv4 |
| Routing Algorithm | DUAL |

## 5. Network Addressing Scheme

The following IP addressing scheme is implemented in the lab.

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R1 | G0/0 | 10.0.12.1 | 255.255.255.252 |
| R1 | G0/1 | 10.0.13.1 | 255.255.255.252 |
| R2 | G0/0 | 10.0.12.2 | 255.255.255.252 |
| R2 | G0/1 | 10.0.24.1 | 255.255.255.252 |
| R3 | G0/0 | 10.0.13.2 | 255.255.255.252 |
| R3 | G0/1 | 10.0.34.2 | 255.255.255.252 |
| R4 | G0/0 | 10.0.24.2 | 255.255.255.252 |
| R4 | G0/1 | 10.0.34.1 | 255.255.255.252 |
| R4 | G0/2 | 192.168.40.1 | 255.255.255.0 |
| PC0 | Fa0 | 192.168.40.10 | 255.255.255.0 |

**PC0 Default Gateway:** `192.168.40.1`

## 6. Router Configuration Evidence

### 6.1 Router R1 Configuration

R1 is configured with two GigabitEthernet interfaces to communicate with R2 and R3.

The EIGRP routing protocol is enabled with AS number 100 to advertise the connected networks.

**R1 Interface Configuration**

![R1 Configuration](./screenshots/02%20-%20R1%20CONFIG.png)

**R1 EIGRP Configuration**

![R1 EIGRP Configuration](./screenshots/03%20-%20R1%20EIGRP.png)

### 6.2 Router R2 Configuration

R2 connects R1 and R4. EIGRP is configured to advertise the networks connected to both interfaces.

**R2 Interface Configuration**

![R2 Configuration](./screenshots/04%20-%20R2%20CONFIG.png)

**R2 EIGRP Configuration**

![R2 EIGRP Configuration](./screenshots/05%20-%20R2%20EIGRP.png)

### 6.3 Router R3 Configuration

R3 connects R1 and R4, providing an alternative routing path within the topology.

EIGRP dynamically exchanges routing information with its neighboring routers.

**R3 Interface Configuration**

![R3 Configuration](./screenshots/06%20-%20R3%20CONFIG.png)

**R3 EIGRP Configuration**

![R3 EIGRP Configuration](./screenshots/07%20-%20R3%20EIGRP.png)

### 6.4 Router R4 Configuration

R4 connects R2, R3, and the end-device PC0.

It advertises the LAN network `192.168.40.0/24` through EIGRP.

The PC-facing interface is configured as a passive interface. This prevents EIGRP neighbor formation on the PC-facing network while allowing the LAN network to be advertised.

**R4 Interface Configuration**

![R4 Configuration](./screenshots/08%20-%20R4%20CONFIG.png)

**R4 EIGRP Configuration**

![R4 EIGRP Configuration](./screenshots/09%20-%20R4%20EIGRP.png)

## 7. EIGRP Configuration Commands

The following commands are used to configure EIGRP on the routers.

### 7.1 Enable EIGRP

```cisco
enable
configure terminal
router eigrp 100
no auto-summary
```

### 7.2 Advertise Networks

Example configuration for R1:

```cisco
network 10.0.12.0 0.0.0.3
network 10.0.13.0 0.0.0.3
```

### 7.3 Passive Interface Configuration

Example configuration for R4:

```cisco
passive-interface gigabitEthernet 0/2
```

### 7.4 Save Configuration

```cisco
end
write memory
```

## 8. EIGRP Verification Commands

The following commands can be used to verify EIGRP operation and routing information.

| Command | Description |
|---|---|
| `show ip interface brief` | Displays router interface status and IP addresses. |
| `show ip eigrp neighbors` | Displays discovered EIGRP neighbors. |
| `show ip route` | Displays connected and dynamically learned routes. |
| `show ip protocols` | Displays active routing protocol information. |
| `show ip eigrp topology` | Displays the EIGRP topology table. |
| `show running-config` | Displays the current router configuration. |

### Important EIGRP Route Codes

| Route Code | Meaning |
|---|---|
| C | Connected Route |
| L | Local Route |
| D | EIGRP Route |
| D EX | EIGRP External Route |

## 9. Understanding EIGRP

EIGRP is an advanced distance-vector routing protocol that uses the **Diffusing Update Algorithm (DUAL)** to calculate loop-free routes.

Important concepts demonstrated in this lab:

### Neighbor Discovery

EIGRP routers discover neighboring routers using Hello packets. Routers must share compatible EIGRP parameters and the same autonomous system number to establish adjacency.

### Autonomous System (AS)

An autonomous system number identifies the EIGRP routing process. In this lab, AS number 100 is configured on all four routers.

### DUAL Algorithm

The Diffusing Update Algorithm calculates loop-free paths and selects the best available routes.

### Successor

The successor is the best route selected by EIGRP for reaching a destination network.

### Feasible Successor

A feasible successor is a qualifying backup route that satisfies the EIGRP feasibility condition.

### Metric Calculation

EIGRP uses a composite metric. By default, bandwidth and delay are the primary metric components.

### Dynamic Route Advertisement

Routers exchange routing information dynamically, allowing remote networks to become reachable without manually configuring individual static routes.

## 10. Connectivity Testing

PC0 is configured with the following IPv4 settings:

| Parameter | Value |
|---|---|
| IP Address | 192.168.40.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.40.1 |

The following commands can be executed from PC0 to test connectivity.

```bash
ping 192.168.40.1
ping 10.0.24.2
ping 10.0.34.2
ping 10.0.12.2
ping 10.0.13.2
```

These tests help verify communication with the directly connected gateway and remote router interfaces.

