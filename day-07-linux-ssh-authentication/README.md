---

# 🚀 Day 7: Linux SSH Authentication (Password-less Access)

## 📌 Task Overview

The system admins team at **xFusionCorp Industries** has automated scripts running from a **jump host**. These scripts need to execute operations on multiple application servers.

To ensure seamless execution, we must configure **password-less SSH authentication** from the `thor` user (jump host) to all application servers using their respective sudo users.

---

## 🎯 Requirements

* Enable **password-less SSH access**
* Source user: `thor` (jump host)
* Target servers:

  * `stapp01` → user `tony`
  * `stapp02` → user `steve`
  * `stapp03` → user `banner`

---

## 🖥️ Infrastructure Details

| Server Name          | Hostname | User   | Purpose                      |
| -------------------- | -------- | ------ | ---------------------------- |
| Application Server 1 | stapp01  | tony   | Hosts Nautilus Application 1 |
| Application Server 2 | stapp02  | steve  | Hosts Nautilus Application 2 |
| Application Server 3 | stapp03  | banner | Hosts Nautilus Application 3 |

---

## 🛠️ Step-by-Step Implementation

### 1️⃣ Login to Jump Host

```bash
ssh thor@jump_host
```

---

### 2️⃣ Generate SSH Key Pair (if not already created)

```bash
ssh-keygen -t rsa
```

* Press **Enter** for default location
* Leave passphrase empty (for automation)

---

### 3️⃣ Copy Public Key to Application Servers

#### 🔹 App Server 1

```bash
ssh-copy-id tony@stapp01
```

---

#### 🔹 App Server 2

```bash
ssh-copy-id steve@stapp02
```

---

#### 🔹 App Server 3

```bash
ssh-copy-id banner@stapp03
```

---

### 4️⃣ Verify Password-less SSH Access

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

👉 You should be able to login **without entering a password**

---

## 🔍 How It Works

* SSH key pair is generated:

  * **Private key** → stays on jump host
  * **Public key** → copied to target servers
* Public key is stored in:

```bash
~/.ssh/authorized_keys
```

* SSH uses this key for authentication instead of passwords

---

## ✅ Key Learnings

* How SSH key-based authentication works
* Importance of password-less access in automation
* Managing multiple servers using SSH
* Secure communication between systems

---

## ⚠️ Notes

* Never share your **private key**
* Ensure proper permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

* Password-less SSH is essential for automation tools like Ansible

---

## 📌 Conclusion

Successfully configured password-less SSH authentication from the `thor` user on the jump host to all application servers. This enables seamless and secure automation across the infrastructure.

---
