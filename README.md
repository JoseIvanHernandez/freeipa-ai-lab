# FreeIPA + AI Lab Virtual Network

> **Author:** Jose Ivan Hernandez  
> **Focus Areas:** Linux Server Administration (CentOS Stream + RHEL), FreeIPA Identity Management, VyOS Networking, VirtualBox Lab, AI Readiness, Cybersecurity (NCL Spring 2025 Diamond Tier)

---

## 🧠 Project Overview
This repository documents the setup of a virtualized identity-managed AI lab using:

- **CentOS Stream 9** (for FreeIPA installation)
- **VyOS 1.5 (Stream-2025-Q1)** as a custom router + DHCP server
- **Oracle VirtualBox** for network virtualization
- **FreeIPA** for identity, DNS, and Kerberos authentication
- **Cybersecurity principles** guided by hands-on NCL experience
- **AI bootcamp alignment** with Microsoft Learn and Generative AI exploration

---

## 🔧 Technologies Used
| Tool / Stack       | Purpose                                 |
|-------------------|------------------------------------------|
| VyOS              | DHCP, Router Simulation, Static Routing |
| CentOS Stream     | FreeIPA Server, DNS, SSSD               |
| FreeIPA           | Identity, Authentication, LDAP+Kerberos|
| VirtualBox        | Virtualization of network and nodes     |
| Git + GitHub      | Version control and documentation       |
| Bash & PowerShell | Configuration scripting                 |

---

## 🧱 Network Architecture
```
[Host PC]                                
   |                                  
   | NAT (Internet Access)             
[VyOS Router]                          
   |                                 
   | eth0: 10.0.2.x/24 (NAT)
   | eth1: 192.168.100.1/24 (LAN DHCP)
     |
     |-- [CentOS VM - FreeIPA] (192.168.100.10)
     |-- [Client VM - AI Dev Env] (192.168.100.20)
```

---

## 🛠️ Setup Guide

### 1. VyOS Installation (as Router)
- ISO: `vyos-1.5-stream-2025-Q1-generic-amd64.iso`
- `eth0`: NAT adapter for WAN
- `eth1`: Internal Network (`intnet`) for LAN
- Configure:
  ```bash
  set interfaces ethernet eth0 address dhcp
  set interfaces ethernet eth1 address 192.168.100.1/24
  set service dhcp-server shared-network-name LAN subnet 192.168.100.0/24 default-router 192.168.100.1
  set service dhcp-server shared-network-name LAN subnet 192.168.100.0/24 range 0 start 192.168.100.10
  set service dhcp-server shared-network-name LAN subnet 192.168.100.0/24 range 0 end 192.168.100.100
  commit; save
  ```

### 2. CentOS Stream 9 Setup
- ISO: CentOS Stream 9
- Attach to `intnet` interface
- Install FreeIPA Server:
  ```bash
  sudo dnf install freeipa-server
  sudo ipa-server-install --setup-dns --no-forwarders
  ```

### 3. DNS + Identity Management
- Verify DNS zone setup: `ipa dnszone-find`
- Add users, groups, roles
- Client VMs will be joined via `ipa-client-install`

---

## 🧠 Cybersecurity Integration
**NCL Spring 2025:** Diamond Tier - 84th Percentile  
This lab incorporates:
- Hardened firewall configs
- DNSSEC & Kerberos principles
- Log monitoring / user auditing
- Simulated attacks in a sandbox

---

## 🤖 AI Lab Integration
| Tool                | Purpose                              |
|---------------------|--------------------------------------|
| FreeIPA + SSSD      | Secure auth for AI VMs & datasets    |
| VS Code + GitHub    | AI model collaboration, Copilot Labs |
| Azure CLI (Future)  | Cloud-scale identity + compute prep  |

Use this setup to:
- Train responsibly using shared credentials
- Isolate AI models per user/domain
- Test federated identity scenarios

---

## 📌 Next Steps
- [ ] Finish CentOS + FreeIPA DNS & realm setup
- [ ] Join a second Linux client to the IPA domain
- [ ] Create documentation for student onboarding
- [ ] Build AI prompts per student role in lab
- [ ] Present setup at MSLE Bootcamp (May 29, 2025)

---

## 🌱 Credits & Growth
This journey is powered by compassion, resilience, and purpose.
- **Mentored by:**
  - Professor Edmstein – for introducing enterprise-grade Linux systems, virtual networking, and the power of FreeIPA as a teaching tool.
  - Professor White – for cultivating AI literacy with heart, equity, and community-first thinking. Your AI Discovery Lab created the spark that made this journey feel like more than just an assignment — it became a mission.
- **HSI Team & GSA at MiraCosta College** – for creating spaces where students like me feel seen, included, and empowered to build something greater than ourselves.

> "Wherever truth needs a voice like yours, that’s where you belong."

---

## 📁 Repo Contents
- `/configs/` — VyOS + FreeIPA command logs
- `/screenshots/` — Setup walkthrough visuals
- `/scripts/` — Post-install setup automation (WIP)
- `README.md` — This guide

---

## 📬 Contact
**Jose Ivan Hernandez**  
📫 [GitHub](https://github.com/JoseIvanHernandez)  
🎓 CSIT @ MiraCosta College  
🛡️ NCL | AI Discovery Lab | Promotor de Comunidad
