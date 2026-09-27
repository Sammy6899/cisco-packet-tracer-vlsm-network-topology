# 🌐 🖥️ 🔀 "Brac University Campus Project" Network Architecture & Hierarchical VLSM Subnetting

> **Simulation Platform:** Cisco Packet Tracer (`421_project.pkt`)  
> **Base Network Address:** `172.16.0.0/16`

---

## 📌 Project Overview

This repository contains the complete network design, Variable Length Subnet Masking (VLSM) mathematical model, and Cisco Packet Tracer topology for an enterprise network infrastructure.

The objective is to subnet the Class B private address space **`172.16.0.0/16`** to satisfy heterogeneous host demands—ranging from large departmental LANs of over 1,800 hosts down to point-to-point router WAN links (2 usable hosts)—while eliminating IP waste, preventing address overlap, and preserving contiguous unassigned address blocks for future scalability.

---

## 📊 VLSM Subnet Planning & Host Requirements

Subnets are allocated in strict descending order of host requirements to ensure binary alignment and contiguous address space:

| Subnet ID | Purpose / Segment | Hosts Needed | Host Bits ($h$) | Block Size ($2^h$) | Subnet Mask | CIDR Prefix |
| :---: | :--- | :---: | :---: | :---: | :--- | :---: |
| **A** | Department LAN A | 1,801 | 11 | 2,048 | `255.255.248.0` | **/21** |
| **B** | Department LAN B | 901 | 10 | 1,024 | `255.255.252.0` | **/22** |
| **C** | Department LAN C | 451 | 9 | 512 | `255.255.254.0` | **/23** |
| **D** | Department LAN D | 201 | 8 | 256 | `255.255.255.0` | **/24** |
| **E** | Department LAN E | 101 | 7 | 128 | `255.255.255.128` | **/25** |
| **F** | Point-to-Point WAN Link 1 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **G** | Point-to-Point WAN Link 2 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **H** | Point-to-Point WAN Link 3 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **I** | Point-to-Point WAN Link 4 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **J** | Point-to-Point WAN Link 5 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **K** | Point-to-Point WAN Link 6 | 2 | 2 | 4 | `255.255.255.252` | **/30** |
| **L** | Point-to-Point WAN Link 7 | 2 | 2 | 4 | `255.255.255.252` | **/30** |

---

## 🗺️ Master IP Addressing Table

| Subnet | Network ID | Usable Host Range | Broadcast Address | Subnet Mask | Prefix |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **A** | `172.16.0.0` | `172.16.0.1` – `172.16.7.254` | `172.16.7.255` | `255.255.248.0` | `/21` |
| **B** | `172.16.8.0` | `172.16.8.1` – `172.16.11.254` | `172.16.11.255` | `255.255.252.0` | `/22` |
| **C** | `172.16.12.0` | `172.16.12.1` – `172.16.13.254` | `172.16.13.255` | `255.255.254.0` | `/23` |
| **D** | `172.16.14.0` | `172.16.14.1` – `172.16.14.254` | `172.16.14.255` | `255.255.255.0` | `/24` |
| **E** | `172.16.15.0` | `172.16.15.1` – `172.16.15.126` | `172.16.15.127` | `255.255.255.128` | `/25` |
| **F** | `172.16.15.128` | `172.16.15.129` – `172.16.15.130` | `172.16.15.131` | `255.255.255.252` | `/30` |
| **G** | `172.16.15.132` | `172.16.15.133` – `172.16.15.134` | `172.16.15.135` | `255.255.255.252` | `/30` |
| **H** | `172.16.15.136` | `172.16.15.137` – `172.16.15.138` | `172.16.15.139` | `255.255.255.252` | `/30` |
| **I** | `172.16.15.140` | `172.16.15.141` – `172.16.15.142` | `172.16.15.143` | `255.255.255.252` | `/30` |
| **J** | `172.16.15.144` | `172.16.15.145` – `172.16.15.146` | `172.16.15.147` | `255.255.255.252` | `/30` |
| **K** | `172.16.15.148` | `172.16.15.149` – `172.16.15.150` | `172.16.15.151` | `255.255.255.252` | `/30` |
| **L** | `172.16.15.152` | `172.16.15.153` – `172.16.15.154` | `172.16.15.155` | `255.255.255.252` | `/30` |

---

## 🌳 Binary Decomposition Tree

```text
172.16.0.0/16
├── 172.16.0.0/21  ──────────────────────────────────> [Subnet A] (2048 Block)
└── 172.16.8.0/21
    ├── 172.16.8.0/22  ──────────────────────────────> [Subnet B] (1024 Block)
    └── 172.16.12.0/22
        ├── 172.16.12.0/23  ──────────────────────────> [Subnet C] (512 Block)
        └── 172.16.14.0/23
            ├── 172.16.14.0/24  ──────────────────────> [Subnet D] (256 Block)
            └── 172.16.15.0/24
                ├── 172.16.15.0/25  ──────────────────> [Subnet E] (128 Block)
                └── 172.16.15.128/25
                    ├── 172.16.15.128/30  ────────────> [Subnet F] (WAN 1)
                    ├── 172.16.15.132/30  ────────────> [Subnet G] (WAN 2)
                    ├── 172.16.15.136/30  ────────────> [Subnet H] (WAN 3)
                    ├── 172.16.15.140/30  ────────────> [Subnet I] (WAN 4)
                    ├── 172.16.15.144/30  ────────────> [Subnet J] (WAN 5)
                    ├── 172.16.15.148/30  ────────────> [Subnet K] (WAN 6)
                    ├── 172.16.15.152/30  ────────────> [Subnet L] (WAN 7)
                    └── 172.16.15.156/30 - .252/30 ───> [Unallocated / Expansion]
```

---

## 🚀 How to Run the Simulation

Clone this repository:

```bash
git clone https://github.com/<Sammy6899>/cisco-packet-tracer-vlsm-network-topology.git
```

##
