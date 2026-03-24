# 📅 Day 4: Script Execution Permissions (Linux)

---

## 🧠 Task

Grant executable permissions to the script `/tmp/xfusioncorp.sh` on **App Server 2**, ensuring all users can execute it.

---

## 🏢 Infrastructure Details

| Server       | Hostname | User   | Purpose                |
| ------------ | -------- | ------ | ---------------------- |
| App Server 1 | stapp01  | tony   | Nautilus Application 1 |
| App Server 2 | stapp02  | steve  | Nautilus Application 2 |
| App Server 3 | stapp03  | banner | Nautilus Application 3 |

---

## 🎯 Objective

* Grant execute permission to `/tmp/xfusioncorp.sh`
* Ensure **all users** can execute the script

---

## 🚀 Steps to Execute

### 1. Connect to Server

```bash
ssh steve@stapp02
```

---

### 2. Switch to Root

```bash
sudo su -
```

---

### 3. Check Current Permissions

```bash
ls -l /tmp/xfusioncorp.sh
```

---

### 4. Add Execute Permission for All Users ✅

```bash
chmod 755 /tmp/xfusioncorp.sh
```

> This explicitly gives execute permission to **owner, group, and others**

---

### 5. Verify Permissions

```bash
ls -l /tmp/xfusioncorp.sh
```

Expected Output:

```
-rwxr-xr-x ...
```

---

## 💡 What I Learned Today

### File Permissions in Linux

Linux uses permissions (read, write, execute) to control access to files and scripts.

### Meaning of Execute Permission

Execute (`x`) allows a script or file to be run as a program.

### chmod Command Basics

The `chmod` command is used to modify file permissions for users (owner, group, others).

---

## 🛠️ What I Built / Practiced

* Connected to Application Server (`stapp02`)
* Checked existing file permissions
* Granted execute permission using `chmod 755`
* Verified updated permissions

---

## ⚠️ Challenges

* Initially used `chmod +x`, but it didn’t pass the validation ❌
* Understanding how permissions apply to all users

---

## 🔧 Fix / Learning

* Used `chmod 755` to explicitly assign permissions
* Learned difference between symbolic (`+x`) and numeric (`755`) modes

---

## 🧩 Key Takeaway

Explicit permissions (`755`) are more reliable in controlled environments and ensure correct access.

---

## 🧩 Summary

```bash
chmod 755 /tmp/xfusioncorp.sh
```

---

## ✅ Outcome

Successfully granted executable permissions to the script for all users and resolved the validation issue.
