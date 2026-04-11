---

# 📥 Day 22: Clone Git Repository on Storage Server

## 🧠 Problem Statement

The DevOps team has already created a Git repository, and now the development team requires a **local copy of this repository** on the Storage Server.

We need to

* Clone an existing repository
* Ensure no modifications are made to the original repository
* Perform the task using the correct user

---

## 🎯 Objective

* Clone repository from `/opt/games.git`
* Destination directory: `/usr/src/kodekloudrepos`
* Perform operation as user `natasha`
* Avoid any permission or structural changes

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Git must be installed on the server
* Access to Storage Server (`ststor01`)
* Proper permissions for user `natasha`
* Source repository must exist

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **Storage Server (ststor01)** as user `natasha`

---

### 1️⃣ Login to Storage Server

```bash
ssh natasha@ststor01
```

---

### 2️⃣ Verify Repository Exists

```bash
ls -ld /opt/games.git
```

👉 Ensure the repository is present

---

### 3️⃣ Create Destination Directory (if not exists)

```bash
mkdir -p /usr/src/kodekloudrepos
```

---

### 4️⃣ Clone the Repository

```bash
git clone /opt/games.git /usr/src/kodekloudrepos
```

---

## 🧪 Verification

```bash
ls -l /usr/src/kodekloudrepos
```

👉 Expected:

* Repository files cloned successfully

---

### Check Git status:

```bash
cd /usr/src/kodekloudrepos
git status
```

👉 Expected:

```bash
On branch main/master
nothing to commit, working tree clean
```

---

## 🚫 Important Notes

* ❌ Do NOT change permissions
* ❌ Do NOT modify repository content
* ❌ Do NOT use root user
* ✅ Use only `natasha` user
* ✅ Clone exactly to `/usr/src/kodekloudrepos`

---

## 🔍 Troubleshooting

### Git not installed:

```bash
git --version
```

---

### Permission denied:

```bash
ls -ld /usr/src
```

👉 Ensure user has access

---

### Repository not found:

```bash
ls /opt/
```

---

## 💡 Key Learnings

* Cloning repositories from local paths
* Difference between bare repo and working copy
* Importance of user permissions in Git operations
* Safe handling of production repositories
* Foundation for CI/CD workflows

---

## 🏁 Final Outcome

* Repository cloned successfully
* No changes made to original repository
* Working copy available at `/usr/src/kodekloudrepos`

---

## 🚀 Summary

Cloned a Git repository from a local bare repository to create a working copy for development purposes, ensuring proper user access and no unintended modifications.

---
