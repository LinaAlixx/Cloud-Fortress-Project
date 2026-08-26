# Cloud Fortress Project (مشروع الحصن السحابي) 🛡️☁️

An advanced secure cloud infrastructure deployed on Microsoft Azure, implementing Zero Trust Architecture to protect sensitive financial or healthcare data.

## 📋 Project Overview
This project demonstrates the implementation of a secure cloud environment using a Jumpbox architecture, private subnets, managed identities, disk encryption, and financial governance tools on Azure.

## 🛠️ Architecture & Core Components
1. **Isolation Topology (هندسة العزل):**
   - **VNet1** with 3 subnets: `default`, `Public-Subnet`, and `Private-Subnet` (10.0.2.0/24).
   - **Jumpbox VM (Public):** The single entry point with a Static Public IP, running Ubuntu 24.04 LTS.
   - **Backend Server VM (Private):** Completely isolated from the internet with no public IP.

2. **Network Security Group (NSG) Rules:**
   - Inbound traffic to the Backend Server is restricted. Only ICMP (Ping) from the Jumpbox IP (`10.0.1.4`) is allowed.
   - Verified that external ping requests from outside the architecture fail, while internal pings succeed.

3. **Identity & Secrets Management (خزنة الأسرار والهوية):**
   - Deployed **Azure Key Vault** (`kv-az1`) and generated an RSA-key.
   - Enabled **System-Assigned Managed Identity** for the Backend Server.
   - Assigned RBAC permissions (`Key Vault Data Access Administrator`) to the Backend Server.

4. **Data Encryption (تشفير البيانات):**
   - Attached an additional 32 GiB Premium SSD data disk (`backend-datadisk`) to the Backend VM.
   - Configured **Customer-Managed Key (CMK)** server-side encryption via a `DiskEncryptionSet` linked to the Key Vault.

5. **Governance & Cost Control (الحوكمة والرقابة):**
   - Unified tags applied: `Owner: Lina`, `Project: CloudFortress`, `Environment: Training`.
   - Setup a **Budget Alert** triggered at $10.00.
   - Created an **Alert Rule** to monitor and track any modifications to NSG rules.

## 📂 Repository Structure
- `/azure-templates/`: Contains ARM templates (`template.json`) for automated deployment.
- `/screenshots/`: Screenshots validating the successful implementation of tasks.
