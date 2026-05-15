# 🛡️ Cyber Sentinel Lab
### FOSS Cybersecurity Lab with Zero Trust Architecture

---

## 📌 Overview
Cyber Sentinel Lab adalah lingkungan simulasi keamanan siber berbasis virtualisasi yang dirancang untuk monitoring, deteksi, dan analisis ancaman secara real-time.

Sistem ini menggunakan pendekatan:
- 💻 Virtualisasi lokal (Proxmox)
- 🔐 Zero Trust VPN (NetBird)
- 🛡️ Security Monitoring (Wazuh)
- 🐝 Honeypot untuk simulasi serangan

Dibangun sepenuhnya menggunakan **Free & Open Source Software (FOSS)** dengan fokus pada efisiensi biaya dan kemudahan implementasi.

---

## 🎯 Features
- 🔐 Akses aman menggunakan Zero Trust VPN (NetBird)
- 🛡️ Monitoring log & alert dengan SIEM (Wazuh)
- 🐝 Simulasi serangan menggunakan Honeypot (T-Pot / Cowrie)
- 🌐 Firewall & Network Gateway (pfSense)
- 💻 Virtual Lab berbasis Proxmox VE
- 📊 Analisis aktivitas sistem secara real-time

---

## 🏗️ System Architecture
![Architecture](docs/architecture.png)

> ⚠️ Semua akses ke sistem dilakukan melalui VPN (Zero Trust)

---

## 📚 Documentation
- 📄 [High Level Design (HDL)](docs/docs/High%20Level%20Design.md)
- 📄 [Low Level Design (LLD)](docs/Low%20Level%20Design.md)

---

## ⚙️ Tech Stack
- Proxmox VE (Virtualization)
- pfSense (Firewall & Router)
- NetBird (Zero Trust VPN)
- Linux Server
- Wazuh (SIEM)
- T-Pot / Cowrie (Honeypot)

---

## 🚀 Notes
Project ini dirancang sebagai:
- Lab pembelajaran cybersecurity
- Simulasi SOC (Security Operation Center)
- Environment testing serangan & monitoring

---

## 👥 Team
| Task | PIC |
|------|-----|
| Design & Setup System | Fathur |
| Validasi Sistem |  Arga |
| Testing Simulasi | Dimas |
| Dokumentasi & Report | Rifka |

---
