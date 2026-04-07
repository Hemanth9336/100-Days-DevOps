---

# 🗄️ Day 18: Install and Configure MariaDB Server

## 🧠 Problem Statement

The team needs to set up a **MariaDB database server** on the Nautilus Database Server to support application deployment.

We need to

* Install and configure MariaDB
* Create a database
* Create a user
* Grant proper permissions

---

## 🎯 Objective

* Install and start MariaDB server
* Create database `kodekloud_db7`
* Create user `kodekloud_joy`
* Grant full access to the user on the database

---

## 🏗️ Infrastructure Details

| Server Name     | Hostname | User  | Purpose          |
| --------------- | -------- | ----- | ---------------- |
| Database Server | stdb01   | peter | MariaDB Database |

---

## ⚙️ Prerequisites

* Access to DB server (`stdb01`)
* Root or sudo privileges
* Internet access for package installation

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

### 2️⃣ Install MariaDB Server

```bash
yum install mariadb-server -y
```

---

### 3️⃣ Start and Enable MariaDB

```bash
systemctl start mariadb
systemctl enable mariadb
```

---

### 4️⃣ Secure Installation (Optional but Recommended)

```bash
mysql_secure_installation
```

---

### 5️⃣ Access MariaDB Shell

```bash
mysql -u root -p
```

👉 Enter root password (or press Enter if not set)

---

### 6️⃣ Create Database

```sql
CREATE DATABASE kodekloud_db7;
```

---

### 7️⃣ Create User

```sql
CREATE USER 'kodekloud_joy'@'localhost' IDENTIFIED BY 'your_password';
```

👉 Replace `your_password` with provided credentials

---

### 8️⃣ Grant Privileges

```sql
GRANT ALL PRIVILEGES ON kodekloud_db7.* TO 'kodekloud_joy'@'localhost';
```

---

### 9️⃣ Apply Changes

```sql
FLUSH PRIVILEGES;
```

---

### 🔟 Exit MariaDB

```sql
EXIT;
```

---

## 🧪 Verification

### Login using new user:

```bash
mysql -u kodekloud_joy -p
```

Then:

```sql
USE kodekloud_db7;
```

👉 Expected:

* Successful login
* Database access granted

---

## 🚫 Important Notes

* Ensure correct password is used
* Use `FLUSH PRIVILEGES` after granting access
* MariaDB service must be running

---

## 🔍 Troubleshooting

### Check MariaDB status:

```bash
systemctl status mariadb
```

---

### List databases:

```sql
SHOW DATABASES;
```

---

### List users:

```sql
SELECT User, Host FROM mysql.user;
```

---

## 💡 Key Learnings

* Installing and configuring MariaDB
* Creating databases and users
* Granting privileges using SQL
* Importance of `FLUSH PRIVILEGES`
* Managing database access securely

---

## 🏁 Final Outcome

* MariaDB installed and running
* Database `kodekloud_db7` created
* User `kodekloud_joy` created
* Full access granted to user

---

## 🚀 Summary

Successfully installed and configured MariaDB, created a database and user, and assigned appropriate permissions to support application requirements.

---
