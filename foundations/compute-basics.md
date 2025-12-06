# OCI Compute Basics

OCI Compute provides virtual machines and bare metal instances for running applications,
containers, and general workloads.

## Key Concepts

### 1. Shapes

A shape defines the number of OCPUs, memory, and available resources.

- **Standard** → general workloads
- **Flex** → customizable OCPU and memory
- **DenseIO** → high-performance local NVMe storage (databases, heavy workloads)
- **GPU** → AI/ML workloads

Flex shapes are the most commonly used since they optimize cost and performance.

---

### 2. Boot Volumes

Every VM has a boot volume stored in **Block Storage**.

- Automatically replicated in AD
- Supports backups and cloning

---

### 3. Instance Lifecycle

- Provisioning
- Running
- Stopped (billing applies to boot volume, not compute)
- Terminated

---

### 4. Access & Security

- Linux instances use SSH keys
- Network access controlled by NSGs and subnet security lists
- Bastion service recommended for private hosts

---

### 5. Common Use Cases

- Small apps and APIs
- Jump/bastion hosts
- Worker nodes for specialized OKE workloads
- Database servers (when not using Autonomous DB)

---

## Mental Model

**Shape = performance
Subnet = exposure
NSG = permissions
Boot volume = persistence**

Everything else builds on these fundamentals.
