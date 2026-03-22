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

Expected Output:

```
javed:x:...:/sbin/nologin
```

---

## 💡 Key Learning

* Non-interactive users are used for automation
* `/sbin/nologin` prevents login access
* Important for system security

---

## ⚠️ Mistakes I Faced

* Forgot to use non-interactive shell initially
* Confused between `/bin/bash` and `/sbin/nologin`

---

## 🧩 Summary

Created a secure system user that cannot log in, used for background services.

---
