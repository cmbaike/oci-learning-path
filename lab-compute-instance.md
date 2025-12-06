# LAB: Launching a Compute Instance on OCI

This lab demonstrates how to create a simple compute instance in OCI, connect to it, and validate network access. This is a foundational skill for almost all OCI workloads.

## 🎯 Objectives

- Create a compute instance in a public subnet
- Generate or upload an SSH key
- SSH into the instance and validate access
- Verify networking and security rules (SSH/HTTP)

---

## Prerequisites

- An OCI tenancy and access to the Console
- A VCN with a public subnet (or an internet-facing subnet)
- Permissions to create Compute instances and VCN resources

---

## 1. Navigate to Compute

1. Open the OCI Console
2. Go to **Compute → Instances**
3. Click **Create Instance**

---

## 2. Instance Configuration

Recommended configuration for this lab:

- **Name:** `lab-compute`
- **Image:** Oracle Linux (or other preferred Linux image)
- **Shape:** `VM.Standard.E2.1.Micro` (free tier eligible)
- **Availability Domain:** Any
- **Networking:**
  - **Virtual Cloud Network:** `lab-vcn`
  - **Subnet:** `public-subnet` (internet-facing / has public IP assignment)
- **Assign Public IP:** Yes (for SSH access in this lab)

---

## 3. SSH Key

Choose one option:

Option A — Generate a key locally and upload the public key to OCI

```bash
ssh-keygen -t rsa -b 4096 -C "oci-lab" -f ~/.ssh/oci_lab_key
cat ~/.ssh/oci_lab_key.pub
```

Copy the output of `cat ~/.ssh/oci_lab_key.pub` and paste it into the OCI Console when creating the instance (Add SSH keys).

Option B — Use the console key-pair generation (if available) or upload an existing public key.

---

## 4. Security Rules

Ensure the subnet's Security List or Network Security Group allows the following ingress rules for the lab:

- SSH: TCP 22 from your IP address (recommended) or 0.0.0.0/0 for temporary lab access
- HTTP: TCP 80 from 0.0.0.0/0 (if you plan to run a web server)

Security note: Allowing 0.0.0.0/0 for SSH is acceptable only in isolated lab environments. In production, restrict to your IP ranges and/or use bastion hosts.

---

## 5. Create the Instance

Click **Create** and wait until the instance status is `Running`.

---

## 6. Connect via SSH

Obtain the instance public IP from the Console and run (from your workstation):

```bash
ssh -i ~/.ssh/oci_lab_key opc@<public-ip>
```

Replace `<public-ip>` with the instance IP and ensure the private key path matches what you generated.

Expected result: a shell prompt on the Oracle Linux VM.

---

## 7. Test Connectivity and Deploy a Basic Service

On the instance, verify connectivity and install a simple web server:

```bash
ping -c 3 oracle.com
sudo dnf install nginx -y
sudo systemctl enable --now nginx
```

From your browser visit:

http://<public-ip>

You should see the default NGINX welcome page.

---

## ✔ Outcome

- Launched a compute instance (`lab-compute`)
- Uploaded or generated an SSH key and connected via SSH
- Installed and started NGINX to validate HTTP access
- Verified VCN, subnet, and security rules for SSH/HTTP

---

If you want, I can add a checklist, screenshots, or a small script to automate the setup next.
