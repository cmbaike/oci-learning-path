# LAB: Creating a VCN with Public and Private Subnets

This lab walks through creating a Virtual Cloud Network (VCN) from scratch,
including subnets, routing, and gateways.

## 🎯 Objectives

- Create a new VCN
- Add public and private subnets
- Attach an Internet Gateway and NAT Gateway
- Verify routing configuration

---

## 1. Create a New VCN

1. Navigate to **Networking → Virtual Cloud Networks**
2. Click **Create VCN**
3. Choose:
   - Name: `lab-vcn`
   - CIDR Block: `10.0.0.0/16`
4. Check **Create Internet Gateway**
5. Click **Create**

---

## 2. Create Subnets

### Public Subnet

- Name: `public-subnet`
- CIDR: `10.0.1.0/24`
- Subnet Type: **Public**
- Route Table: default (with IGW route)

### Private Subnet

- Name: `private-subnet`
- CIDR: `10.0.2.0/24`
- Subnet Type: **Private**
- Route Table: custom (we will attach NAT)

---

## 3. Add a NAT Gateway

1. Go to **Gateways → NAT Gateway**
2. Click **Create NAT Gateway**
3. Name: `lab-nat`

---

## 4. Update Private Route Table

Add:

Destination: 0.0.0.0/0
Target: NAT Gateway

This allows outbound access from private networks.

---

## 5. Verify

- Public subnet should show a route to IGW
- Private subnet should show a route to NAT
- VCN should now contain:
  - 2 subnets
  - Internet Gateway
  - NAT Gateway
  - 2 route tables

---

## ✔ Outcome

You have created a working network foundation for:

- OKE clusters
- Compute instances
- Load balancer architectures
- Multi-tier apps

This lab forms the basis for all future OCI designs.
