---

# 📦 Day 31: Git Stash

## 🧠 Problem Statement

The development team was working on the repository

```bash
/usr/src/kodekloudrepos/blog
```

Some in-progress changes were **stashed earlier**, and now they want to

* Restore a specific stash → `stash@{1}`
* Commit the restored changes
* Push them to the remote repository

---

## 🎯 Objective

* Identify available stashes
* Restore `stash@{1}`
* Commit the changes
* Push to origin

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Git installed
* Repository exists at `/usr/src/kodekloudrepos/blog`
* Stash entries already present

---

## 🔍 What is Git Stash?

Git stash allows you to

* Save uncommitted changes temporarily
* Clean working directory
* Restore changes later when needed

---

## 🛠️ Implementation Steps

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/blog
```

---

## 2️⃣ Check Available Stashes

```bash
git stash list
```

👉 Example output:

```bash
stash@{0}: WIP on master
stash@{1}: WIP on master
```

---

## 3️⃣ Restore Required Stash

```bash
git stash apply stash@{1}
```

👉 Result:

* Changes from `stash@{1}` restored
* Stash entry remains intact

---

## 4️⃣ Verify Changes

```bash
git status
```

👉 Output:

* Modified / added files visible

---

## 5️⃣ Stage Changes

```bash
git add .
```

---

## 6️⃣ Commit Changes

```bash
git commit -m "Restore stashed changes"
```

---

## 7️⃣ Push Changes to Remote

```bash
git push origin master
```

---

## 🧪 Verification

```bash
git log --oneline
```

👉 Confirm new commit added

---

## 🚨 Troubleshooting

### If stash not found

```bash
git stash list
```

---

### If conflicts occur

```bash
# Resolve conflicts manually
git add .
git commit -m "Resolve stash conflicts"
```

---

### If repository marked unsafe

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/blog
```

---

## 🔍 Key Differences

| Command           | Behavior                       |
| ----------------- | ------------------------------ |
| `git stash`       | Save changes temporarily       |
| `git stash apply` | Restore without removing stash |
| `git stash pop`   | Restore and delete stash       |

---

## 💡 Key Learnings

* How to manage temporary work using stash
* Difference between `apply` and `pop`
* Importance of verifying stash before applying
* Handling conflicts after stash restore
* Real-world use case: switching tasks without losing work

---

## 🔁 Git Stash Workflow

```bash
work in progress → stash → switch task → apply stash → commit → push
```

---

## 🏁 Final Outcome

* Successfully restored `stash@{1}`
* Changes committed
* Repository updated on remote

---

## 🚀 Summary

Used **Git stash** to restore previously saved work and integrate it back into the repository — a common real-world scenario when handling interruptions or context switching in development.

---
