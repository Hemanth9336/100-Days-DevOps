---

# 🚀 Day 9: MariaDB Troubleshooting

## 📌 Task Overview

A critical issue was reported in the Nautilus application within the Stratos Datacenter. The production support team identified that the application was unable to connect to the database.

After investigation, it was found that the **MariaDB service was down** on the database server.

During troubleshooting, multiple issues were identified including:|

* Partial/corrupted database initialization
* Existing data directory conflicts
* Runtime/socket file issues

---

## 🎯 Objective

* Identify why MariaDB failed to start
* Fix database initialization issues
* Resolve runtime/socket conflicts
* Restore database service

---

## 🖥️ Infrastructure Details

| Server Name          | Hostname  | User    | Purpose                      |
| -------------------- | --------- | ------- | ---------------------------- |
| Application Server 1 | stapp01   | tony    | Hosts Nautilus Application 1 |
| Application Server 2 | stapp02   | steve   | Hosts Nautilus Application 2 |
| Application Server 3 | stapp03   | banner  | Hosts Nautilus Application 3 |
| Load Balancer Server | stlb01    | loki    | Distributes traffic          |
| Database Server      | stdb01    | peter   | Hosts Nautilus Database      |
| Storage Server       | ststor01  | natasha | Stores data                  |
| Backup Server        | stbkp01   | clint   | Manages backups              |
| Mail Server          | stmail01  | groot   | Handles email services       |
| Jump Host            | jump-host | thor    | Access point                 |
| Jenkins Server       | jenkins   | jenkins | CI/CD pipeline               |

---

## 🛠️ Step-by-Step Troubleshooting

### 1️⃣ Login to Jump Host

```bash id="1u7qhp"
ssh thor@jump-host
```

---

### 2️⃣ Connect to Database Server

```bash id="1dsqga"
ssh peter@stdb01
```

---

### 3️⃣ Check Service Status

```bash id="dx2ytq"
sudo systemctl status mariadb
```

👉 Output:

* `failed (exit-code)`

---

### 4️⃣ Check Logs

```bash id="c6nnvn"
sudo journalctl -xeu mariadb.service
```

### 🔍 Observed Errors:

* Database already initialized
* Initialization failed
* Service exited with status=1

---

## 🔥 Root Cause Analysis

Multiple issues were identified:

1. **Corrupted / Partial Database Initialization**
2. **Non-empty data directory (`/var/lib/mysql`)**
3. **MariaDB refusing to reinitialize**
4. **Runtime/socket file conflicts**

---

## 🔧 Solution Steps

### 🔴 Step 1: Stop MariaDB

```bash id="3nxw2u"
sudo systemctl stop mariadb
```

---

### 🔴 Step 2: Clean Data Directory

```bash id="0od1y4"
sudo rm -rf /var/lib/mysql/*
```

👉 Verify:

```bash id="v8gxtc"
ls -la /var/lib/mysql
```

---

### 🔴 Step 3: Reinitialize Database

```bash id="f3v74z"
sudo mariadb-install-db --user=mysql --datadir=/var/lib/mysql
```

---

### 🔴 Step 4: Fix Ownership

```bash id="j7jx6p"
sudo chown -R mysql:mysql /var/lib/mysql
```

---

### 🔴 Step 5: Remove Socket & PID Files

```bash id="h4fy5n"
sudo rm -f /var/lib/mysql/mysql.sock
sudo rm -f /var/lib/mysql/*.pid
```

---

### 🔴 Step 6: Fix Runtime Directory

```bash id="o3r6kk"
sudo rm -rf /run/mariadb
sudo mkdir -p /run/mariadb
sudo chown mysql:mysql /run/mariadb
```

---

### 🔴 Step 7: Start MariaDB

```bash id="w8kvt3"
sudo systemctl start mariadb
```

---

### 🔴 Step 8: Enable Service

```bash id="q4twv8"
sudo systemctl enable mariadb
```

---

### 🔴 Step 9: Verify

```bash id="v6azsb"
sudo systemctl status mariadb
```

👉 Expected:

```text id="e3m02z"
active (running)
```

---

## 🔍 How It Works

* MariaDB requires:

  * Clean data directory
  * Proper initialization
  * Correct ownership
  * Valid runtime/socket environment

* Any inconsistency leads to service failure

---

## ✅ Key Learnings

* Troubleshooting using `journalctl`
* Identifying partial database initialization issues
* Importance of cleaning corrupted data
* Handling runtime/socket file conflicts
* Multi-step debugging approach

---

## ⚠️ Notes

* Never ignore log messages
* Always verify directory state before initialization
* Socket/runtime issues are common in database failures
* Avoid repeated restarts without fixing root cause

---

## 📌 Conclusion

The issue was caused by a combination of corrupted database initialization and runtime conflicts. After cleaning the data directory, reinitializing the database, and fixing runtime/socket issues, the MariaDB service was successfully restored.

---
