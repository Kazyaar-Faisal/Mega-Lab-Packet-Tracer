<div align="center">

# 🌐 MEGA LAB — Cisco Packet Tracer

### A Complete Enterprise Network Lab | Phase 1 to Phase 6

[![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco&logoColor=white)](https://www.netacad.com/courses/packet-tracer)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)](https://github.com/Kazyaar-Faisal/Mega-Lab-Packet-Tracer)

</div>

---

## 🎬 Simulation Demo

<div align="center">

<img src="Simulation.gif" alt="Network Simulation Demo" width="100%">

</div>

---

## 📁 Project Files

| File | Description |
|------|-------------|
| `MEGA LAB.pkt` | Cisco Packet Tracer project file |
| `Simulation.mp4` | Full video walkthrough |
| `Simulation.gif` | Animated simulation preview |
| `MEGA_LAB_Phase_1-6.pdf` | Complete Lab Documentation & Guide (Phase 1-6) |

---

<div align="center">

# 📘 LAB DOCUMENTATION

</div>

---

## <img src="https://img.shields.io/badge/PHASE%201-Physical%20Setup%20%26%20Basic%20Configuration-0066CC?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. Saare network devices (2 Routers, 2 Switches, 2 PCs, 1 Server) ko Packet Tracer mein rakhna.
2. Sahi cables ke zariye unhe connect karna.
3. Har device ko basic IP address dena taaki connectivity establish ho.
4. WAN (Router-to-Router) aur LAN (PC-to-Gateway) connectivity verify karna.

### 🖥️ 2. Device Selection (Exact Models)
Packet Tracer ke neeche left panel se yeh devices uthayein:

| # | Device Category | Exact Model | Qty | Kis Kaam Ke Liye |
|---|----------------|-------------|-----|-------------------|
| 1 | Network Devices > Routers | **2911** | 2 | HQ aur Branch ke liye |
| 2 | Network Devices > Switches | **2960-24TT** | 2 | HQ aur Branch LAN ke liye |
| 3 | End Devices > End Devices | **PC-PT** | 2 | HQ aur Branch ke PCs |
| 4 | End Devices > End Devices | **Server-PT** | 1 | HQ Server |

### 🔧 3. Hardware Setup (Serial Module Lagana)
> Router 2911 mein by default Serial port nahi hota. Usay manually add karna padta hai.

**Steps (Dono Routers ke liye):**

1. Router par click karein → **Physical tab** kholiye.
2. Right side mein **Power Switch ko OFF** karein.
3. Left side ki list mein se **HWIC-2T** module utha kar Router ke khali slot mein drag karein.
4. Ab **Power Switch ko wapas ON** kar dein.

*(Yeh step skip karne se Serial cable connect nahi hogi).*

### 🔌 4. Cabling (Connections)
Neeche diye gaye table ke mutabiq cables lagayein. Cable uthane ke liye neeche left panel se **Connections (Lightning Icon)** select karein.

| Source Device | Source Port | Destination Device | Destination Port | Cable Type |
|--------------|------------|-------------------|-----------------|------------|
| Router0 (HQ) | GigabitEthernet0/0 | Switch2 (HQ) | FastEthernet0/1 | Copper Straight-Through |
| Router1 (Branch) | GigabitEthernet0/0 | Switch1 (Branch) | FastEthernet0/1 | Copper Straight-Through |
| Switch2 (HQ) | FastEthernet0/2 | PC0 | FastEthernet0 | Copper Straight-Through |
| Switch2 (HQ) | FastEthernet0/3 | Server0 | FastEthernet0 | Copper Straight-Through |
| Switch1 (Branch) | FastEthernet0/2 | PC1 | FastEthernet0 | Copper Straight-Through |
| Router0 (HQ) | Serial0/3/0 | Router1 (Branch) | Serial0/3/0 | **Serial DCE (Red Cable)** |

*(Note: Serial cable lagate waqt Router0 par clock icon (DCE) nazar aayega, isliye wahan clock rate lagani hai).*

### 📋 5. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway | Description |
|--------|-----------|-----------|-------------|---------|-------------|
| **HQ_Router** | Gig0/0 | `192.168.10.1` | 255.255.255.0 | - | HQ LAN Gateway |
| **HQ_Router** | Serial0/3/0 | `10.0.0.1` | 255.255.255.252 | - | WAN Link (DCE) |
| **Branch_Router** | Gig0/0 | `192.168.20.1` | 255.255.255.0 | - | Branch LAN Gateway |
| **Branch_Router** | Serial0/3/0 | `10.0.0.2` | 255.255.255.252 | - | WAN Link (DTE) |
| **HQ_Switch** | Vlan 1 | `192.168.10.2` | 255.255.255.0 | 192.168.10.1 | Management IP |
| **Branch_Switch** | Vlan 1 | `192.168.20.2` | 255.255.255.0 | 192.168.20.1 | Management IP |
| **Server0** | NIC | `192.168.10.100` | 255.255.255.0 | 192.168.10.1 | HQ Server |
| **PC0** | NIC | `192.168.10.10` | 255.255.255.0 | 192.168.10.1 | HQ PC |
| **PC1** | NIC | `192.168.20.10` | 255.255.255.0 | 192.168.20.1 | Branch PC |

### ⌨️ 6. CLI Configuration Commands

**Device 1: HQ_Router**
```
enable
configure terminal
hostname HQ_Router
! Interface Gig0/0 (LAN)
interface g0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
! Interface Serial0/3/0 (WAN - DCE side)
interface s0/3/0
ip address 10.0.0.1 255.255.255.252
clock rate 64000
no shutdown
exit
```

**Device 2: Branch_Router**
```
enable
configure terminal
hostname Branch_Router
! Interface Gig0/0 (LAN)
interface g0/0
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
! Interface Serial0/3/0 (WAN - DTE side)
interface s0/3/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
```

**Device 3: HQ_Switch**
```
enable
configure terminal
hostname HQ_Switch
! Management IP
interface vlan 1
ip address 192.168.10.2 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.10.1
exit
```

**Device 4: Branch_Switch**
```
enable
configure terminal
hostname Branch_Switch
! Management IP
interface vlan 1
ip address 192.168.20.2 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.20.1
exit
```

**Device 5: End Devices (GUI Configuration)**

**PC0:**
1. PC0 par click karein → Desktop → IP Configuration
2. IP Address: `192.168.10.10`
3. Subnet Mask: `255.255.255.0`
4. Default Gateway: `192.168.10.1`

**PC1:**
1. PC1 par click karein → Desktop → IP Configuration
2. IP Address: `192.168.20.10`
3. Subnet Mask: `255.255.255.0`
4. Default Gateway: `192.168.20.1`

**Server0:**
1. Server0 par click karein → Desktop → IP Configuration
2. IP Address: `192.168.10.100`
3. Subnet Mask: `255.255.255.0`
4. Default Gateway: `192.168.10.1`

### ✅ 7. Verification (Testing)

**Test 1: WAN Link Check (Router to Router)**
HQ_Router ke CLI par:
```
ping 10.0.0.2
```
Expected Output: `!!!!!` (5 exclamation marks) ya Reply from 10.0.0.2.

**Test 2: LAN Gateway Check (PC to Router)**
PC0 ke Command Prompt par:
```
ping 192.168.10.1
```
Expected Output: Reply from 192.168.10.1

**Test 3: Interface Status Check**
HQ_Router ke CLI par:
```
show ip interface brief
```
Expected Output: Gig0/0 aur Serial0/3/0 dono **up/up** hone chahiye.

**Test 4: Routing Table Check**
HQ_Router ke CLI par:
```
show ip route
```
Expected Output: 10.0.0.0/24 aur 192.168.10.0/24 directly connected dikhne chahiye.

### 💾 8. Save Configuration
Dono Routers aur dono Switches par yeh command chalayein:
```
write
```
Expected Output: `Building configuration... [OK]`

---

## <img src="https://img.shields.io/badge/PHASE%202-Switching%20%26%20VLANs-00994C?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. Switch par VLANs banana (VLAN 10 aur VLAN 20).
2. Ports ko VLANs mein assign karna.
3. Uplink port ko Trunk mode mein configure karna taaki Router tak saara traffic pahunch sake.
4. Router par "Router-on-a-Stick" (Sub-interfaces) configure karna taaki VLAN 10 aur VLAN 20 aapas mein baat kar sakein.

### 📋 2. VLAN Plan

| VLAN ID | Name | Ports (HQ Side) | Ports (Branch Side) |
|---------|------|-----------------|---------------------|
| **10** | HR_Department | Fa0/2 (PC0) | Fa0/2 (PC1) |
| **20** | Server_Farm | Fa0/3 (Server0) | - |
| **Trunk** | Uplink | Fa0/1 (to Router) | Fa0/1 (to Router) |

### 📋 3. Updated IP Addressing Table (Server IP Badalna Zaroori Hai)
> Kyunki Server ab VLAN 20 (Server_Farm) mein ja raha hai, uska subnet change karna padega.

| Device | Interface | IP Address | Subnet Mask | Gateway | VLAN |
|--------|-----------|-----------|-------------|---------|------|
| **HQ_Router** | Gig0/0.10 | `192.168.10.1` | 255.255.255.0 | - | VLAN 10 |
| **HQ_Router** | Gig0/0.20 | `192.168.30.1` | 255.255.255.0 | - | VLAN 20 |
| **Server0** | NIC | `192.168.30.100` | 255.255.255.0 | 192.168.30.1 | VLAN 20 |
| **PC0** | NIC | `192.168.10.10` | 255.255.255.0 | 192.168.10.1 | VLAN 10 |
| **PC1** | NIC | `192.168.20.10` | 255.255.255.0 | 192.168.20.1 | VLAN 10 |

*(Note: Physical interface Gig0/0 par IP nahi hoga, sirf sub-interfaces par hoga).*

### ⌨️ 4. CLI Configuration Commands

**Device 1: HQ_Switch (Switch2)**
```
enable
configure terminal
! Step 1: VLANs Create karna
vlan 10
name HR_Department
vlan 20
name Server_Farm
exit
! Step 2: Ports ko VLANs mein Assign karna
interface fa0/2
switchport mode access
switchport access vlan 10
exit
interface fa0/3
switchport mode access
switchport access vlan 20
exit
! Step 3: Uplink Port (Router se juda hua) ko Trunk banana
interface fa0/1
switchport mode trunk
exit
```

**Device 2: Branch_Switch (Switch1)**
```
enable
configure terminal
! Step 1: VLAN Create karna
vlan 10
name HR_Department
exit
! Step 2: Port ko VLAN mein Assign karna
interface fa0/2
switchport mode access
switchport access vlan 10
exit
! Step 3: Uplink Port ko Trunk banana
interface fa0/1
switchport mode trunk
exit
```

**Device 3: HQ_Router (Router-on-a-Stick)**
```
enable
configure terminal
! Step 1: Physical interface se IP hatana aur ON rakhna
interface g0/0
no ip address
no shutdown
exit
! Step 2: VLAN 10 ke liye Sub-interface banana
interface g0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
exit
! Step 3: VLAN 20 ke liye Sub-interface banana
interface g0/0.20
encapsulation dot1q 20
ip address 192.168.30.1 255.255.255.0
exit
```

**Device 4: End Device Update (Server0)**
1. Server0 par click karein → Desktop → IP Configuration
2. IP Address: `192.168.30.100`
3. Subnet Mask: `255.255.255.0`
4. Default Gateway: `192.168.30.1`

### ✅ 5. Verification (Testing - Galti Se Bachne Ke Liye)

**Test 1: VLAN Check (HQ_Switch par)**
```
show vlan brief
```
Expected Output:
- VLAN 10 mein Fa0/2 hona chahiye.
- VLAN 20 mein Fa0/3 hona chahiye.

**Test 2: Trunk Check (HQ_Switch par)**
```
show interfaces trunk
```
Expected Output: Fa0/1 par trunking aur 802.1q likha hona chahiye.

**Test 3: Router Sub-interface Check (HQ_Router par)**
```
show ip interface brief
```
Expected Output:
- Gig0/0 **up/up** (bina IP ke).
- Gig0/0.10 par `192.168.10.1`.
- Gig0/0.20 par `192.168.30.1`.

**Test 4: Inter-VLAN Routing (PC0 se Server ko Ping)**
PC0 ke Command Prompt par:
```
ping 192.168.30.100
```
Expected Output: Reply from 192.168.30.100 (0% loss)

**Test 5: WAN Routing (PC0 se PC1 ko Ping)**
PC0 ke Command Prompt par:
```
ping 192.168.20.10
```
Expected Output: Reply from 192.168.20.10 (0% loss)

### ⚠️ 6. Common Mistakes to Avoid (Testing Fail Hone Ki Wajah)

1. **Router par IP bhool jana:** Gig0/0 (physical port) par agar IP laga hua hai, toh sub-interfaces kaam nahi karenge. Usay `no ip address` se hatana zaroori hai.
2. **Encapsulation bhool jana:** Sub-interface par `encapsulation dot1q 10` ya `20` lagana zaroori hai. Iske bina Router ko pata nahi chalega ke kaun sa packet kis VLAN ka hai.
3. **Trunk mode bhool jana:** Switch ke uplink port (Fa0/1) par `switchport mode trunk` lagana zaroori hai. Agar woh access mode mein rahega, toh Router tak VLAN 10 aur 20 ka traffic nahi pahunchega.
4. **Server ka IP na badalna:** Server ab VLAN 20 mein hai, isliye uska IP `192.168.30.100` aur Gateway `192.168.30.1` hona chahiye. Agar woh purana `192.168.10.100` hi rahega, toh ping fail hoga.
5. **PC ka Gateway galat hona:** PC0 ka Gateway `192.168.10.1` hi rahega (VLAN 10), lekin Server ka Gateway `192.168.30.1` (VLAN 20) hoga. Inhe mix mat karein.

### 💾 7. Save Configuration
Dono Switches aur HQ_Router par:
```
write
```
[OK] aana chahiye.

---

## <img src="https://img.shields.io/badge/PHASE%203-Routing%20%26%20Inter--VLAN%20(OSPF)-CC6600?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. OSPF (Open Shortest Path First) dynamic routing protocol configure karna.
2. HQ_Router aur Branch_Router ke darmiyan routing establish karna.
3. Taaki HQ LAN (192.168.10.0/24), Server VLAN (192.168.30.0/24), aur Branch LAN (192.168.20.0/24) aapas mein baat kar sakein.
4. End-to-End connectivity verify karna.

### 📋 2. Networks to Advertise (OSPF mein daalne wale networks)

| Router | Network ID | Wildcard Mask | Area |
|--------|-----------|---------------|------|
| **HQ_Router** | 192.168.10.0 | 0.0.0.255 | 0 |
| **HQ_Router** | 192.168.30.0 | 0.0.0.255 | 0 |
| **HQ_Router** | 10.0.0.0 | 0.0.0.3 | 0 |
| **Branch_Router** | 192.168.20.0 | 0.0.0.255 | 0 |
| **Branch_Router** | 10.0.0.0 | 0.0.0.3 | 0 |

*(Note: Wildcard Mask subnet mask ka ulta hota hai. Jaise /24 ke liye 0.0.0.255, aur /30 ke liye 0.0.0.3).*

### ⌨️ 3. CLI Configuration Commands

**Device 1: HQ_Router**
```
enable
configure terminal
! OSPF Process 1 start karna
router ospf 1
! HQ LAN (VLAN 10) advertise karna
network 192.168.10.0 0.0.0.255 area 0
! Server VLAN (VLAN 20) advertise karna
network 192.168.30.0 0.0.0.255 area 0
! WAN Link advertise karna
network 10.0.0.0 0.0.0.3 area 0
exit
```

**Device 2: Branch_Router**
```
enable
configure terminal
! OSPF Process 1 start karna
router ospf 1
! Branch LAN advertise karna
network 192.168.20.0 0.0.0.255 area 0
! WAN Link advertise karna
network 10.0.0.0 0.0.0.3 area 0
exit
```

### ✅ 4. Verification (Testing - Galti Se Bachne Ke Liye)

**Test 1: OSPF Neighbor Check**
HQ_Router ke CLI par:
```
show ip ospf neighbor
```
Expected Output: Branch_Router ka Router ID **FULL** state mein dikhna chahiye.

**Test 2: Routing Table Check**
HQ_Router ke CLI par:
```
show ip route
```
Expected Output:
- `O 192.168.20.0/24 [110/65] via 10.0.0.2` dikhna chahiye (Yeh OSPF ka route hai).
- `C 192.168.10.0/24` aur `C 192.168.30.0/24` directly connected dikhne chahiye.

**Test 3: End-to-End Connectivity (PC0 to PC1)**
PC0 ke Command Prompt par:
```
ping 192.168.20.10
```
Expected Output: Reply from 192.168.20.10 (0% loss)

**Test 4: Inter-VLAN with Routing (PC0 to Server)**
PC0 ke Command Prompt par:
```
ping 192.168.30.100
```
Expected Output: Reply from 192.168.30.100 (0% loss)

### ⚠️ 5. Common Mistakes to Avoid (Testing Fail Hone Ki Wajah)

1. **Wildcard Mask galat lagana:** Sabse aam ghalti. `255.255.255.0` (subnet mask) nahi lagani, `0.0.0.255` (wildcard mask) lagani hai.
2. **Area number galat dalna:** Dono routers par **area 0** hi hona chahiye. Agar ek par 0 aur doosre par 1 hoga, toh neighbor nahi banega.
3. **WAN link advertise na karna:** Agar aap `network 10.0.0.0 0.0.0.3 area 0` nahi lagayenge, toh dono routers ek doosre ko OSPF ke zariye nahi dhoondh payenge.
4. **Interface down hona:** `show ip interface brief` se check karein ke Gig0/0 aur Serial0/3/0 dono **up/up** hain. Agar Serial down hai, toh clock rate check karein (HQ side par).
5. **Sub-interface bhool jana:** HQ_Router par Gig0/0.10 aur Gig0/0.20 up hone chahiye. Agar woh down hain, toh physical interface Gig0/0 ko `no shutdown` karein.

### 💾 6. Save Configuration
Dono Routers par:
```
write
```
[OK] aana chahiye.

---

## <img src="https://img.shields.io/badge/PHASE%204-Network%20Services%20(DHCP%2C%20DNS%2C%20HTTP)-9933CC?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. HQ_Router par DHCP Server configure karna taaki VLAN 10 ke PCs ko automatically IP mile.
2. Server0 par DNS Server configure karna taaki domain name (www.mylab.com) resolve ho sake.
3. Server0 par HTTP (Web) Server configure karna taaki browser se website open ki ja sake.
4. PC0 ko DHCP par shift karke Web Browser se website open karna.

### 📋 2. DHCP Pool Plan

| Pool Name | Network | Gateway | DNS Server | Range |
|-----------|---------|---------|------------|-------|
| **VLAN10_POOL** | 192.168.10.0 | 192.168.10.1 | 192.168.30.100 | .11 se .254 |

*(Note: Server0 ka IP 192.168.30.100 hai aur wahi DNS Server banega).*

### ⌨️ 3. Configuration Steps (CLI & GUI)

**Device 1: HQ_Router (DHCP Configuration)**
HQ_Router par click karein → CLI tab.
```
enable
configure terminal
! DHCP Pool for VLAN 10
ip dhcp pool VLAN10_POOL
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.30.100
exit
! Router ko batana hai ke DNS Server kahan hai (DNS Relay)
ip domain-lookup
ip name-server 192.168.30.100
exit
```

**Device 2: Server0 (DNS & HTTP Configuration)**
Server0 par click karein → Services tab.

**Step A: DNS Service Enable Karein**
1. Left side mein **DNS** par click karein.
2. DNS Service: **ON** karein.
3. Neeche Add button dabayein aur yeh record dalein:
   - Name: `www.mylab.com`
   - Address: `192.168.30.100`
4. **Add** par click karein. (Yeh record save ho jayega).

**Step B: HTTP Service Enable Karein**
1. Left side mein **HTTP** par click karein.
2. HTTP Service: **ON** karein.
3. Edit button dabayein aur default HTML code ko mitakar yeh likhein:

```html
<html>
<body>
<h1>Welcome to My Mega Lab</h1>
<p>This is a Cisco Packet Tracer Mega Lab.</p>
<p>Student: Syed Asad Abbas Shah</p>
<p>Program: Network Technology</p>
</body>
</html>
```
4. **Save** karein.

**Device 3: PC0 (DHCP Enable Karein)**
1. PC0 par click karein → Desktop → IP Configuration.
2. **Static** ki jagah **DHCP** select karein.
3. Kuch seconds mein automatically IP mil jayega (jaise 192.168.10.11), Subnet Mask, aur Default Gateway.

### ✅ 4. Verification (Testing - Galti Se Bachne Ke Liye)

**Test 1: DHCP Check (PC0 par)**
PC0 ke Command Prompt par:
```
ipconfig
```
Expected Output: PC0 ko automatically IP mila hua dikhna chahiye (DHCP enabled).

**Test 2: DNS Check (PC0 par)**
PC0 ke Command Prompt par:
```
ping www.mylab.com
```
Expected Output: Reply from 192.168.30.100 (Name resolve ho kar IP ban gaya).

**Test 3: Web Server Check (PC0 par)**
PC0 par click karein → Desktop → Web Browser.
URL bar mein type karein: `http://www.mylab.com`
Expected Output: Aapka banaya hua web page khul jayega.

**Test 4: Router DHCP Binding Check**
HQ_Router ke CLI par:
```
show ip dhcp binding
```
Expected Output: PC0 ka MAC address aur usko mila hua IP address dikhega.

### ⚠️ 5. Common Mistakes to Avoid (Testing Fail Hone Ki Wajah)

1. **DHCP Pool mein galti:** `network` address aur `default-router` bilkul sahi hona chahiye. Agar Gateway galat hua, toh PC internet use nahi kar payega.
2. **DNS Server ka IP galat dalna:** Router ke DHCP pool mein `dns-server 192.168.30.100` hi hona chahiye. Agar yahan `192.168.10.1` likh diya, toh domain name resolve nahi hoga.
3. **PC0 abhi bhi Static par hona:** Agar PC0 Static mode mein rahega, toh DHCP se IP nahi lega. Usay DHCP par switch karna zaroori hai.
4. **HTTP Service ON na karna:** Server0 ke Services tab mein HTTP **ON** karna zaroori hai. Agar OFF rahega, toh browser page open nahi karega.
5. **DNS Record na dalna:** Server0 ke DNS tab mein `www.mylab.com` ka record add karna zaroori hai. Bina record ke DNS resolve nahi hoga.
6. **Routing ka masla:** Agar PC0 (VLAN 10) se Server0 (VLAN 20) tak routing theek nahi hai, toh DNS aur HTTP dono fail honge. Pehle `ping 192.168.30.100` se routing check karein.

### 💾 6. Save Configuration
HQ_Router par:
```
write
```
[OK] aana chahiye.

---

## <img src="https://img.shields.io/badge/PHASE%205-Security%20%26%20Wireless-CC0000?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. SSH (Secure Shell) enable karna taaki Router ko remotely secure tareeqe se access kiya ja sake.
2. ACL (Access Control List) lagana taaki Branch network se HTTP traffic block ho jaye.
3. Wireless Router add karke WiFi connectivity setup karna.
4. Laptop ko WiFi se connect karke network access dena.

### 📋 2. Plan

| Task | Device | Detail |
|------|--------|--------|
| **SSH** | HQ_Router | Username: `admin`, Password: `cisco123` |
| **ACL** | HQ_Router | Branch (`192.168.20.0/24`) se HTTP block |
| **Wireless** | HomeRouter | SSID: `Asad_Lab_WiFi`, WPA2: `cisco12345` |
| **Laptop** | Laptop0 | WiFi se connect karega |

### ⌨️ 3. Configuration Steps (CLI & GUI)

**Part A: HQ_Router par SSH Enable Karein**
HQ_Router par click karein → CLI tab.
```
enable
configure terminal
! 1. Hostname aur Domain Name set karna (SSH ke liye zaroori hai)
hostname HQ_Router
ip domain-name mylab.com
! 2. SSH ke liye RSA Crypto Key generate karna
crypto key generate rsa
! (Jab modulus size puche, toh 1024 likhein aur Enter dabayein)
! 3. SSH Version 2 enable karna
ip ssh version 2
! 4. Local Username aur Password banana (SSH login ke liye)
username admin privilege 15 secret cisco123
! 5. VTY Lines ko SSH ke liye configure karna
line vty 0 4
transport input ssh
login local
exit
```

**Part B: HQ_Router par ACL (Access Control List) Lagayein**
```
! Extended ACL banayein (Number 100)
access-list 100 deny tcp 192.168.20.0 0.0.0.255 host 192.168.30.100 eq 80
access-list 100 permit ip any any
! Is ACL ko Router ke LAN interface par apply karein
interface g0/0
ip access-group 100 in
exit
```

**Part C: Wireless Router Add & Configure Karein**
1. Neeche **Network Devices > Wireless Devices > Wireless Router-PT** uthayein.
2. Usay Switch2 ke khali port (jaise Fa0/5) se **Copper Straight-Through** cable ke zariye connect karein.

3. Wireless Router par click karein → **GUI tab.**

**Internet Setup:**
- Internet Connection Type: **Automatic Configuration - DHCP** select karein.
- **Save Settings** dabayein.

**Wireless Setup:**
- Network Name (SSID): `Asad_Lab_WiFi`
- SSID Broadcast: **Enabled**
- **Save Settings** dabayein.

**Wireless Security:**
- Security Mode: **WPA2 Personal**
- Passphrase: `cisco12345`
- **Save Settings** dabayein.

**Part D: Laptop Connect Karein**
1. Laptop0 par click karein → **Physical tab.**
2. **Power Switch OFF** karein.
3. Left side list se **WPC300N** (wireless module) utha kar laptop ke khali slot mein drag karein.
4. **Power Switch ON** karein.
5. Ab Laptop ke Desktop → **PC Wireless** mein jayein.
6. **Connect** tab par click karein.
7. List mein se **Asad_Lab_WiFi** select karein aur **Connect** dabayein.
8. Passphrase maangega: `cisco12345` type karein.
9. Ab Laptop ke Desktop → **IP Configuration** mein **DHCP** select karein. Laptop ko automatically IP mil jayega.

### ✅ 4. Verification (Testing - Galti Se Bachne Ke Liye)

**Test 1: SSH Check (PC0 se)**
PC0 par jayein → Desktop → Command Prompt.
```
ssh -l admin 192.168.10.1
```
Password maangega: `cisco123` type karein.
Expected Output: Aap `HQ_Router#` par pahunch jayenge (SSH successful).

**Test 2: ACL Check (PC1 se HTTP Block)**
PC1 (Branch) par jayein → Desktop → Web Browser.
URL: `http://www.mylab.com`
Expected Output: Website open nahi honi chahiye (**Request Timeout** aana chahiye).

**Test 3: ACL Check (PC0 se HTTP Allow)**
PC0 (HQ) par jayein → Desktop → Web Browser.
URL: `http://www.mylab.com`
Expected Output: **Website khulni chahiye.**

**Test 4: Wireless Check (Laptop)**
Laptop0 ke Command Prompt mein jayein.
```
ping 192.168.10.1
ping 192.168.30.100
```
Expected Output: Dono ping **successful** hone chahiye.

### ⚠️ 5. Common Mistakes to Avoid (Testing Fail Hone Ki Wajah)

1. **SSH Key generate nahi karna:** Agar `crypto key generate rsa` nahi lagayenge, toh SSH kaam nahi karega. Domain name set karna bhi zaroori hai.
2. **ACL galat interface par lagana:** ACL ko interface `g0/0` par **`in`** direction mein lagana hai. Agar `out` laga diya, toh kaam nahi karega.
3. **ACL mein permit ip any any bhool jana:** Agar yeh line nahi lagayenge, toh ACL ke baad saara traffic block ho jayega (default deny).
4. **Laptop mein WiFi card na lagana:** Laptop mein by default WiFi card nahi hota. **WPC300N** module lagana zaroori hai, warna PC Wireless option kaam nahi karega.
5. **Wireless Router ko Switch se connect na karna:** Wireless Router ka **Internet port** Switch se connect karein, LAN port nahi.
6. **SSID ya Password galat dalna:** WiFi connect karte waqt SSID aur password bilkul wahi hona chahiye jo Wireless Router mein set kiya tha.

### 💾 6. Save Configuration
HQ_Router par:
```
write
```
[OK] aana chahiye.

---

## <img src="https://img.shields.io/badge/PHASE%206-Final%20Simulation%20%26%20Troubleshooting-333333?style=for-the-badge" />

### 🎯 1. Objective (Maqsad)
> Is phase ka maqsad hai:

1. Simulation Mode ka istemal karke data travel ko visually verify karna.
2. Har device par packet ka flow dekhna (Layer 2 aur Layer 3).
3. ACL ke zariye block hone wale traffic ko simulate karna.
4. Poore network ki end-to-end connectivity ko finalize karna.

### 📋 2. Simulation Plan

| Test | Source | Destination | Protocol | Expected Result |
|------|--------|------------|----------|----------------|
| 1 | Laptop0 | Server0 | ICMP (Ping) | ✅ **Successful (Data Travel)** |
| 2 | PC0 | PC1 (Branch) | ICMP (Ping) | ✅ **Successful (OSPF Routing)** |
| 3 | PC1 (Branch) | Server0 | HTTP | ❌ **Blocked (ACL Drop)** |
| 4 | PC0 | Server0 | HTTP | ✅ **Allowed (Web Page Open)** |

### 🔬 3. Simulation Steps (Step-by-Step)

**Step 1: Simulation Mode ON Karein**
- Packet Tracer ke bilkul neeche right corner mein **"Realtime"** likha hoga.
- Us par click karein, woh **"Simulation"** ban jayega.
- Event List khali hogi.

**Step 2: PDU Bhejein (Laptop to Server)**
1. Top toolbar mein **"Add Simple PDU"** (Envelope icon with +) par click karein.
2. Source: **Laptop0** par click karein.
3. Destination: **Server0** par click karein.
4. Right panel mein **Play** (Blue triangle) button dabayein.

**Step 3: Data Travel Ko Check Karein**
- Ab envelope Laptop0 se nikal kar Wireless Router, Switch2, HQ_Router, aur Server0 ki taraf jayega.
- Har device par envelope par click karein aur **PDU Information** window mein dekhein:
  - **Layer 2 (Data Link):** Source MAC aur Destination MAC.
  - **Layer 3 (Network):** Source IP aur Destination IP.
- Jab envelope Server0 par pahunche, toh reply wapas aayega.
- Event List mein saare steps (At Laptop0, At Wireless Router, etc.) dikhenge.

**Step 4: ACL Block Simulate Karein (PC1 to Server)**
1. Ab dobara **Add Simple PDU** par click karein.
2. Source: **PC1 (Branch)** par click karein.
3. Destination: **Server0** par click karein.
4. **Play** button dabayein.
5. Jab envelope HQ_Router par pahunchega, toh woh **Red X (Drop)** ho jayega.
6. Envelope par click karein aur dekhein ke ACL ne usay block kar diya.
7. Event List mein **Drop** likha hoga.

**Step 5: Wapas Realtime Mode**
- Simulation complete hone ke baad, neeche right corner se **"Realtime"** par click karein.
- Ab network normal speed par kaam karega.

### ✅ 4. Final Verification (End-to-End Testing)

**Test 1: Laptop to Server (Wireless to Wired)**
Laptop0 ke Command Prompt par:
```
ping 192.168.30.100
```
Expected Output: Reply from 192.168.30.100 (0% loss)

**Test 2: PC0 to PC1 (OSPF Routing)**
PC0 ke Command Prompt par:
```
ping 192.168.20.10
```
Expected Output: Reply from 192.168.20.10 (0% loss)

**Test 3: ACL Block (PC1 to HTTP)**
PC1 ke Web Browser par:
URL: `http://www.mylab.com`
Expected Output: **Request Timeout (Blocked)**

**Test 4: ACL Allow (PC0 to HTTP)**
PC0 ke Web Browser par:
URL: `http://www.mylab.com`
Expected Output: **Web page open honi chahiye.**

**Test 5: DHCP Binding Check**
HQ_Router ke CLI par:
```
show ip dhcp binding
```
Expected Output: PC0 ka MAC address aur IP address dikhega.

### ⚠️ 5. Common Mistakes to Avoid (Testing Fail Hone Ki Wajah)

1. **Simulation Mode mein galti se Realtime na karna:** Simulation mode mein network slow chalta hai, isliye jab aap real-time tests karein toh wapas Realtime mode par aayein.
2. **PDU galat source/destination dena:** Dhyaan rahe ke PDU hamesha sahi source aur destination par click karke banayein.
3. **ACL galat interface par lagana:** ACL ko interface `g0/0` par **`in`** direction mein lagana hai. Agar `out` laga diya, toh block nahi hoga.
4. **ACL mein permit ip any any bhool jana:** Agar yeh line nahi lagayenge, toh ACL ke baad saara traffic block ho jayega (default deny).
5. **DNS record bhool jana:** Agar `www.mylab.com` ka record nahi dalenge, toh website open nahi hogi.
6. **Wireless Router ko Static IP na dena:** Agar Wireless Router DHCP se IP nahi le pa raha, toh usay Static IP dein aur HQ_Router par route lagayein.
7. **Laptop mein WiFi card na lagana:** Laptop mein **WPC300N** module lagana zaroori hai, warna WiFi connect nahi hoga.

### 🛠️ 6. Troubleshooting (Agar Kuch Kaam Na Kare)

| Problem | Solution |
|---------|----------|
| Laptop se ping fail | Wireless Router ka IP check karein, Switch port VLAN 10 mein hai ya nahi |
| PC0 se PC1 ping fail | OSPF neighbor check karein (`show ip ospf neighbor`) |
| Web page open nahi ho raha | DNS record check karein, HTTP service ON hai ya nahi |
| SSH login fail | `crypto key generate rsa` dobara chalayein, username/password check karein |
| ACL block nahi kar raha | ACL ko interface `g0/0` par `in` lagaya hai ya nahi, `permit ip any any` hai ya nahi |

### 💾 7. Save Configuration
Aakhri baar dono Routers aur dono Switches par:
```
write
```
[OK] aana chahiye.

---

<div align="center">

## 🏆 8. Conclusion (Poore Lab Ka Natija)

</div>

> **Is Mega Lab mein humne ek complete enterprise network banaya jisme:**

- ✅ **VLANs** (VLAN 10 aur 20) banaye.
- ✅ **Inter-VLAN Routing** (Router-on-a-Stick) configure kiya.
- ✅ **OSPF** dynamic routing se HQ aur Branch ko joda.
- ✅ **DHCP, DNS, HTTP** services provide kiye.
- ✅ **SSH** se remote access secure kiya.
- ✅ **ACL** se Branch ka HTTP traffic block kiya.
- ✅ **Wireless** connectivity setup ki.

Yeh lab aapko networking ke har basic aur intermediate concept ka practical exposure deta hai. Ab aap ise dobara bana sakte hain, modify kar sakte hain, aur apne portfolio mein rakh sakte hain.

---

## 🚀 How to Use

1. Download and install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
2. Clone this repository:
   ```bash
   git clone https://github.com/Kazyaar-Faisal/Mega-Lab-Packet-Tracer.git
   ```
3. Open `MEGA LAB.pkt` in Packet Tracer
4. Follow the phases above step by step

---

<div align="center">

*Made with 💻 by [Kazyaar-Faisal](https://github.com/Kazyaar-Faisal)*

</div>
