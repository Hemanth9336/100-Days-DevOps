---

# 🗃️ Day 21: Set Up Git Repository on Storage Server

## 🧠 Problem Statement

The development team requires a **central Git repository** to manage code for a new application.

We need to

* Install Git on the **Storage Server**
* Create a **bare repository** for collaboration

---

## 🎯 Objective

* Install Git using `yum`
* Create a bare repository at `/opt/cluster.git`

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose             |
| -------------- | -------- | ------- | ------------------- |
| Storage Server | ststor01 | natasha | Git Repository Host |

---

## ⚙️ Prerequisites

* Access to Storage Server (`ststor01`)
* Root or sudo privileges
* Internet access for package installation

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **Storage Server (ststor01)**

---

### 1️⃣ Login to Storage Server

```bash
ssh natasha@ststor01
sudo su -
```

---

### 2️⃣ Install Git

```bash
yum install git -y
```

---

### 3️⃣ Verify Installation

```bash
git --version
```

👉 Expected:

```bash
git version x.x.x
```

---

### 4️⃣ Create Bare Repository

```bash
mkdir -p /opt/cluster.git
cd /opt/cluster.git

git init --bare
```

---

## 📌 What is a Bare Repository?

* Does NOT contain working files
* Used as a **central remote repository**
* Developers can push/pull code

---

## 🧪 Verification

```bash
ls -l /opt/cluster.git
```

👉 Expected structure:

```bash
HEAD
branches
config
description
hooks
info
objects
refs
```

---

## 🚫 Important Notes

* Repository name must be exactly:

  ```bash
  /opt/cluster.git
  ```
* Use `--bare` flag (mandatory)
* Do not create a normal repo

---

## 🔍 Troubleshooting

### Git not installed:

```bash
yum install git -y
```

---

### Permission issues:

```bash
chown -R natasha:natasha /opt/cluster.git
```

---

### Check repo type:

```bash
git rev-parse --is-bare-repository
```

👉 Expected:

```bash
true
```

---

## 💡 Key Learnings

* Difference between **bare vs non-bare repositories**
* Setting up centralized version control
* Installing and verifying Git
* Repository structure and purpose
* Foundation for CI/CD workflows

---

## 🏁 Final Outcome

* Git successfully installed
* Bare repository `/opt/cluster.git` created
* Ready for team collaboration

---

## 🚀 Summary

Set up a centralized Git bare repository on the storage server to enable collaborative development and version control for applications.

---
