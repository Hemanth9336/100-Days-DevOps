---

# 🔀 Day 25: Git Merge Branches

## 🧠 Problem Statement

The development team needs to

* Create a new branch
* Add a new file
* Commit changes
* Merge into master
* Push both branches to remote

---

## 🎯 Objective

* Create branch `datacenter` from `master`
* Copy `/tmp/index.html` into repo
* Add and commit the file
* Merge `datacenter` → `master`
* Push both branches to origin

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Repository exists at `/usr/src/kodekloudrepos/media`
* File `/tmp/index.html` available
* Git installed

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **Storage Server (ststor01)**

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/media
```

---

## 2️⃣ Fix Safe Directory Issue (if needed)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/media
```

---

## 3️⃣ Checkout Master Branch

```bash
git checkout master
```

---

## 4️⃣ Create New Branch

```bash
git checkout -b datacenter
```

---

## 5️⃣ Copy File

```bash
cp /tmp/index.html .
```

---

## 6️⃣ Add File

```bash
git add index.html
```

---

## 7️⃣ Commit Changes

```bash
git commit -m "Added index.html"
```

---

## 8️⃣ Push New Branch (CRITICAL STEP)

```bash
git push origin datacenter
```

👉 ⚠️ This step is mandatory — missing this will cause task failure

---

## 9️⃣ Switch to Master

```bash
git checkout master
```

---

## 🔟 Merge Branch

```bash
git merge datacenter
```

---

## 1️⃣1️⃣ Push Master

```bash
git push origin master
```

---

## 🧪 Verification

```bash
git branch
```

👉 Expected:

```
* master
  datacenter
```

---

```bash
git branch -r
```

👉 Expected:

```
origin/master
origin/datacenter
```

---

```bash
git log --oneline
```

👉 Should show commit from `datacenter`

---

## 🚨 Issue Faced (Important)

### ❌ Error:

```
required changes are not added or pushed to new branch
```

---

### 🔍 Root Cause

* Branch was created
* File was added and committed
* ❌ But new branch was NOT pushed

---

### ✅ Fix

```bash
git push origin datacenter
```

---

## 🔍 Troubleshooting

### Safe directory error:

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/media
```

---

### File missing:

```bash
ls /tmp/index.html
```

---

### Check commit:

```bash
git log --oneline
```

---

## 💡 Key Learnings

* Complete Git workflow (branch → commit → merge → push)
* Importance of pushing feature branches
* Difference between local and remote branches
* Handling real-world Git errors
* Git security (safe.directory)

---

## 🔀 Git Workflow

```
master → create branch → add → commit → push → merge → push
```

---

## 🏁 Final Outcome

* Branch `datacenter` created
* File added and committed
* Branch pushed to remote
* Changes merged into master
* Both branches successfully pushed

---

## 🚀 Summary

Completed a full Git workflow by creating a feature branch, committing changes, pushing the branch, merging into master, and resolving a real-world issue where missing branch push caused failure.

---
