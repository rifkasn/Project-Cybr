# 🔍 Low Level Design (LLD)
## Cyber Sentinel Lab - Implementation Detail

---

## 1. 📌 Overview

Dokumen ini menjelaskan detail implementasi teknis dari Cyber Sentinel Lab, termasuk konfigurasi sistem, instalasi layanan, dan integrasi antar komponen.

---

## 2. 🖥️ Environment Setup

### 2.1 Host Requirement
- CPU: Minimal 4 Core
- RAM: Minimal 8 GB (Recommended 16 GB)
- Storage: Minimal 100 GB

---

### 2.2 Virtualization Platform

Install Proxmox VE:

```bash
# download ISO dari official proxmox
# install via bootable media
```

3. 🧱 Virtual Machine Design
| VM Name      | OS      | Function          | RAM  | CPU    |
| ------------ | ------- | ----------------- | ---- | ------ |
| pfSense      | FreeBSD | Firewall          | 1 GB | 1 Core |
| Wazuh Server | Ubuntu  | SIEM              | 4 GB | 2 Core |
| Honeypot     | Ubuntu  | Attack Simulation | 2 GB | 1 Core |
| Linux Server | Ubuntu  | Monitoring Target | 1 GB | 1 Core |

## 3. 🧱 VM Design

| VM | Function |
|----|--------|
| pfSense | Firewall |
| Wazuh | SIEM |
| Honeypot | Attack Simulation |
| Linux Server | Target |

---

## 4. 🌐 Network Setup

### pfSense
- Gateway utama
- Firewall aktif

---

## 5. 🔐 VPN (NetBird)

```bash
curl -fsSL https://pkgs.netbird.io/install.sh | sh
netbird up 
```

---
## 6. 🛡️ Wazuh

```bash
curl -sO https://packages.wazuh.com/install.sh
sudo bash install.sh
```

---
## 7. 🐝 Honeypot

```bash
git clone https://github.com/telekom-security/tpotce
cd tpotce
sudo ./install.sh
```

---
## 8. 🔄 Integration

- Endpoint → Wazuh
- Honeypot → Wazuh

---
## 9. 🧪 Testing

```bash
hydra -l root -P pass.txt ssh://target-ip
```

---
## 10. 🔐 Security

- VPN only access
- Firewall rules aktif

## 11. 🧪 Troubleshooting

| Issue | Possible Cause | Solution |
|------|--------------|----------|
| VPN tidak connect | Service NetBird belum aktif | Jalankan `netbird up` |
| VPN disconnect tiba-tiba | Koneksi jaringan tidak stabil | Restart koneksi & cek network |
| Wazuh tidak berjalan | Service berhenti | Jalankan `systemctl restart wazuh-manager` |
| Wazuh agent tidak terhubung | IP server salah / agent belum register | Cek konfigurasi `/var/ossec/etc/ossec.conf` |
| Dashboard Wazuh tidak bisa diakses | Port tidak terbuka | Cek firewall pfSense & port 443 |
| Honeypot tidak berjalan | Docker service mati | Jalankan `systemctl restart docker` |
| Honeypot tidak menerima serangan | Network tidak expose | Cek routing & firewall rules |
| VM tidak bisa koneksi internet | Gateway salah | Cek konfigurasi pfSense |
| Resource overload (lemot) | RAM/CPU kurang | Kurangi jumlah VM atau upgrade resource |
| Tidak ada alert di Wazuh | Rule belum aktif | Update rules atau trigger event manual |

---

### 🔍 Debug Commands

```bash
# cek status VPN
netbird status

# cek service wazuh
systemctl status wazuh-manager

# cek docker (honeypot)
docker ps

# cek network
ip a
ping 8.8.8.8
```

### ⚠️ Notes

- Pastikan semua service berjalan sebelum testing  
- Gunakan VPN untuk semua akses  
- Lakukan pengecekan log jika terjadi error  
