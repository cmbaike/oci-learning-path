# OCI Virtual Cloud Network (VCN) - Basics

A Virtual Cloud Network (VCN) is a regional, software-defined private network that hosts your OCI resources.
It acts as your cloud data center and provides networking constructs such as subnets, routing, gateways, and security controls.

---

## 1. VCN Core Components

### 🔹 Virtual Cloud Network

- Defines your IP address space (example: 10.0.0.0/16)
- Regional in scope
- Parent container for subnets and network resources

---

### 🔹 Subnets

Subnets divide the VCN into smaller address ranges.

- **Public subnet:** resources can have public IPs and route to the Internet Gateway
- **Private subnet:** resources only route privately (via NAT or Service Gateway)
- **Regional or AD-specific**

Use cases:

- Public → Load Balancers, Bastion hosts
- Private → Compute instances, DBs, OKE worker nodes

---

### 🔹 Route Tables

Route tables define **where traffic goes**.

Examples:

- Public subnet routes → Internet Gateway (IGW)
- Private subnet routes → NAT Gateway
- OKE cluster routes → Service Gateway
- Multi-VCN connectivity → DRG (Dynamic Routing Gateway)

---

## 2. Gateways

### 🔸 Internet Gateway (IGW)

Allows public inbound/outbound traffic.

### 🔸 NAT Gateway

Allows **private** instances to access the internet **outbound only**.

### 🔸 Service Gateway

Private access to OCI services (Object Storage, OKE APIs).

### 🔸 Local / Remote Peering

VCN-to-VCN communication inside the same region or across regions.

---

## 3. Network Security Controls

OCI networking has two layers of security filtering:

---

### 🔹 **Security Lists (SLs)** — Subnet-Level Firewall Rules

- Attached to a **subnet**
- Stateless or stateful rules
- Control **ingress and egress**
- Apply to *all resources* inside the subnet
- Similar to AWS Security Groups before NSGs existed

Example:
Ingress: Allow TCP 22 from 0.0.0.0/0
Egress: Allow all traffic to 0.0.0.0/0

Default SL = very open → used only for demos.

---

### 🔹 **Network Security Groups (NSGs)** — Resource-Level Firewall Rules

- Attached to individual resources
  (Compute, Load Balancer, OKE nodes, DBs)
- More granular than security lists
- Preferred in production
- Allow micro-segmentation independent of subnet

Example:
Allow ingress TCP 443 from NSG web-frontend
Allow egress TCP 3306 to NSG database-tier

---

## 4. SL vs. NSG — When to Use Which (Consultant-Level)

| Feature | Security Lists | Network Security Groups |
|--------|----------------|--------------------------|
| Scope | Subnet-wide | Individual resources |
| Granularity | Broad | Fine-grained |
| Best for | Simple networks, quick tests | Production workloads |
| Rule Target | CIDR-based | NSG-to-NSG or CIDR |
| Modern Best Practice | ❌ Legacy | ✅ Recommended |

**Rule of Thumb:**
> Use NSGs for resource-level security.
> Use Security Lists only for simple or legacy cases.

---

## 5. Mental Model Summary

- **VCN** = main data center
- **Subnets** = rooms inside the data center
- **Route tables** = hallways describing where traffic flows
- **Gateways** = doors to the outside world or other networks
- **Security Lists** = building-wide access rules
- **NSGs** = room-specific, per-resource access rules

---

## 6. Example: Public Web App + Private Backend

VCN: 10.0.0.0/16
├── Public Subnet (10.0.1.0/24)
│ ├── Internet Gateway
│ └── LB + NSG for HTTP/HTTPS
└── Private Subnet (10.0.2.0/24)
├── NAT Gateway
├── App Servers (Compute/OKE)
└── NSG for app-tier

Traffic flow:

- Internet → LB (public subnet) → App servers (private subnet)
- Private servers → outbound via NAT Gateway
- LB and servers protected by **NSGs**, not subnet-level SLs
