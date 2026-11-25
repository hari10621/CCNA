
@'
# RIP v2 Routing Configuration – Four Router Topology

## 1. Objective

The objective of this practical is to configure and verify RIP Version 2 (RIPv2) dynamic routing between four routers using Cisco Packet Tracer.

The topology contains four routers (R1, R2, R3 and R4), one PC connected to R4, and an ISP connection connected to R1.

## 2. Network Architecture

The network uses a square topology:

- R1 connects to R2 and R3.
- R2 connects to R4.
- R3 connects to R4.
- R4 connects to PC0.
- R1 connects to the ISP router.

### Network Topology

![Network Architecture](screenshots/01%20-%20ARCHITECTURE.png)

## 3. IP Addressing Scheme

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R1 | G0/0 | 10.0.12.1 | 255.255.255.252 |
| R1 | G0/1 | 10.0.13.1 | 255.255.255.252 |
| R1 | G0/2 | 203.0.113.2 | 255.255.255.252 |
| R2 | G0/0 | 10.0.12.2 | 255.255.255.252 |
| R2 | G0/1 | 10.0.24.1 | 255.255.255.252 |
| R3 | G0/0 | 10.0.13.2 | 255.255.255.252 |
| R3 | G0/1 | 10.0.34.2 | 255.255.255.252 |
| R4 | G0/0 | 10.0.24.2 | 255.255.255.252 |
| R4 | G0/1 | 10.0.34.1 | 255.255.255.252 |
| R4 | G0/2 | 192.168.40.1 | 255.255.255.0 |
| PC0 | FastEthernet0 | 192.168.40.10 | 255.255.255.0 |
| ISP | G0/0 | 203.0.113.1 | 255.255.255.252 |

## 4. R1 Configuration

R1 is connected to R2, R3 and the ISP router.

### R1 Interface Configuration

![R1 Configuration](screenshots/02%20-%20R1%20CONFIG.png)

### R1 RIP Configuration

![R1 RIP Configuration](screenshots/03%20-%20R1%20RIP.png)

RIP configuration:

```text
router rip
version 2
no auto-summary
network 10.0.0.0
default-information originate
```

For default route advertisement, R1 must also have a default route configured:

```text
ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

## 5. R2 Configuration

R2 connects R1 and R4.

### R2 Interface Configuration

![R2 Configuration](screenshots/04%20-%20R2%20CONFIG.png)

### R2 RIP Configuration

![R2 RIP Configuration](screenshots/05%20-%20R2%20RIP.png)

RIP configuration:

```text
router rip
version 2
no auto-summary
network 10.0.0.0
```

## 6. R3 Configuration

R3 connects R1 and R4.

### R3 Interface Configuration

![R3 Configuration](screenshots/06%20-%20R3%20CONFIG.png)

### R3 RIP Configuration

![R3 RIP Configuration](screenshots/07%20%20-%20R3%20RIP.png)

RIP configuration:

```text
router rip
version 2
no auto-summary
network 10.0.0.0
```

## 7. R4 Configuration

R4 connects R2, R3 and PC0.

### R4 Interface Configuration

![R4 Configuration](screenshots/08%20-%20R4%20CONFIG.png)

### R4 RIP Configuration

![R4 RIP Configuration](screenshots/09%20-%20R4%20RIP.png)

RIP configuration:

```text
router rip
version 2
no auto-summary
network 10.0.0.0
network 192.168.40.0
```

## 8. RIP Protocol Verification

The routing table on R1 can be checked using:

```text
show ip route
```

The RIP protocol information can be checked using:

```text
show ip protocols
```

### R1 Protocol Verification

![R1 Protocol Verification](screenshots/10%20-%20R1%20PROTOCOL.png)

## 9. Useful Verification Commands

| Command | Purpose |
|---|---|
| show ip interface brief | Displays interface IP addresses and status |
| show ip route | Displays the routing table |
| show ip protocols | Displays routing protocol information |
| show running-config | Displays the active router configuration |
| show ip route rip | Displays routes learned through RIP |
| ping | Tests connectivity between devices |
| tracert | Displays the path taken by packets from a PC |

## 10. Working Principle

RIP Version 2 is a distance-vector dynamic routing protocol. Routers exchange routing information with neighboring routers and use hop count to determine the best path.

RIPv2 supports classless routing and carries subnet mask information in routing updates. Its maximum usable hop count is 15; a metric of 16 represents an unreachable network.

## 11. Conclusion

In this practical, four routers were connected using a square topology and configured with RIP Version 2. The routers exchange routing information dynamically, allowing the network behind R4 to be learned by the other routers.

The configuration and routing protocol were documented using Cisco Packet Tracer screenshots.
'@ | Set-Content -Path ".\README.md" -Encoding UTF8
