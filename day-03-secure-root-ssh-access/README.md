# 📅 Day 3: Secure Root SSH Access (Linux)

---

## 🧠 Task

Disable direct **root SSH login** on all application servers for improved security.

---

## 🏢 Infrastructure Details

| Server       | Hostname | User   | Purpose                |
| ------------ | -------- | ------ | ---------------------- |
| App Server 1 | stapp01  | tony   | Nautilus Application 1 |
| App Server 2 | stapp02  | steve  | Nautilus Application 2 |
| App Server 3 | stapp03  | banner | Nautilus Application 3 |

---

## 🎯 Objective

* Disable direct SSH login for `root` user
* Apply changes on all servers (`stapp01`, `stapp02`, `stapp03`)
* Improve system security by restricting root access

---

## 🚀 Steps to Execute

### 1. Connect to Server

```bash
ssh tony@stapp01
```

(Repeat for all servers: `stapp02`, `stapp03`)

---

### 2. Switch to Root

```bash
sudo su -
```

---

### 3. Edit SSH Configuration

```bash
vi /etc/ssh/sshd_config
```

Find the line:

```bash
PermitRootLogin yes
```

Change it to:

```bash
PermitRootLogin no
```

> If the line is commented (`#`), uncomment and update it.

---

### 4. Restart SSH Service

```bash
systemctl restart sshd
```

---

### 5. Verify Configuration

```bash
grep PermitRootLogin /etc/ssh/sshd_config
```

Expected Output:

```bash
PermitRootLogin no
```

---

## 💡 What I Learned Today

### Why Disable Root SSH Login

Direct root access is risky because it gives full control. Disabling it improves security by forcing users to log in with normal accounts first.

### SSH Configuration Basics

The `/etc/ssh/sshd_config` file controls SSH behavior, including authentication and access settings.

### Principle of Least Privilege

Users should only have the access they need. Root access should be limited and controlled.

---

## 🛠️ What I Built / Practiced

* Connected to multiple application servers
* Modified SSH configuration file
* Disabled root login access
* Restarted SSH service to apply changes

---

## ⚠️ Challenges

* Identifying the correct config parameter
* Ensuring changes don’t break SSH access

---

## 🔧 Fix / Learning

* Learned to carefully edit SSH configs
* Understood importance of verifying before closing session

---

## 🧩 Key Takeaway

Disabling root SSH login is a simple but critical step in securing Linux servers.

---

## 🧩 Summary

```bash
Disable root SSH login by setting PermitRootLogin no in sshd_config
```

---

## ✅ Outcome

Successfully secured all application servers by disabling direct root SSH access.
