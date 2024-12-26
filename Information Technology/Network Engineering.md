# Network Engineering Cheat Sheet

## OSI Model Reference

### Layer 7 - Application
- Protocols: HTTP, FTP, SMTP, DNS, DHCP
- Function: End-user services
- Troubleshooting: Application logs, Wireshark

### Layer 6 - Presentation
- Data formatting and encryption
- SSL/TLS
- JPEG, GIF, MPEG encoding

### Layer 5 - Session
- Session establishment and management
- NetBIOS, RPC
- Connection management

### Layer 4 - Transport
- TCP (Connection-oriented)
  - Ports: 0-65535
  - Three-way handshake: SYN, SYN-ACK, ACK
  - Window size and flow control
- UDP (Connectionless)
  - Stateless communication
  - No guarantee of delivery
  - Used for streaming, DNS

### Layer 3 - Network
- IP addressing and routing
- ICMP
- Router functions

### Layer 2 - Data Link
- MAC addresses
- Switching
- Frame transmission
- Error detection

### Layer 1 - Physical
- Cables, fiber, wireless
- Bits transmission
- Physical topology

## IP Addressing

### IPv4 Classes
- Class A: 1.0.0.0 to 126.255.255.255 (/8)
- Class B: 128.0.0.0 to 191.255.255.255 (/16)
- Class C: 192.0.0.0 to 223.255.255.255 (/24)
- Class D: 224.0.0.0 to 239.255.255.255 (Multicast)
- Class E: 240.0.0.0 to 255.255.255.255 (Reserved)

### Subnet Mask Quick Reference
```
/8  = 255.0.0.0
/16 = 255.255.0.0
/24 = 255.255.255.0
/25 = 255.255.255.128
/26 = 255.255.255.192
/27 = 255.255.255.224
/28 = 255.255.255.240
/29 = 255.255.255.248
/30 = 255.255.255.252
```

### IPv6 Basics
- 128-bit address
- 8 groups of 4 hexadecimal digits
- Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- Shorthand: Remove leading zeros
- Double colon (::) to represent multiple zero groups

## Common Protocols and Ports

### Well-Known Ports
```
TCP 20,21 - FTP
TCP 22 - SSH
TCP 23 - Telnet
TCP 25 - SMTP
TCP/UDP 53 - DNS
TCP 80 - HTTP
TCP 443 - HTTPS
UDP 67,68 - DHCP
TCP 110 - POP3
TCP 143 - IMAP
TCP 3389 - RDP
```

## Routing Protocols

### Interior Gateway Protocols (IGP)
- OSPF
  - Link-state protocol
  - Areas and hierarchy
  - Fast convergence
  - Dijkstra algorithm

- EIGRP
  - Advanced distance vector
  - DUAL algorithm
  - Cisco proprietary
  - Fast convergence

- RIP
  - Distance vector
  - Max 15 hops
  - Bellman-Ford algorithm
  - Slow convergence

### Exterior Gateway Protocols (EGP)
- BGP
  - Path vector protocol
  - AS path attribute
  - Complex path selection
  - Internet routing standard

## Switching Concepts

### VLANs
- Logical network segmentation
- 802.1Q tagging
- Native VLAN
- Voice VLAN
- Management VLAN

### Spanning Tree Protocol
- 802.1D (Original STP)
- 802.1w (RSTP)
- 802.1s (MSTP)
- Port states and roles
- Root bridge election
- BPDUs

### Port Security
- MAC address learning
- Sticky MAC
- Violation modes
- Maximum MAC addresses
- Aging time

## Network Security

### Access Control Lists (ACLs)
```
Standard ACL: 1-99, 1300-1999
Extended ACL: 100-199, 2000-2699
```

### AAA Framework
- Authentication
- Authorization
- Accounting
- RADIUS/TACACS+

### VPN Technologies
- IPSec
- SSL/TLS
- DMVPN
- GRE tunnels
- L2TP/PPTP

## Network Services

### DHCP
- DORA process
  - Discover
  - Offer
  - Request
  - Acknowledge
- Options and parameters
- DHCP relay

### DNS
- Record types
  - A (IPv4)
  - AAAA (IPv6)
  - MX (Mail)
  - CNAME (Alias)
  - PTR (Reverse)
  - NS (Nameserver)
- Hierarchy
- Zone transfers

## Troubleshooting Commands

### Basic Commands
```bash
ping
traceroute/tracert
nslookup/dig
ipconfig/ifconfig
netstat
route
arp
nmap
tcpdump
```

### Cisco IOS Commands
```
show running-config
show interfaces
show ip route
show cdp neighbors
show spanning-tree
show vlan
show ip protocols
debug ip routing
```

## Network Design

### Three-Tier Architecture
- Core Layer
  - High availability
  - Fast switching
  - Minimal services

- Distribution Layer
  - Route aggregation
  - Policy enforcement
  - QoS implementation

- Access Layer
  - Port security
  - QoS trust
  - User connectivity

### High Availability
- HSRP/VRRP/GLBP
- Stackwise/VSS
- NSF/SSO
- Redundant links
- Load balancing

## Quality of Service (QoS)

### Classification Methods
- CoS (Layer 2)
- DSCP (Layer 3)
- NBAR
- ACL-based
- Interface-based

### QoS Models
- Best Effort
- IntServ
- DiffServ
- Custom queuing
- Priority queuing

## Network Management

### SNMP
- SNMPv1, v2c, v3
- MIBs and OIDs
- Traps and informs
- Community strings

### Syslog
- Severity levels (0-7)
- Facility codes
- Local buffering
- Remote logging

### NetFlow
- Flow collection
- Analysis
- Version 5/9
- IPFIX

## Wireless Networks

### 802.11 Standards
```
802.11a - 5 GHz, 54 Mbps
802.11b - 2.4 GHz, 11 Mbps
802.11g - 2.4 GHz, 54 Mbps
802.11n - 2.4/5 GHz, 600 Mbps
802.11ac - 5 GHz, 3.46 Gbps
802.11ax (Wi-Fi 6) - 2.4/5/6 GHz, 9.6 Gbps
```

### Security Protocols
- WEP (Obsolete)
- WPA
- WPA2
- WPA3
- Enterprise vs Personal

## Performance Metrics

### Network Metrics
- Throughput
- Latency
- Jitter
- Packet loss
- Utilization
- Error rates

### Bandwidth Calculation
- Overhead consideration
- Protocol efficiency
- Application requirements
- Peak vs average usage

## Documentation

### Network Diagrams
- Physical topology
- Logical topology
- IP addressing scheme
- Cable documentation
- Rack layouts

### Change Management
- Change requests
- Impact analysis
- Rollback plans
- Testing procedures
- Implementation schedules
