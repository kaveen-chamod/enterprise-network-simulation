# Enterprise Multi-Branch Network Design & Simulation

A comprehensive multi-tier enterprise network infrastructure designed, implemented, and simulated using **Cisco Packet Tracer**. This project showcases Variable Length Subnet Masking (VLSM), VLAN segmentation with 802.1Q trunking, Router-on-a-Stick (ROAS) inter-VLAN routing, WLAN integration, and WAN multi-router routing.

---

## 📌 Topology Overview

![Network Topology](topology-diagram.png)

The topology models a distributed enterprise structure comprising:
1. **Headquarters (HQ) LAN:** Segmented into three distinct functional departments (IT, HR, Sales) and local servers.
2. **Branch Office LAN & WLAN:** Connected via access switch, integrating wired servers and wireless hosts via an Access Point.
3. **Remote Server Branch:** Dedicated remote infrastructure terminating on an edge router.
4. **WAN Backbone:** Multi-router serial interconnection providing end-to-end communication.

---

## ⚙️ Key Technical Features

* **VLSM Address Allocation:** Optimized address space allocation based on departmental host requirements from a base network of `192.168.10.0/24`.
* **VLAN Segmentation:** Logical separation of broadcast domains across access ports to improve security and minimize broadcast traffic.
* **Inter-VLAN Routing (ROAS):** Configured 802.1Q sub-interfaces on `Router0` to route traffic between isolated departmental VLANs.
* **WAN Connectivity:** Configured back-to-back DCE/DTE serial connections across routers with routing enabled for cross-network packet forwarding.
* **Wireless LAN Integration:** Configured an Access Point bridging wireless mobile clients (laptops) seamlessly into the enterprise switch infrastructure.
* **Verification & Testing:** Fully tested end-to-end ICMP reachability across all endpoints, hosts, and servers.

---

## 📊 IP Addressing & VLSM Scheme

**Base Network:** `192.168.10.0/24`

| Department / Network | Needed Hosts | Subnet Address | Subnet Mask | CIDR | Default Gateway | Usable Host Range |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **IT Department** | 100 | `192.168.10.0` | `255.255.255.128` | `/25` | `192.168.10.1` | `.2` - `.126` |
| **HR Department** | 40 | `192.168.10.128` | `255.255.255.192` | `/26` | `192.168.10.129` | `.130` - `.190` |
| **Sales Department** | 16 | `192.168.10.192` | `255.255.255.224` | `/27` | `192.168.10.193` | `.194` - `.222` |

---

## 🛠️ Configuration Highlights

### 1. Switch Trunk Configuration (Switch0 to Router0)
```text
Switch0(config)# interface Gig0/1
Switch0(config-if)# switchport mode trunk
Switch0(config-if)# no shutdown
