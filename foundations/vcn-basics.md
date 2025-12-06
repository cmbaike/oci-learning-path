# OCI Virtual Cloud Network (VCN) - Basics

A Virtual Cloud Network (VCN) is the core networking construct in OCI.
It defines the IP space, routing, segmentation, and connectivity for all cloud resources.

## Key Concepts

- **VCN**: A regional, software-defined network.
- **Subnets**: Public or private, regional or AD scoped.
- **Route Tables**: Define where traffic goes.
- **Gateways**:
  - Internet Gateway (public access)
  - NAT Gateway (private outbound)
  - Service Gateway (private access to OCI services)
  - Local/Remote Peering (VCN-to-VCN)

## Mental Model

VCN = cloud data center
Subnets = segments
Route tables = traffic rules
Gateways = traffic entry/exits
