---

# ↩️ Day 27: Git Revert Changes

## 🧠 Problem Statement

The development team reported issues with the latest commit in the repository:

```bash
/usr/src/kodekloudrepos/beta
```

They requested to **revert the latest commit (HEAD)** and restore the repository to the previous stable state (initial commit).

---

## 🎯 Objective

* Revert latest commit (`HEAD`)
* Restore previous state (initial commit)
* Use commit message: `revert beta`

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Repository exists at `/usr/src/kodekloudrepos/beta`
* Git installed

---

## 🛠️ Implementation Steps

> ⚠️ Performed on **Storage Server (ststor01)**

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/beta
```

---

## 2️⃣ Check Repository Status

```bash
git status
```

👉 Observed:

* On branch `master`
* Untracked file: `beta.txt`

---

## 3️⃣ Check Commit History

```bash
git log --oneline
```

👉 Output:

```bash
4dfb080 add data.txt file
2f4bb96 initial commit
```

---

## 4️⃣ Verify Previous Commit (Initial State)

```bash
git checkout 2f4bb96
```

👉 Result:

* Entered **detached HEAD state**
* Verified initial commit

```bash
git log --oneline
```

```bash
2f4bb96 initial commit
```

---

## 5️⃣ Switch Back to Master

```bash
git checkout master
```

---

## 6️⃣ Revert Latest Commit

```bash
git revert HEAD
```

👉 Commit message used:

```bash
revert beta
```

👉 Output:

```bash
Revert "add data.txt file" revert beta
```

---

## 7️⃣ Verify Revert

```bash
git log --oneline
```

👉 Final output:

```bash
79d9bfb Revert "add data.txt file" revert beta
4dfb080 add data.txt file
2f4bb96 initial commit
```

---

## 🧪 Verification

```bash
git status
```

👉 Output:

```bash
nothing to commit, working tree clean
```

---

## 🚨 Observations (Important)

* Untracked file `beta.txt` remains unaffected
* Revert only impacted committed changes
* History is preserved (no deletion of commits)

---

## 🔍 Troubleshooting

### Detached HEAD state:

```bash
git checkout master
```

---

### Verify commits:

```bash
git log --oneline
```

---

### Safe directory issue (if occurs):

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/beta
```

---

## 💡 Key Learnings

* Difference between `git revert` and `git checkout`
* Safe way to undo commits without losing history
* Understanding detached HEAD state
* Importance of verifying commit history before revert
* Real-world rollback scenario

---

## 🔁 Git Revert Workflow

```bash
latest commit → revert → new commit created → history preserved
```

---

## 🏁 Final Outcome

* Latest commit successfully reverted
* New commit created with message `revert beta`
* Repository restored to previous state
* Commit history preserved

---

## 🚀 Summary

Reverted a faulty commit using Git revert, preserving history and safely restoring the repository to a stable state — a common real-world DevOps scenario.

---
