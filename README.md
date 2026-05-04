<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" width="70%">
</p>

# Network Security Groups (NSGs) and Watching Traffic Between Azure Virtual Machines  
*A beginner‑friendly walkthrough with screenshots*

This guide shows you how to watch network traffic between Azure Virtual Machines using **Wireshark**, and how **Network Security Groups (NSGs)** affect what traffic is allowed or blocked.

---

## 🧰 Tools and Technologies Used
- Microsoft Azure (Virtual Machines)
- Remote Desktop (RDP)
- Command‑line tools (PowerShell, Bash)
- Network protocols: ICMP (ping), SSH, RDP, DNS, HTTP/HTTPS
- Wireshark (packet analyzer)

---

## 🖥 Operating Systems Used
- Windows 10  
- Ubuntu Server 20.04

---

# 🧭 High‑Level Steps (Beginner Friendly)

1. **Create two virtual machines** in Azure (one Windows, one Linux).
2. **Install Wireshark** on the Windows VM.
3. **Generate traffic** between the VMs (ping, SSH, web browsing).
4. **Change NSG rules** and watch how traffic changes in Wireshark.

---

# 📸 Step‑by‑Step With Screenshots

---

## **1. Create Two Virtual Machines in Azure**

You will create:
- **Windows 10 VM** (for Wiresh
