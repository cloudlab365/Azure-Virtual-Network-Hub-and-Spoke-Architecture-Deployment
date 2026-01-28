# 🌐 Secure Hub‑and‑Spoke Network Architecture in Azure

## 🔒 Project Overview  
This project demonstrates the design and implementation of a **secure Hub‑and‑Spoke network architecture** in Microsoft Azure. The solution uses **Azure Virtual Networks (VNets)**, **Network Security Groups (NSGs)**, and **Azure Firewall** to enforce segmentation, control east‑west traffic, and reduce lateral‑movement risk across **Production** and **Development** environments.

The architecture reflects real‑world enterprise patterns and aligns with Microsoft’s cloud security best practices.

---

## 🧱 Architecture Summary

### **Hub VNet**
- Centralized security and routing layer  
- Hosts Azure Firewall for outbound filtering and traffic inspection  
- Acts as the shared services network for spokes  

### **Spoke VNets**
- Separate **Prod** and **Dev** VNets  
- Isolated workloads with strict NSG rules  
- Connected to the Hub via VNet peering  

### **Security Controls**
- Azure Firewall rules to enforce outbound restrictions  
- NSGs applied at subnet level to limit east‑west movement  
- Segmentation ensures Prod and Dev workloads remain isolated  

---

## 🏗️ High‑Level Architecture Diagram  

```
Hub VNet
 ├── Azure Firewall
 ├── Shared Services Subnet
 │
 ├── Peering
      ├── Prod Spoke VNet
      │     ├── App Subnet (NSG)
      │     ├── Data Subnet (NSG)
      │
      └── Dev Spoke VNet
            ├── App Subnet (NSG)
            ├── Test Subnet (NSG)
```

---

## 🎯 Key Outcomes

### ✔️ Improved Traffic Segmentation  
Workloads in Prod and Dev are isolated using subnet‑level NSGs and VNet peering rules.

### ✔️ Reduced Lateral Movement Risk  
Azure Firewall and NSGs enforce strict east‑west and outbound traffic policies.

### ✔️ Centralized Security Management  
Firewall policies and logging are centralized in the Hub, simplifying governance.

### ✔️ Scalable Enterprise‑Ready Design  
The architecture supports additional spokes (QA, UAT, Shared Services) without redesign.

---

## 🛠️ Technologies Used

| Component | Purpose |
|----------|---------|
| **Azure Virtual Networks (VNets)** | Logical network segmentation |
| **Network Security Groups (NSGs)** | Subnet‑level traffic filtering |
| **Azure Firewall** | Centralized outbound control and threat protection |
| **VNet Peering** | Secure Hub‑to‑Spoke connectivity |
| **Azure Monitor / Logs** | Traffic analytics and auditing |

---

## 🚀 Deployment Approach

### 1. **Create Hub VNet**
- Deploy subnets for Azure Firewall and shared services  
- Configure route tables for forced tunneling  

### 2. **Deploy Azure Firewall**
- Create DNAT, network, and application rules  
- Enable logging to Log Analytics  

### 3. **Create Spoke VNets**
- Separate Prod and Dev VNets  
- Define subnets for application tiers  

### 4. **Apply NSGs**
- Deny cross‑environment traffic  
- Allow only required inbound/outbound flows  

### 5. **Configure VNet Peering**
- Hub ↔ Prod  
- Hub ↔ Dev  
- Disable spoke‑to‑spoke transit  

---

## 📊 Security Enhancements

- Zero‑trust segmentation between Prod and Dev  
- Centralized inspection of all outbound traffic  
- Reduced attack surface through least‑privilege NSG rules  
- Full visibility via Firewall logs and NSG flow logs  

---

## 📁 Repository Structure

```
/
├── README.md
├── diagrams/
│   └── hub-spoke-architecture.png
├── templates/
│   ├── hub-vnet.json
│   ├── spoke-vnet.json
│   ├── azure-firewall.json
└── nsg/
    ├── prod-nsg.json
    └── dev-nsg.json
```

---

## 🧩 Future Enhancements

- Integration with Azure Bastion for secure admin access  
- Private Endpoints for PaaS services   

---

