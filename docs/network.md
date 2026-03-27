# 🌐 Network Design & Segmentation

## Overview

The network is segmented using VLANs to isolate devices, improve security, and control traffic flow between different parts of the environment.

---

## 🧱 VLAN Structure

| VLAN  | Purpose         | Subnet          | Notes                       |
| ----- | --------------- | --------------- | --------------------------- |
| Home  | Trusted devices | 10.10.10.0/24   | Full internal access        |
| Guest | Internet-only   | 192.168.20.0/24 | No LAN access               |
| VPN   | Privacy network | 192.168.30.0/24 | Routed through VPN provider |
| IoT   | Smart devices   | 192.168.40.0/24 | Isolated from Home          |

---

## 🔐 Firewall & Traffic Rules

### Default Policy

* Inter-VLAN traffic is **blocked by default**
* Only required traffic is explicitly allowed

---

### Key Rules

#### 1. IoT VLAN Restrictions

* ❌ IoT → Home: Blocked
* ❌ IoT → Management interfaces: Blocked
* ✅ IoT → Internet: Allowed

👉 Prevents compromised IoT devices from accessing trusted systems

---

#### 2. Guest Network

* ❌ Guest → Any internal VLAN: Blocked
* ✅ Guest → Internet: Allowed

👉 Standard guest isolation model

---

#### 3. Home VLAN

* ✅ Home → All VLANs: Allowed (controlled)
* ✅ Home → Proxmox / Services: Allowed

👉 Trusted network for administration and access

---

#### 4. VPN VLAN

* ✅ VPN → Internet: Forced through VPN
* ❌ VPN → Internal networks: Restricted

👉 Ensures traffic privacy and segmentation

---

## 🌍 DNS Flow

* Clients → AdGuard DNS (primary/secondary)
* AdGuard → Unbound (recursive resolution)

### Benefits

* Ad blocking and filtering
* Local DNS control
* No reliance on external DNS providers

---

## 🔁 Traffic Flow Example

### External Access

```
Internet → Cloudflare → UniFi Gateway → Nginx Proxy Manager → Internal Service
```

---

### Internal Access

```
Home VLAN → Proxmox → Docker / Services
```

---

## 🔐 Security Considerations

* No direct port forwarding from WAN
* All external access routed through Cloudflare
* IoT devices fully isolated from trusted network
* VLAN segmentation enforced at gateway

---

## 🎯 Design Goals

* Minimize lateral movement
* Enforce least-privilege network access
* Centralize control at gateway
* Maintain visibility into traffic patterns
