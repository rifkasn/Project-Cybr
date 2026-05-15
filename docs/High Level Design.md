# 🧠 High Level Design (HDL)
## Cyber Sentinel Lab - Zero Trust FOSS Security Architecture

---

## 1. 📌 System Overview

Cyber Sentinel Lab adalah arsitektur sistem keamanan berbasis virtualisasi yang mengimplementasikan konsep:

- Zero Trust Network Access (ZTNA)
- Centralized Security Monitoring (SIEM)
- Threat Simulation Environment (Honeypot)
- Segmented Virtual Network Infrastructure

Sistem ini dirancang sebagai **mini Security Operation Center (SOC)** dalam skala lab dengan fokus pada observability, threat detection, dan controlled attack simulation.

---

## 2. 🧭 Design Scope & Boundary

### 2.1 In Scope
- Endpoint monitoring (laptop client)
- Internal network traffic inspection
- Log aggregation & analysis
- Attack simulation (honeypot interaction)

### 2.2 Out of Scope
- Public-facing production services
- High availability cluster
- Enterprise-scale orchestration

---

## 3. 🏗️ Architecture Blueprint

### 3.1 Logical Topology
          ┌──────────────────────┐
          │   Client Endpoint    │
          │   (Laptop User)      │
          └─────────┬────────────┘
                    │
                    ▼
          ┌──────────────────────┐
          │   NetBird VPN Layer  │
          │ (Zero Trust Access)  │
          └─────────┬────────────┘
                    │
                    ▼
                 ┌──────────────────────┐
                 │   pfSense Firewall   │
                 │  (Gateway & Filter)  │
                 └─────────┬────────────┘
                           │
           ┌───────────────┼────────────────┐
           ▼               ▼                ▼
    ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
    │ Wazuh Server │ │ Honeypot     │ │ Linux Server │
    │ (SIEM Core)  │ │ (T-Pot)      │ │ (Monitored)  │
    └──────────────┘ └──────────────┘ └──────────────┘

---

### 3.2 Network Segmentation Model

| Segment | Description | Trust Level |
|--------|------------|------------|
| Client Network | Endpoint user | Low |
| VPN Network | Secure tunnel | Medium |
| Internal Server Network | Wazuh & Server | High |
| Honeypot Network | Isolated trap network | Untrusted |

---

### 3.3 Trust Boundaries

- Boundary 1: Client → VPN  
- Boundary 2: VPN → Firewall  
- Boundary 3: Firewall → Internal Services  
- Boundary 4: Honeypot isolation zone  

Setiap boundary menerapkan:
- Authentication
- Traffic inspection
- Access restriction

---

## 4. 🧩 Component Architecture

### 4.1 Virtualization Layer

| Component | Responsibility |
|----------|---------------|
| Proxmox VE | Hosting seluruh VM dan isolasi resource |

---

### 4.2 Network Control Layer

| Component | Responsibility |
|----------|---------------|
| pfSense | Routing, NAT, firewall rules |
| NetBird | Identity-based VPN access |

---

### 4.3 Security Monitoring Layer

| Component | Responsibility |
|----------|---------------|
| Wazuh Manager | Log processing & correlation |
| Wazuh Agent | Endpoint log collector |

---

### 4.4 Threat Simulation Layer

| Component | Responsibility |
|----------|---------------|
| T-Pot / Cowrie | Meniru layanan vulnerable untuk menarik attacker |

---

### 4.5 Workload Layer

| Component | Responsibility |
|----------|---------------|
| Linux Server | Target monitoring |
| Client Laptop | User endpoint |

---

## 5. 🔄 Interaction & Data Flow Model

### 5.1 Control Flow (Access Path)

1. User melakukan authentication ke NetBird
2. VPN tunnel dibuat
3. Traffic diarahkan ke pfSense
4. Firewall melakukan filtering
5. Request diteruskan ke service internal

---

### 5.2 Observability Flow (Monitoring Path)

1. Endpoint menghasilkan log
2. Wazuh Agent mengumpulkan log
3. Log dikirim ke Wazuh Manager
4. Event diparsing dan dikorelasi
5. Alert dihasilkan jika ada anomaly

---

### 5.3 Threat Flow (Attack Path)

1. Attacker berinteraksi dengan honeypot
2. Honeypot mencatat payload & behavior
3. Log dikirim ke SIEM
4. SIEM melakukan detection rule matching
5. Alert diklasifikasikan

---

## 6. 🔐 Security Architecture

### 6.1 Access Model
- Identity-based access (NetBird)
- No direct exposure ke internet

### 6.2 Network Security
- Stateful firewall (pfSense)
- Network isolation (honeypot segment)

### 6.3 Detection Strategy
- Rule-based detection (Wazuh)
- Log correlation

### 6.4 Deception Strategy
- Honeypot sebagai decoy system
- Monitoring attacker behavior

---

## 7. ⚙️ Technology Mapping

| Layer | Technology |
|------|-----------|
| Virtualization | Proxmox VE |
| Network | pfSense |
| VPN | NetBird |
| SIEM | Wazuh |
| Honeypot | T-Pot / Cowrie |
| OS | Linux |

---

## 8. ⚠️ Constraints & Assumptions

### Constraints
- Single host virtualization
- Limited compute resource
- No redundancy

### Assumptions
- Semua endpoint menggunakan VPN
- Tidak ada direct internet exposure
- Environment hanya untuk lab

---

## 9. 🚧 Risk Consideration

| Risk | Description | Mitigation |
|------|------------|-----------|
| VPN dependency | Single point of access | Backup config |
| Resource exhaustion | VM overload | Resource limit |
| Detection gap | Rule tidak lengkap | Update rules |
| Misconfiguration | Firewall error | Audit config |

---

## 10. 🔮 Evolution Path

- Integrasi IDS/IPS (Suricata)
- SOAR automation
- Multi-node architecture
- AI-based anomaly detection

---

## 11. 👥 Responsibility Matrix

| Role | Responsibility |
|------|--------------|
| System Designer | Arsitektur & deployment |
| Validator | Validasi sistem |
| Tester | Simulasi serangan |
| Documenter | Dokumentasi |

---
