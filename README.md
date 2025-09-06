# IPSec Site-to-Site VPN Project

## 🎓 Graduation Project – Computer Science & Engineering

This project demonstrates the implementation of a **Site-to-Site IPSec VPN** using Cisco Packet Tracer.  
We configured two routers (R1 and R3) to establish a secure encrypted tunnel over an untrusted network, ensuring confidentiality, integrity, and authentication of transmitted data.

---

## 📖 Project Overview
- **Technology:** Cisco IOS, IPSec VPN, ISAKMP, ESP  
- **Tools Used:** Cisco Packet Tracer (PKA files), CLI configuration  
- **Team Members:**  
  - Yazan Fahad  
  - Mohammed Alharbi  
  - Bandar Almutairi  
  - Meshal Mohammed  
  - **Hatem Alhamar**  
  - Abdulaziz Aldughaim  

---

## 🛠️ Implementation
### Network Topology
![Network Topology](docs/screenshots/topology.jpg)  
*(Add your topology screenshot here)*

- **R1 ↔ R3:** VPN endpoints  
- **R2:** Transit router (pass-through)  
- **PC-A ↔ PC-C:** Communication tested through encrypted tunnel  

### Addressing Table
| Device | Interface | IP Address      | Subnet Mask     | Notes          |
|--------|-----------|----------------|-----------------|----------------|
| R1     | G0/0      | 192.168.1.1    | 255.255.255.0   | LAN segment    |
| R1     | S0/0/0    | 10.1.1.2       | 255.255.255.252 | DCE link to R2 |
| R2     | S0/0/0    | 10.1.1.1       | 255.255.255.252 | Link to R1     |
| R2     | S0/0/1    | 10.2.2.1       | 255.255.255.252 | Link to R3     |
| R3     | S0/0/1    | 10.2.2.2       | 255.255.255.252 | DCE link to R2 |
| R3     | G0/0      | 192.168.3.1    | 255.255.255.0   | LAN segment    |
| PC-A   | NIC       | 192.168.1.3    | 255.255.255.0   | Gateway R1     |
| PC-C   | NIC       | 192.168.3.3    | 255.255.255.0   | Gateway R3     |

---

## 🔑 VPN Configuration Steps
### Phase 1 – ISAKMP (IKE)
- Encryption: AES 256  
- Hashing: SHA-1  
- Authentication: Pre-shared key (`vpnpa55`)  
- DH Group: 5  

### Phase 2 – IPSec
- Transform Set: ESP-AES with ESP-SHA-HMAC  
- Traffic encrypted:  
  - From **192.168.1.0 → 192.168.3.0**  
  - From **192.168.3.0 → 192.168.1.0**  

---

## ✅ Verification
1. Verified baseline connectivity with `ping` and `tracert`.  
   ![Ping Test](docs/screenshots/ping.jpg)  
2. Observed Security Associations with:  
   ```bash
   show crypto isakmp sa
   show crypto ipsec sa
