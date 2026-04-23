---

# 🔄 Day 32: Git Rebase

## 🧠 Problem Statement

The development team is working on a repository

```bash
/opt/games.git
```

Cloned at

```bash
/usr/src/kodekloudrepos/games
```

A developer is working on a **feature branch**, while new changes have already been pushed to the `master` branch.

👉 Requirement

* Update feature branch with latest `master` changes
* Do NOT create a merge commit
* Do NOT lose feature branch work

---

## 🎯 Objective

* Rebase feature branch onto latest `master`
* Maintain clean commit history
* Avoid merge commits
* Push updated branch to remote

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Repository exists at `/usr/src/kodekloudrepos/games`
* Git installed
* Feature branch already present

---

## 🧠 What is Git Rebase?

👉 Rebase moves your feature branch **on top of latest master**

Instead of:

```bash
merge → creates extra commit
```

Rebase:

```bash
replays commits → clean history
```

---

## 🛠️ Implementation Steps

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/games
```

---

## 2️⃣ Fix Safe Directory Issue (if needed)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

## 3️⃣ Check Branches

```bash
git branch
```

👉 Example

```bash
* feature
  master
```

---

## 4️⃣ Switch to Feature Branch

```bash
git checkout feature
```

---

## 5️⃣ Pull Latest Changes from Master

```bash
git fetch origin
```

---

## 6️⃣ Rebase Feature Branch onto Master

```bash
git rebase origin/master
```

---

## 🚨 If Conflict Occurs

### Resolve conflicts manually, then

```bash
git add .
git rebase --continue
```

---

### To abort rebase (if needed)

```bash
git rebase --abort
```

---

## 7️⃣ Verify History

```bash
git log --oneline
```

👉 History will be linear (no merge commits)

---

## 8️⃣ Push Changes to Remote

```bash
git push origin feature --force
```

👉 ⚠️ Force push required because history changed

---

## 🧪 Verification

```bash
git log --oneline --graph
```

👉 Clean linear history expected

---

## 🔍 Troubleshooting

### Safe directory issue

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

### Rebase conflict

```bash
git status
```

Fix → `git add` → `git rebase --continue`

---

### Push rejected

```bash
git push origin feature --force
```

---

## 🔁 Rebase vs Merge

| Feature  | Rebase          | Merge             |
| -------- | --------------- | ----------------- |
| History  | Linear          | Non-linear        |
| Commits  | No extra commit | Adds merge commit |
| Use case | Clean history   | Preserve context  |

---

## 💡 Key Learnings

* Clean Git history using rebase
* Difference between rebase and merge
* Handling conflicts during rebase
* Importance of force push after rebase
* Real-world Git workflow for feature branches

---

## 🔄 Git Rebase Workflow

```bash
feature branch → rebase on master → resolve conflicts → push
```

---

## 🏁 Final Outcome

* Feature branch successfully rebased
* Latest master changes included
* No merge commit created
* Clean commit history maintained

---

## 🚀 Summary

Rebased a feature branch onto the latest master to maintain a clean and linear commit history without creating unnecessary merge commits — a common practice in modern DevOps workflows.

---
