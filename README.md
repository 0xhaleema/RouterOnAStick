# 🌐 Router-on-a-Stick Network Simulation — GNS3

A hands-on network simulation project implementing **inter-VLAN routing using the Router-on-a-Stick technique** in GNS3, built with real Cisco IOS router and switch images. The topology spans 8 VLANs with 16 VPCs and full inter-VLAN communication via subinterfaces.

---

## 🖥️ Topology Overview

![Network Topology](topology.png)

- **1 Router** (IOSv) — handles inter-VLAN routing via subinterfaces
- **1 Layer 3 Switch** (c3640) — uplink to router, trunk configuration
- **8 Ethernet Switches** (GNS3 built-in) — one per VLAN
- **16 VPCs** — distributed across 8 VLANs (2 per VLAN)
- **8 VLANs** — VLAN 10, 20, 30, 40, 50, 60, 70, 80

---

## ⚙️ Lab Setup

| Component | Details |
|---|---|
| Simulation Platform | GNS3 + GNS3 VM |
| Router Image | `vios-adventerprisek9-m.vmdk.SPA.156-2` (IOSv) |
| L3 Switch Image | `c3640-a3js-mz.124-23` |
| Access Switches | GNS3 Built-in Ethernet Switch |
| End Devices | 16 VPCs |

---

## 📡 Router-on-a-Stick — How It Works

In this design, a **single physical router interface** is divided into multiple **logical subinterfaces**, one per VLAN. Each subinterface is assigned an IP address that acts as the **default gateway** for that VLAN. Traffic between VLANs is routed through the router and sent back on the appropriate subinterface.

```
Router (IOSv)
├── Fa0/0.10  → Gateway for VLAN 10  (e.g. 192.168.10.1)
├── Fa0/0.20  → Gateway for VLAN 20  (e.g. 192.168.20.1)
├── Fa0/0.30  → Gateway for VLAN 30  (e.g. 192.168.30.1)
│   ...
└── Fa0/0.80  → Gateway for VLAN 80  (e.g. 192.168.80.1)
```

The link between the router and the L3 switch is configured as a **trunk**, allowing all VLAN-tagged traffic to pass over a single cable.

---

## 🗂️ Repository Contents

| File | Description |
|---|---|
| `network.gns3` | GNS3 project file (topology) |
| `cisco-iosv.gns3a` | GNS3 appliance template for IOSv router |
| `cisco-iosv.gns3a.md5sum` | Integrity checksum for appliance file |
| `IOSv_startup_config.img` | Startup configuration disk image |
| `IOSv_startup_config.img.md5sum` | Integrity checksum for config image |
| `Router-on-a-stick Network Using GNS3.pdf` | Full lab report and documentation |

> ⚠️ Cisco IOS image files (`vios-adventerprisek9-m.vmdk.SPA.156-2.T`, `c3640-a3js-mz.124-23.image`) are **not included** in this repository due to Cisco licensing restrictions. You must provide your own licensed copies.

---

## 🚀 How to Run

1. Install **GNS3** and configure **GNS3 VM** (VMware or VirtualBox)
2. Import the IOSv appliance using `cisco-iosv.gns3a`
3. Add the router and L3 switch IOS images in GNS3 preferences
4. Open `network.gns3` in GNS3
5. Start all devices and verify connectivity using `ping` between VPCs across VLANs

---

## ✅ Verification

Once the lab is running, test inter-VLAN routing by pinging across VLANs from any VPCS:

```bash
# From a VPC in VLAN 10, ping a VPC in VLAN 20
ping 192.168.20.x
```

All pings should succeed if subinterfaces, trunk links, and VLAN assignments are configured correctly.

---

## 📄 Documentation

A full lab report covering topology design, device configurations, VLAN assignments, and verification steps is available in:
📎 `Router-on-a-stick Network Using GNS3.pdf`

---

<p align="center">Built with 🔧 GNS3 · Cisco IOSv · Real IOS Images</p>
