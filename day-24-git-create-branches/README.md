---

# 🌿 Day 24: Create Git Branch

## 🧠 Problem Statement

The development team wants to implement new features without affecting the main codebase.

To achieve this, a **new branch** must be created from the `master` branch in the repository

```bash
/usr/src/kodekloudrepos/games
```

---

## 🎯 Objective

* Navigate to repository
* Create a new branch `xfusioncorp_games`
* Ensure it is based on `master`
* Do NOT modify any code

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Repository exists at `/usr/src/kodekloudrepos/games`
* Git installed
* Proper access to server

---

## 🛠️ Implementation Steps

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/games
```

---

## 2️⃣ Issue Faced: Dubious Ownership ❌

```bash
fatal: detected dubious ownership in repository
```

### 🔍 Reason

* Repository owned by another user
* Git security restriction prevents access

---

## 3️⃣ Fix: Mark Repository as Safe ✅

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

## 4️⃣ Check Existing Branches

```bash
git branch
```

👉 Output

```bash
* kodekloud_games
  master
```

---

## 5️⃣ Switch to Master Branch

```bash
git checkout master
```

---

## 6️⃣ Create New Branch

```bash
git checkout -b xfusioncorp_games
```

---

## 7️⃣ Verify Branch Creation

```bash
git branch
```

👉 Expected:

```bash
  kodekloud_games
  master
* xfusioncorp_games
```

---

## 🧪 Verification

```bash
git status
```

👉 Output:

```bash
On branch xfusioncorp_games
nothing to commit, working tree clean
```

---

## 🔍 Troubleshooting

### Dubious ownership error:

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

### Wrong branch selected:

```bash
git checkout master
```

---

### Verify current branch:

```bash
git branch
```

---

## 💡 Key Learnings

* Git branch creation workflow
* Importance of creating branch from correct base (`master`)
* Git security feature: **safe.directory**
* Handling permission-related Git issues
* Difference between `git branch` and `git checkout -b`

---

## 🌿 Git Workflow

```bash
master → create branch → develop → merge
```

---

## 🏁 Final Outcome

* Repository accessed successfully
* Security issue resolved
* New branch `xfusioncorp_games` created
* No code changes made

---

## 🚀 Summary

Created a new Git branch from master after resolving a real-world Git security issue (dubious ownership), ensuring safe and isolated feature development.

---
