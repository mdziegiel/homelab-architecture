# 🏗 Architecture Breakdown

## Overview

This environment is designed using a layered architecture with external access secured through Cloudflare and internal services hosted on a Proxmox virtualization platform.

---

## 🌐 External Access Flow

```
Internet → Cloudflare → UniFi Gateway → Nginx Proxy Manager → Internal Services
```

* Cloudflare provides DNS, WAF, and Zero Trust access
* No services are directly exposed to the internet
* All inbound traffic is filtered before reaching internal systems

---

## 🔐 Network Segmentation

The network is segmented using VLANs:

| VLAN  | Purpose                    | Subnet          |
| ----- | -------------------------- | --------------- |
| Home  | Trusted devices            | 10.10.10.0/24   |
| Guest | Internet-only access       | 192.168.20.0/24 |
| VPN   | Encrypted outbound traffic | 192.168.30.0/24 |
| IoT   | Isolated smart devices     | 192.168.40.0/24 |

### Security Model

* IoT VLAN is isolated from the Home VLAN
* Guest VLAN has no access to internal resources
* VPN VLAN routes traffic through a privacy provider
* Inter-VLAN communication is restricted at the gateway

---

## 🖥 Compute Layer (Proxmox)

* Centralized virtualization host: **10.10.10.251**
* Runs both LXC containers and virtual machines

### LXC Services

* CasaOS
* FreshRSS
* WireGuard
* Unbound

### VM Services

* Docker / Portainer
* Home Assistant
* Wazuh
* Fing

---

## 🔁 Reverse Proxy Layer

* Nginx Proxy Manager handles:

  * HTTPS termination
  * Internal routing
  * Access control

* Integrated with Cloudflare for secure external access

---

## 📦 Services Layer

### Media Stack

* Plex
* Sonarr / Radarr
* Overseerr

### Monitoring & Security

* Wazuh
* Uptime Kuma
* Gotify

### DNS Layer

* AdGuard (primary + secondary)
* Unbound (recursive resolver)

---

## 💾 Backup Strategy

* Proxmox Backup Server (PBS)
* UrBackup for endpoints
* QNAP NFS storage

---

## 🔐 Remote Access

* Cloudflare Zero Trust (primary access method)
* Tailscale (overlay network access)
* WireGuard VPN (fallback access)

---

## 🎯 Design Goals

* Zero Trust external access
* Strong network segmentation
* Centralized compute and storage
* Scalable and modular infrastructure
