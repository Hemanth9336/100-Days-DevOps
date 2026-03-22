# 📅 Day 1: Linux User Setup with Non-Interactive Shell

---

## 🧠 Task

Create a user named `javed` with a **non-interactive shell** on Application Server 3.

---

## 🏢 Infrastructure Details

| Server       | Hostname | User   | Purpose       |
| ------------ | -------- | ------ | ------------- |
| App Server 1 | stapp01  | tony   | Application 1 |
| App Server 2 | stapp02  | steve  | Application 2 |
| App Server 3 | stapp03  | banner | Application 3 |

---

## 🎯 Objective

* Create user: `javed`
* Assign shell: `/sbin/nologin`
* Prevent login access (security purpose)

---

## 🚀 Steps to Execute

### 1. Connect to Server

```bash
ssh banner@stapp03
```

---

### 2. Switch to Root

```bash
sudo su -
```

---

### 3. Create User

```bash
useradd -s /sbin/nologin javed
```

---

### 4. Verify User

```bash
grep javed /etc/passwd
```

**Expected Output:**

```
javed:x:...:/sbin/nologin
```

---

## 💡 What I Learned Today

### Basics of Linux User Management 🐧

Linux user management involves creating, modifying, and deleting users to control system access. Each user has a username, UID, home directory, and shell, which defines how they interact with the system.

### Difference Between Interactive and Non-Interactive Shells

* **Interactive shell** (e.g., `/bin/bash`): Allows users to log in and execute commands.
* **Non-interactive shell** (e.g., `/sbin/nologin`): Prevents user login; used for background services or system tasks.

### Why System Users Are Created for Automation and Security

System users are created to run applications or services instead of humans. This improves security by restricting login access and limiting permissions, ensuring services run safely without exposing the system to unnecessary risks.

---

## 🛠️ What I Built / Practiced

* Connected to Application Server (`stapp03`)
* Created a user `javed` with a non-interactive shell (`/sbin/nologin`)
* Verified the user and ensured login is restricted

---

## ⚠️ Challenges

* Initially confused between `/bin/bash` and `/sbin/nologin`
* Didn’t understand why we create users who can’t log in

---

## 🔧 Fix / Learning

* Realized non-interactive users are used for services, not humans
* Understood how this improves system security

---

## 🧩 Key Takeaway

Small concepts like user shells play a big role in real-world system security.

---

## 🧩 Summary

Created a secure system user that cannot log in, used for background services.
