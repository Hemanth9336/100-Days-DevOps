---

# 🚀 Day 8: Install Ansible (Automation Setup)

## 📌 Task Overview

During a weekly meeting, the Nautilus DevOps team decided to adopt **Ansible** as their automation and configuration management tool due to its simple setup and minimal prerequisites.

To begin testing, the **jump host** will act as the **Ansible controller**, managing and automating tasks across all servers in the infrastructure.

---

## 🎯 Requirements

* Install **Ansible version 4.9.0**
* Use **pip3 only**
* Ensure Ansible is **globally accessible**
* Perform installation on **Jump Host**

---

## 🖥️ Infrastructure Details

| Server Name            | Hostname  | User    | Purpose                      |
| ---------------------- | --------- | ------- | ---------------------------- |
| Application Server 1   | stapp01   | tony    | Hosts Nautilus Application 1 |
| Application Server 2   | stapp02   | steve   | Hosts Nautilus Application 2 |
| Application Server 3   | stapp03   | banner  | Hosts Nautilus Application 3 |
| Load Balancer Server   | stlb01    | loki    | Distributes traffic          |
| Database Server        | stdb01    | peter   | Hosts database               |
| Storage Server         | ststor01  | natasha | Stores application data      |
| Backup Server          | stbkp01   | clint   | Manages backups              |
| Mail Server            | stmail01  | groot   | Handles email services       |
| Jump Host (Controller) | jump-host | thor    | Ansible control node         |
| Jenkins Server         | jenkins   | jenkins | CI/CD pipeline               |

---

## 🛠️ Step-by-Step Implementation

### 1️⃣ Login to Jump Host

```bash
ssh thor@jump-host
```

---

### 2️⃣ Switch to Root User

```bash
sudo su
```

👉 Enter password when prompted

---

### 3️⃣ Install Ansible (Version 4.9.0)

```bash
pip3 install ansible==4.9.0
```

---

### 4️⃣ Verify Installation

```bash
ansible --version
```

👉 Expected output:

```
ansible [core 2.11.x]
```

---

### 5️⃣ Verify Binary Location

```bash
which ansible
```

👉 Expected:

```
/usr/bin/ansible
```

or

```
/usr/local/bin/ansible
```

---

## 🔍 Important Note

* Ansible **4.9.0** includes **ansible-core 2.11.x**
* The CLI shows **core version**, not the package version
* Root installation ensures **global accessibility for all users**

---

## 🔍 How It Works

* Jump host acts as **Ansible control node**
* Other servers are **managed nodes**
* Communication happens over **SSH (agentless)**

---

## ✅ Key Learnings

* Installing Ansible using pip3 as root
* Ensuring global availability of commands
* Understanding Ansible vs ansible-core
* Preparing infrastructure for automation

---

## ⚠️ Notes

* Always install the **exact version required**
* Use root installation to avoid PATH issues
* Do not mix user-level and root-level installations

---

## 📌 Conclusion

Successfully installed **Ansible 4.9.0** on the jump host using pip3 with root privileges. The setup ensures global accessibility and prepares the system for automation across all servers.

---
