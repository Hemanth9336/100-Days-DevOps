---

# 📦 Day 10: Linux Bash Script – Website Backup Automation

## 🧠 Problem Statement

The production support team at **xFusionCorp Industries** needs a Bash script to automate website backups.

A static website is hosted on **App Server 3**, and the goal is to -

* Create a backup of the website media files
* Store it locally
* Copy it to a remote storage server
* Ensure password-less execution
* Avoid using `sudo` inside the script

---

## 🎯 Objective

Create a Bash script named:

```
/scripts/media_backup.sh
```

That performs the following:

1. Compress `/var/www/html/media` into a zip file
2. Store it in `/backup/` on App Server 3
3. Copy the backup to the Storage Server (`/backup/`)
4. Execute without password prompt
5. Run using the respective server user (e.g., `banner`)

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname | User    | Purpose              |
| -------------------- | -------- | ------- | -------------------- |
| Application Server 3 | stapp03  | banner  | Hosts static website |
| Storage Server       | ststor01 | natasha | Stores backup data   |

---

## ⚙️ Prerequisites

Before running the script:

### 1. Install `zip` package (run manually)

```bash
sudo yum install zip -y   # RHEL/CentOS
# OR
sudo apt install zip -y   # Ubuntu
```

### 2. Setup Passwordless SSH

On **App Server 3 (stapp03)**:

```bash
ssh-keygen -t rsa
ssh-copy-id natasha@ststor01
```

This ensures the script does not prompt for a password.

---

## 📜 Script: `media_backup.sh`

```bash
#!/bin/bash

# Variables
SOURCE_DIR="/var/www/html/media"
BACKUP_DIR="/backup"
ZIP_NAME="xfusioncorp_media.zip"
REMOTE_USER="natasha"
REMOTE_HOST="ststor01"
REMOTE_DIR="/backup"

# Step 1: Create backup directory if not exists
mkdir -p $BACKUP_DIR

# Step 2: Create zip archive
zip -r $BACKUP_DIR/$ZIP_NAME $SOURCE_DIR

# Step 3: Copy archive to storage server
scp $BACKUP_DIR/$ZIP_NAME ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}

# Step 4: Success message
echo "Backup completed and copied to storage server successfully."
```

---

## 🔐 Permissions

Make the script executable:

```bash
chmod +x /scripts/media_backup.sh
```

---

## ▶️ Execution

Run the script:

```bash
/scripts/media_backup.sh
```

---

## ✅ Expected Outcome

* `xfusioncorp_media.zip` created in `/backup/`
* Backup successfully copied to `ststor01:/backup/`
* No password prompt during execution

---

## 🚫 Important Notes

* ❌ Do NOT use `sudo` inside the script
* ✅ Ensure SSH keys are configured for passwordless login
* ✅ Script should be executed using the respective server user (`banner`)

---

## 💡 Key Learnings

* Automating backups using Bash scripting
* Using `zip` for compression
* Secure file transfer with `scp`
* Setting up passwordless SSH authentication
* Writing production-safe scripts without `sudo`

---
