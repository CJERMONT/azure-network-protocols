<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" width="70%">
</p>

# Network Security Groups (NSGs) and Watching Traffic Between Azure Virtual Machines  
*A beginner‑friendly walkthrough with screenshots*

This guide shows you how to watch network traffic between Azure Virtual Machines using **Wireshark**, and how **Network Security Groups (NSGs)** affect what traffic is allowed or blocked.

---

# 🧰 Tools and Technologies Used
- Microsoft Azure (Virtual Machines)
- Remote Desktop (RDP)
- Command‑line tools (PowerShell, Bash)
- Network protocols: ICMP (ping), SSH, RDP, DNS, DHCP, HTTP/HTTPS
- Wireshark (packet analyzer)

---

# 🖥 Operating Systems Used
- Windows 10  
- Ubuntu Server 20.04

---

# 🟦 Part 1 — Create Your Azure Virtual Machines

## **1. Create Two Virtual Machines in Azure**

You will create:
- **Windows 10 VM** (for Wireshark)
- **Ubuntu VM** (for SSH + ping testing)

### ✔️ Steps
- Go to: https://portal.azure.com  
- Create a **Resource Group**
- Create a **Windows 10 VM**
  - Select your Resource Group  
  - Allow Azure to create a **new Virtual Network** and **Subnet**
- Create a **Linux (Ubuntu) VM**
  - Select the **same Resource Group**
  - Select the **same Virtual Network + Subnet**
  - Authentication: **Username + Password**
- Confirm both VMs are running in the **same VNet/Subnet**

<p align="center">
  <img src="virtual machins in azure.png" alt="Azure VM Creation Screenshot" width="80%">
</p>

---

# 🟩 Part 2 — Observe ICMP (Ping) Traffic

## **2. Connect to the Windows VM and Install Wireshark**

### ✔️ Steps
- If on Mac: install **Microsoft Remote Desktop**
- Use RDP to connect to the Windows VM
- Inside the Windows VM:
  - Download Wireshark: https://www.wireshark.org  
  - Install with default settings

<p align="center">
  <img src="windows VM wireshark.png" alt="Wireshark Installation Screenshot" width="80%">
</p>

---

## **3. Start Capturing Traffic in Wireshark**

### ✔️ Steps
1. Open **Wireshark**
2. Select your main network adapter
3. Click **Start Capture**
4. Watch background traffic appear (DNS, ARP, etc.)

<p align="center">
  <img src="Traffic in wireshark.png" alt="Wireshark Capture Screenshot" width="80%">
</p>

---

## **4. Test Connectivity Between the VMs (Ping)**

<p align="center">
  <img src="Testconnection.png" alt="Ping and Wireshark Screenshot" width="80%">
</p>

### ✔️ Steps
1. Get the **private IP** of the Ubuntu VM  
2. In Windows VM, open **Command Prompt**  
3. Run: ping <Linux-VM-private-IP>
4. You should see replies like: Reply from 10.1.0.4: bytes=32 time<1ms TTL=128
5. In Wireshark, filter for ICMP: icmp
6. Watch the ping request/reply packets appear

> 💡 **Tip:**  
> If you block ICMP in the NSG, the ping will fail and Wireshark will show **“Destination unreachable.”**

---

# 🟧 Part 3 — Network Security Group (NSG) Testing

## **5. Block and Allow ICMP Traffic**

### ✔️ Steps
1. Start a nonstop ping: ping <Linux-VM-private-IP> -t
2. Open the **NSG** for the Ubuntu VM  
3. Add an **Inbound Rule → Deny ICMP**  
4. Watch ping fail + Wireshark show blocked ICMP  
5. Re‑enable ICMP  
6. Ping should start working again

---

# 🟪 Part 4 — Observe Other Protocols in Wireshark

## **6. Observe SSH Traffic**

### ✔️ Steps
1. In Wireshark, filter for SSH: ssh
2. From Windows VM, open PowerShell: ssh labuser@<Linux-VM-private-IP>
3. Enter username + password  
4. Type a few Linux commands  
5. Watch SSH packets appear  
6. Exit: exit

---

## **7. Observe DHCP Traffic**

### ✔️ Steps
1. In Wireshark, filter for DHCP: dhcp
2. In Windows VM, open PowerShell as Admin: ipconfig /renew
3. Watch DHCP traffic appear

---

## **8. Observe DNS Traffic**

### ✔️ Steps
1. In Wireshark, filter for DNS: dns
2. In Windows VM, run: nslookup google.com
3. Watch DNS queries + responses appear

---

## **9. Observe RDP Traffic**

### ✔️ Steps
1. In Wireshark, filter for RDP: tcp.port == 3389
2. Watch nonstop RDP traffic appear  
- RDP constantly streams your desktop  
- So traffic never stops, even when idle


---



