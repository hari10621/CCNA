# 

# \# CCNA Lab – Single Router, Three LANs

# 

# \## 1. Project Overview

# 

# This project demonstrates the configuration of three separate Local Area Networks (LANs) using a single Cisco router in Cisco Packet Tracer.

# 

# Each LAN contains one switch and two PCs. The router provides communication between the three different networks.

# 

# \## 2. Network Topology

# 

# !\[Network Topology](Screenshots/01-Network-Topology.png)

# 

# \### Devices Used

# 

# \- 1 × Cisco 2911 Router (R1)

# \- 3 × Cisco 2960 Switches (SW1, SW2, SW3)

# \- 6 × PCs

# \- Copper Straight-Through Cables

# \- Cisco Packet Tracer

# 

# \## 3. IP Addressing Table

# 

# | LAN | Switch | Router Interface | Gateway | Network |

# |---|---|---|---|---|

# | Green LAN | SW1 | G0/0 | 192.168.10.1 | 192.168.10.0/24 |

# | Blue LAN | SW2 | G0/1 | 192.168.20.1 | 192.168.20.0/24 |

# | Orange LAN | SW3 | G0/2 | 192.168.30.1 | 192.168.30.0/24 |

# 

# \### PC IP Allocation

# 

# | PC | LAN | IP Address | Subnet Mask | Default Gateway |

# |---|---|---|---|---|

# | PC0 | Green | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 |

# | PC1 | Green | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |

# | PC4 | Blue | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 |

# | PC5 | Blue | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |

# | PC2 | Orange | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |

# | PC3 | Orange | 192.168.30.3 | 255.255.255.0 | 192.168.30.1 |

# 

# \## 4. Router Configuration

# 

# \### Initial Router Interface Status

# 

# !\[Initial Router Status](Screenshots/02-Initial-Router-Interface-Status.png)

# 

# \### Configure Router G0/0 – Green LAN

# 

# ```cisco

# enable

# configure terminal

# hostname R1

# 

# interface gigabitEthernet 0/0

# description GREEN\_LAN\_SW1

# ip address 192.168.10.1 255.255.255.0

# no shutdown

# exit

# ```

# 

# !\[G0/0 Configuration](Screenshots/03-Router-G0-0-Configuration.png)

# 

# \### Configure Router G0/1 – Blue LAN

# 

# ```cisco

# interface gigabitEthernet 0/1

# description BLUE\_LAN\_SW2

# ip address 192.168.20.1 255.255.255.0

# no shutdown

# exit

# ```

# 

# !\[G0/1 Configuration](Screenshots/04-Router-G0-1-Configuration.png)

# 

# \### Configure Router G0/2 – Orange LAN

# 

# ```cisco

# interface gigabitEthernet 0/2

# description ORANGE\_LAN\_SW3

# ip address 192.168.30.1 255.255.255.0

# no shutdown

# exit

# ```

# 

# !\[G0/2 Configuration](Screenshots/05-Router-G0-2-Configuration.png)

# 

# \### Save Configuration

# 

# ```cisco

# end

# copy running-config startup-config

# ```

# 

# \## 5. Router Interface Verification

# 

# Command used:

# 

# ```cisco

# show ip interface brief

# ```

# 

# Expected interface configuration:

# 

# | Interface | IP Address | Status | Protocol |

# |---|---|---|---|

# | G0/0 | 192.168.10.1 | up | up |

# | G0/1 | 192.168.20.1 | up | up |

# | G0/2 | 192.168.30.1 | up | up |

# 

# !\[Router Interface Verification](Screenshots/06-Router-Interface-Verification.png)

# 

# \## 6. PC IP Configuration

# 

# All six PCs are configured with static IPv4 addresses.

# 

# !\[PC IP Configuration](Screenshots/07-PC-IP-Configuration.png)

# 

# \## 7. Connectivity Testing

# 

# Ping commands used:

# 

# \### Same LAN Communication

# 

# ```cmd

# ping 192.168.10.2

# ```

# 

# PC0 to PC1.

# 

# Result: Successful – 4 packets received, 0% packet loss.

# 

# \### Green LAN to Blue LAN

# 

# ```cmd

# ping 192.168.20.2

# ```

# 

# Result: Failed in the captured test.

# 

# \### Green LAN to Orange LAN

# 

# ```cmd

# ping 192.168.30.2

# ```

# 

# Result: Failed in the captured test.

# 

# !\[Ping Test Results](Screenshots/08-Ping-Test-Results.png)

# 

# \*\*Note:\*\* The captured PC IP configuration shows default gateways as `0.0.0.0`. These must be corrected to the gateway addresses in the IP allocation table before successful inter-LAN communication can be verified.

# 

# \## 8. Skills Demonstrated

# 

# \- Cisco IOS CLI Configuration

# \- Router Interface Configuration

# \- IPv4 Addressing

# \- Subnet Mask Configuration

# \- LAN Segmentation

# \- Default Gateway Configuration

# \- Network Connectivity Testing

# \- ICMP Ping

# \- Basic Network Troubleshooting

# 

# 



