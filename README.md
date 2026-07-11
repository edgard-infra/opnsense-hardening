# OPNsense Hardening for MSP Environments

This repository provides a structured, reproducible OPNsense firewall hardening baseline designed for MSP white‑label operations. It includes aliases, rules, WireGuard configuration, logging, VLAN segmentation, and security best practices.

---

## 🧩 Firewall Architecture Overview

- **[Aliases](ca://s?q=Explicar_aliases)** — Clean, hierarchical alias structure for networks, hosts, and services.
- **[Rules](ca://s?q=Explicar_rules)** — Minimal, deterministic rule sets with explicit allow/deny logic.
- **[WireGuard](ca://s?q=Explicar_wireguard)** — Secure remote access and site‑to‑site tunnels for MSP operations.
- **[VLANs](ca://s?q=Explicar_vlans)** — Segmented networks for servers, users, VoIP, and MSP management.
- **[Logging](ca://s?q=Explicar_logging)** — Structured logs for auditing, troubleshooting, and compliance.
- **[Hardening](ca://s?q=Explicar_hardening)** — System-level security improvements and best practices.

---

## 🏗️ Base Configuration

### 1. System Settings
- **Disable root login**  
- **Enable 2FA for GUI access**  
- **Set strong admin password**  
- **Restrict GUI to management VLAN**

### 2. Interfaces & VLANs
Example VLAN layout:
- VLAN 10 — Servers  
- VLAN 20 — Workstations  
- VLAN 30 — VoIP  
- VLAN 40 — MSP Management  
- VLAN 50 — Guest  

---

## 🔐 Aliases Structure

Recommended alias hierarchy:

- `NET_SERVERS`  
- `NET_WORKSTATIONS`  
- `NET_VOIP`  
- `NET_MSP`  
- `NET_GUEST`  

- `SRV_DNS`  
- `SRV_PBS`  
- `SRV_PROXMOX`  

- `PORT_DNS`  
- `PORT_HTTP`  
- `PORT_HTTPS`  
- `PORT_WG`  

Aliases reduce rule count and improve clarity.

---

## 🚦 Firewall Rules

Example rule pattern:

Action: Pass
Interface: LAN
Source: NET_WORKSTATIONS
Destination: SRV_DNS
Port: PORT_DNS
Description: Allow DNS

Principles:
- Allow only what is required  
- Deny everything else  
- Use aliases everywhere  
- Keep rules minimal and deterministic  

---

## 🔗 WireGuard Configuration

### Server configuration example:
[Interface]
Address = 10.10.10.1/24
ListenPort = 51820
PrivateKey = <server-private-key>

[Peer]
PublicKey = <peer-public-key>
AllowedIPs = 10.10.10.2/32


### Client configuration example:
[Interface]
Address = 10.10.10.2/32
PrivateKey = <client-private-key>

[Peer]
PublicKey = <server-public-key>
Endpoint = <WAN-IP>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25

---

## 📊 Logging & Monitoring

- Enable firewall logging  
- Enable WireGuard handshake logging  
- Enable system audit logs  
- Forward logs to SIEM or MSP monitoring stack  

---

## 🛡️ Hardening Checklist

- Disable unused services  
- Restrict GUI to management VLAN  
- Enforce 2FA  
- Use aliases for all rules  
- Enable IDS/IPS (Suricata)  
- Block bogons  
- Block private networks on WAN  
- Enable DNS over TLS  

---

## 📬 Contact

For MSP white‑label firewall architecture or OPNsense hardening:  
**l3@febtech.net**


