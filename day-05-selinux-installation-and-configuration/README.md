# 📅 Day 5: SELinux Installation and Configuration

---

## 🧠 Task

Install SELinux packages and permanently disable SELinux on **Application Server 1 (stapp01)**.
No immediate reboot is required; changes should take effect after the scheduled reboot.

---

## 🎯 Objective

* Install required SELinux packages
* Configure SELinux to be **disabled permanently**
* Ensure configuration persists after reboot

---

## 🏢 Infrastructure Details

| Server       | Hostname | User | Purpose            |
| ------------ | -------- | ---- | ------------------ |
| App Server 1 | stapp01  | tony | Application Server |

---

## 🚀 Steps to Execute

### 1. Connect to Server

```bash
ssh tony@stapp01
```

---

### 2. Switch to Root

```bash
sudo su -
```

---

### 3. Install SELinux Packages

```bash
yum install selinux-policy selinux-policy-targeted -y
```

---

### 4. Verify SELinux Config File

```bash
cat /etc/selinux/config
```

---

### 5. Permanently Disable SELinux

Edit the config file:

```bash
vi /etc/selinux/config
```

Change:

```bash
SELINUX=enforcing
```

To:

```bash
SELINUX=disabled
```

---

### 6. Save and Exit

* Press `Esc`
* Type `:wq`
* Press Enter

---

## 🔍 Verification

```bash
grep SELINUX /etc/selinux/config
```

Expected Output:

```bash
SELINUX=disabled
```

---

## 💡 Key Learning

* SELinux provides enhanced security through mandatory access control
* Disabling SELinux requires modifying configuration file
* Changes take effect only after reboot

---

## ⚠️ Important Notes

* No need to reboot immediately
* Current SELinux status may still show enforcing/permissive
* Final state after reboot will be **disabled**

---

## ⚠️ Challenges Faced

* Understanding difference between runtime vs permanent SELinux changes
* Confusion between `setenforce` and config file changes

---

## 🧩 Summary

Installed SELinux packages and configured SELinux to be permanently disabled by updating the system configuration file.

---
