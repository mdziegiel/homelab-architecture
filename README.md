![Proxmox](https://img.shields.io/badge/Proxmox-Virtualization-orange) ![UniFi](https://img.shields.io/badge/UniFi-Network-blue) ![Cloudflare](https://img.shields.io/badge/Cloudflare-ZeroTrust-F38020) ![Docker](https://img.shields.io/badge/Docker-Containers-2496ED)

# 🏠 Home Lab Architecture

This repository documents the architecture, networking, and security design of a segmented home lab environment built using enterprise-style principles.

---

## 🧠 What This Demonstrates

* Network segmentation using VLANs and firewall rules
* Secure remote access without exposing services publicly
* Hybrid infrastructure (VMs, LXC containers, Docker)
* Defense-in-depth security design
* Monitoring and observability across services

---

## 🏗 Architecture Overview

This environment is built around:

* Proxmox for virtualization and workload separation
* VLAN segmentation (Home, Guest, IoT, VPN) for isolation
* Cloudflare Zero Trust and tunnels for secure external access
* UniFi infrastructure for network management
* Docker for application deployment
* Centralized monitoring and security tooling

---

## 📊 Architecture Diagram

<p align="center">
  <img src="docs/diagrams/architecture.png" width="900">
</p>

### 🔎 Overview

The diagram represents a segmented environment with:

* External access secured via Cloudflare Zero Trust
* Internal segmentation across multiple VLANs
* Centralized compute using Proxmox
* Containerized services running on Docker

---

## 🔐 Key Design Goals

* Minimize attack surface and eliminate direct exposure
* Enforce segmentation between trusted and untrusted devices
* Provide secure remote access using Zero Trust principles
* Maintain scalability and modular design
* Mirror real-world enterprise architecture patterns

---

## ⚙️ Core Stack

* Proxmox VE
* UniFi UDM-SE
* Cloudflare (DNS, WAF, Zero Trust)
* Docker / Portainer
* Nginx Proxy Manager
* Wazuh / Uptime Kuma
* AdGuard + Unbound

---

## 📂 Documentation

* [Architecture](docs/architecture.md)
* [Network Design](docs/network.md)
* [Services](docs/services.md)
* [Security](docs/security.md)

---

## 📂 Repository Structure

```
docs/
  diagrams/
  architecture.md
  network.md
  services.md
  security.md
```
