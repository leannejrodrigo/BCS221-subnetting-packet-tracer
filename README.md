# 🌐 CIDR Subnetting & Network Design — Cisco Packet Tracer

> **BCS221 — Computer Networks | Lab Final Assessment (SP25)**  
> Canadian University Dubai

A fully implemented enterprise-style network design using CIDR-based subnetting, multi-router topology, and RIPv2 dynamic routing — simulated in Cisco Packet Tracer.

---

## 📋 Project Overview

This project simulates a real-world network design scenario where a growing organization needs a scalable IP addressing scheme for multiple departments. We designed and implemented 22 subnets across 8 interconnected routers using classless inter-domain routing (CIDR) and verified end-to-end connectivity through ping tests, routing tables, and traceroutes.

---

## 👥 Team Members

| Name | Student ID | Contribution |
|---|---|---|
| Leanne Rodrigo | 20210001983 | Implemented RIPv2 dynamic routing on all routers; router configuration screenshots |
| Aysha Ejaz | 20220002458 | Built the full network topology in Cisco Packet Tracer; assisted with RIP setup; routing table screenshots |
| Jana Mahmoud | 20230002900 | Subnetting calculations using CIDR; ping test screenshots |

---

## 🎯 Objectives

- Design a subnetting strategy using CIDR to divide a Class B IP block into equal-sized subnets
- Configure a multi-router topology in Cisco Packet Tracer (5–8 subnets, 2+ PCs each)
- Implement **RIPv2** as the dynamic routing protocol across all routers
- Verify full connectivity via ping tests, routing tables (`show ip route`), and traceroutes

---

## 🧮 Subnet Design

### Parameters (derived from Student IDs)
Subnetting parameters were derived from group member student IDs per the project specification.
| Parameter | Value |
|---|---|
| Total Subnets Required | 22 |
| Minimum Hosts per Subnet | 83 |
| Chosen CIDR Block | `172.20.0.0/25` |
| Subnet Mask | `255.255.255.128` |
| Total IPs per Subnet | 128 |
| Usable Hosts per Subnet | 126 |

**Justification:** A Class B block was chosen with 5 bits borrowed for subnetting (leaving 7 bits for hosts). This yields 126 usable hosts per subnet — comfortably above the 83-host minimum — while minimizing IP wastage and leaving room for future growth.

### Subnet Addressing Table (first 8 subnets)

| Subnet | Network Address | First Usable | Last Usable | Broadcast |
|---|---|---|---|---|
| Subnet 1 | 172.20.0.0 | 172.20.0.1 | 172.20.0.126 | 172.20.0.127 |
| Subnet 2 | 172.20.0.128 | 172.20.0.129 | 172.20.0.254 | 172.20.0.255 |
| Subnet 3 | 172.20.1.0 | 172.20.1.1 | 172.20.1.126 | 172.20.1.127 |
| Subnet 4 | 172.20.1.128 | 172.20.1.129 | 172.20.1.254 | 172.20.1.255 |
| Subnet 5 | 172.20.2.0 | 172.20.2.1 | 172.20.2.126 | 172.20.2.127 |
| Subnet 6 | 172.20.2.128 | 172.20.2.129 | 172.20.2.254 | 172.20.2.255 |
| Subnet 7 | 172.20.3.0 | 172.20.3.1 | 172.20.3.126 | 172.20.3.127 |
| Subnet 8 | 172.20.3.128 | 172.20.3.129 | 172.20.3.254 | 172.20.3.255 |

> Full 22-subnet table available in the project report.

---

## 🖧 Network Topology

**8 Cisco routers** interconnected via Serial links, each serving 3 LAN subnets via GigabitEthernet interfaces.

Router-to-router links use `/30` subnets from the `172.20.50.0` block — only 2 usable IPs per link, minimizing address waste on point-to-point connections.

### Router Interface Summary (excerpt)

| Device | Interface | IP Address | Subnet |
|---|---|---|---|
| Router 1 | Gi0/0 | 172.20.0.1/25 | 172.20.0.0 |
| Router 1 | Gi0/1 | 172.20.0.129/25 | 172.20.0.128 |
| Router 1 | Gi0/2 | 172.20.1.1/25 | 172.20.1.0 |
| Router 1 | Se0/3/0 | 172.20.50.1/30 | 172.20.50.0 |
| Router 2 | Gi0/0 | 172.20.2.1/25 | 172.20.2.0 |
| Router 2 | Se0/3/0 | 172.20.50.2/30 | 172.20.50.0 |
| Router 2 | Se0/3/1 | 172.20.50.5/30 | 172.20.50.4 |

> Full configuration table in the project report.

---

## 📡 Dynamic Routing — RIPv2

**Protocol used:** RIPv2 (classless dynamic routing)

RIPv2 was configured on all 8 routers to propagate routes across the network. Neighbouring routers were linked using `/30` point-to-point subnets from the `172.20.50.0` block.

**Why RIPv2 over RIPv1?**
- Supports CIDR (classless routing) — essential for our `/25` and `/30` subnets
- Sends subnet mask information with route updates
- Simple to configure for small-to-medium topologies

---

## ✅ Connectivity Verification

All subnets were tested for end-to-end reachability:

- **Ping tests:** PC-to-PC across different subnets ✓
- **Router-to-PC pings** ✓
- **`show ip route`** output verified on all 8 routers ✓
- **Traceroute** between distant subnets ✓

---

## 📁 Repository Contents

```
├── comnets.pkt            # Cisco Packet Tracer simulation file
├── Project_Report.docx    # Full report with subnet tables, screenshots & configs
└── README.md
```

---

## 🛠️ Tools Used

- **Cisco Packet Tracer** — Network simulation
- **RIPv2** — Dynamic routing protocol
- **CIDR** — IP address allocation strategy
- **Class B addressing** — `172.20.0.0` block

---

## 🚀 How to Open the Simulation

1. Install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (free with a Cisco NetAcad account)
2. Clone or download this repository
3. Open `comnets.pkt` in Packet Tracer
4. Use **Simulation Mode** to observe packet flow between subnets
5. Click any router → **CLI tab** to view routing tables with `show ip route`

---

## 📚 Key Concepts Demonstrated

- **CIDR subnetting** — dividing an address space efficiently
- **Variable-length subnet masking (VLSM)** — `/25` for LANs, `/30` for point-to-point links
- **Dynamic routing with RIPv2** — automatic route propagation
- **Multi-router topology design** — scalable enterprise network architecture
