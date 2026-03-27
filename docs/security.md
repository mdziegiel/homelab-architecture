# 🔐 Security Design

## Overview

This environment is designed using a defense-in-depth strategy, combining network segmentation, Zero Trust access, and continuous monitoring.

---

## 🛡 Perimeter Security

### Cloudflare

* DNS management
* Web Application Firewall (WAF)
* Zero Trust access controls
* Tunnel-based access (no open inbound ports)

### Benefits

* No direct WAN exposure
* DDoS protection
* Identity-aware access

---

## 🔐 Network Security

### VLAN Segmentation

* IoT devices isolated from trusted network
* Guest network fully isolated
* VPN network separated from internal systems

### Firewall Model

* Default deny between VLANs
* Explicit allow rules for required traffic
* Management access restricted to trusted VLAN

---

## 🔑 Access Control

### Zero Trust (Primary)

* Cloudflare Access for external services
* Authentication required before reaching services

### VPN Access

* WireGuard (fallback access)
* Tailscale (private overlay network)

---

## 🧠 Monitoring & Detection

### Wazuh

* Log aggregation
* Threat detection
* File integrity monitoring

### Uptime Kuma

* Service health monitoring
* Availability tracking

### Fing

* Network visibility
* Device tracking

---

## 🌐 DNS Security

* AdGuard filters malicious domains
* Unbound provides secure recursive resolution
* Prevents DNS leaks and external dependency

---

## 🔒 Internal Security Practices

* No services exposed directly to the internet
* Reverse proxy enforces HTTPS
* Minimal open ports internally
* Separation of services by function

---

## 🎯 Security Goals

* Reduce attack surface
* Prevent lateral movement
* Enforce identity-based access
* Maintain visibility across the environment
