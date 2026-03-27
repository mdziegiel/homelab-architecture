# 📦 Services Overview

## Overview

This document outlines the services running within the home lab environment, including their purpose and where they are hosted.

---

## 🖥 Compute Placement

| Platform           | Purpose                               |
| ------------------ | ------------------------------------- |
| Proxmox VE         | Hypervisor for all workloads          |
| LXC Containers     | Lightweight services (DNS, utilities) |
| Virtual Machines   | Core services and Docker host         |
| Docker / Portainer | Application deployment and management |

---

## 📦 Service Breakdown

### 🔧 Infrastructure Services

| Service             | Purpose                     | Location    |
| ------------------- | --------------------------- | ----------- |
| AdGuard DNS         | DNS filtering / ad blocking | LXC         |
| Unbound             | Recursive DNS resolver      | LXC         |
| Nginx Proxy Manager | Reverse proxy / SSL         | VM (Docker) |

---

### 🏠 Smart Home

| Service        | Purpose                  | Location |
| -------------- | ------------------------ | -------- |
| Home Assistant | Home automation platform | VM       |

---

### 🎬 Media Stack

| Service   | Purpose          | Location |
| --------- | ---------------- | -------- |
| Plex      | Media streaming  | Docker   |
| Sonarr    | TV automation    | Docker   |
| Radarr    | Movie automation | Docker   |
| Overseerr | Media requests   | Docker   |
| SABnzbd   | Download client  | Docker   |
| Tautulli  | Plex analytics   | Docker   |

---

### 🔐 Security & Monitoring

| Service     | Purpose                 | Location |
| ----------- | ----------------------- | -------- |
| Wazuh       | SIEM / threat detection | VM       |
| Uptime Kuma | Service monitoring      | Docker   |
| Fing        | Network monitoring      | VM       |
| Gotify      | Notifications / alerts  | Docker   |

---

### 🌐 Networking & Access

| Service               | Purpose                 | Location |
| --------------------- | ----------------------- | -------- |
| Cloudflare Zero Trust | Secure external access  | Cloud    |
| Tailscale             | Private overlay network | Mixed    |
| WireGuard             | VPN access              | LXC      |

---

## 💾 Backup Services

| Service               | Purpose          | Location |
| --------------------- | ---------------- | -------- |
| Proxmox Backup Server | VM/LXC backups   | External |
| UrBackup              | Endpoint backups | VM       |
| QNAP NFS              | Storage backend  | NAS      |

---

## 🎯 Design Approach

* Services are segmented by function and risk level
* Critical infrastructure runs on VMs for isolation
* Lightweight services run in LXC containers
* Applications are containerized using Docker
* External exposure is controlled via Cloudflare and reverse proxy

---

## 🔐 Security Considerations

* No direct WAN exposure
* Reverse proxy enforces HTTPS
* DNS filtering protects endpoints
* Monitoring provides visibility into system health and threats
