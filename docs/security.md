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

* IoT devices (smart home ecosystem) isolated from trusted network
* Guest network fully isolated
* VPN network separated from internal systems

### 🏠 Smart Home / IoT Security

The smart home ecosystem is treated as an untrusted network segment and is isolated within a dedicated IoT VLAN.

#### Devices Included

* Sonos (audio systems)
* Philips Hue (lighting)
* Leviton (switches and outlets)
* Brilliant Smart Switches
* Amazon Alexa (voice control)
* Nest Thermostats
* Ring (security cameras and alarm system)

#### Security Approach

* All IoT devices are isolated from the Home (trusted) VLAN
* No direct access to internal services or management interfaces
* Internet access is allowed but controlled
* Communication between IoT and trusted networks is explicitly blocked

#### Rationale

Smart home devices are treated as potentially vulnerable endpoints due to:

* Limited patching and update visibility
* Third-party cloud dependencies
* Increased attack surface

Segmentation ensures that compromise of an IoT device does not impact the rest of the network.

---

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
* Prevents DNS leaks and reduces reliance on external resolvers

---

## 🔒 Internal Security Practices

* No services exposed directly to the internet
* Reverse proxy enforces HTTPS
* Minimal required ports exposed internally
* Separation of services by function

---

## 🎯 Security Goals

* Reduce overall attack surface by eliminating direct WAN exposure
* Prevent lateral movement through strict VLAN segmentation
* Enforce identity-based access using Zero Trust principles
* Maintain continuous visibility into system and network activity
* Ensure secure and resilient service access

---

## ⚠️ Threat Model (High-Level)

This environment is designed with the assumption that:

* IoT devices are untrusted and potentially compromised
* External traffic is inherently hostile
* Internal lateral movement must be restricted
* Services exposed to the internet must be protected by identity and proxy layers

---

## 🔍 Key Security Decisions

### No Port Forwarding

* All external access is routed through Cloudflare tunnels
* Eliminates direct exposure of internal services

### IoT Isolation

* Smart devices are placed in a dedicated VLAN
* No access to trusted or management networks

### Layered Access

* Cloudflare (identity + edge protection)
* Reverse proxy (routing + HTTPS)
* Internal service controls

### Centralized Monitoring

* Wazuh provides security visibility
* Uptime Kuma ensures service availability
* Fing monitors network-level activity

---

## 🧠 Security Philosophy

This environment follows a defense-in-depth model where:

* Multiple layers of protection exist at the edge, network, and application levels
* Trust is never assumed based on network location
* Access is granted based on identity and necessity
* Visibility is maintained across all critical systems
