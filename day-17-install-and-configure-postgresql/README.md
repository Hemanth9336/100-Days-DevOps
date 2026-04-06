---

# 🐘 Day 17: Install and Configure PostgreSQL

## 🧠 Problem Statement

The application team requires a **PostgreSQL database setup** for deploying a new application.

PostgreSQL is already installed on the **Database Server (stdb01)**.
We need to configure:

* A database user
* A database
* Proper access permissions

---

## 🎯 Objective

* Create PostgreSQL user `kodekloud_sam`
* Set password for the user
* Create database `kodekloud_db5`
* Grant full privileges to the user
* Do NOT restart PostgreSQL service

---

## 🏗️ Infrastructure Details

| Server Name     | Hostname | User  | Purpose             |
| --------------- | -------- | ----- | ------------------- |
| Database Server | stdb01   | peter | PostgreSQL Database |

---

## ⚙️ Prerequisites

* PostgreSQL already installed
* Access to `stdb01`
* Root/sudo privileges
* Access to `postgres` user

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **Database Server (stdb01)**

---

### 1️⃣ Login to Database Server

```bash
ssh peter@stdb01
sudo su -
```

---

### 2️⃣ Switch to PostgreSQL User

```bash
su - postgres
```

---

### 3️⃣ Access PostgreSQL Shell

```bash
psql
```

---

### 4️⃣ Create Database User

```sql
CREATE USER kodekloud_sam WITH PASSWORD 'your_password';
```

👉 Replace `your_password` with the given credentials

---

### 5️⃣ Create Database

```sql
CREATE DATABASE kodekloud_db5;
```

---

### 6️⃣ Grant Privileges (✅ Correct Syntax)

```sql
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db5 TO kodekloud_sam;
```

---

### 7️⃣ Exit PostgreSQL

```sql
\q
```

---

## 🧪 Verification

### Connect using new user:

```bash
psql -U kodekloud_sam -d kodekloud_db5
```

👉 Expected:

* Successful login
* Access granted

---

## 🚨 Issue Faced (Real Debugging)

### ❌ Error:

```sql
GRANT ALL PRIVILEGES ON kodekloud_db5 TO kodekloud_sam;
ERROR: relation "kodekloud_db5" does not exist
```

### 🔍 Root Cause

* PostgreSQL treated `kodekloud_db5` as a **table (relation)**
* Missing keyword `DATABASE`

---

### ✅ Fix

```sql
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db5 TO kodekloud_sam;
```

---

## ⚠️ Notes

* Message below is normal and can be ignored:

```bash
could not change directory to "/root": Permission denied
```

* No PostgreSQL service restart required

---

## 🔍 Useful Commands

```sql
\du   -- list users
\l    -- list databases
```

---

## 💡 Key Learnings

* Difference between **database vs relation (table)** in PostgreSQL
* Importance of correct SQL syntax
* Granting privileges at database level
* Working safely without restarting services
* Real-world debugging of SQL errors

---

## 🏁 Final Outcome

* User `kodekloud_sam` created
* Database `kodekloud_db5` created
* Privileges successfully granted
* PostgreSQL configured without downtime

---

## 🚀 Summary

Configured PostgreSQL by creating a user and database, and resolved a syntax-related permission issue to ensure proper access control for application deployment.

---
