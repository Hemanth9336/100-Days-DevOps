---

# 🔥 Day 30: Git Hard Reset

## 🧠 Problem Statement

The development team used the repository

```bash
/usr/src/kodekloudrepos/beta
```

for testing purposes and pushed multiple commits.

Now, they want to

* Clean commit history
* Keep only

  * `initial commit`
  * `add data.txt file`
* Remove all later commits
* Update remote repository accordingly

---

## 🎯 Objective

* Reset repository to a specific commit
* Remove unwanted commits permanently
* Ensure only **2 commits remain**
* Push updated history to remote

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Git installed
* Repository exists at `/usr/src/kodekloudrepos/beta`
* Proper permissions to push changes

---

## ⚠️ Important Concept

> 🔴 `git reset --hard` rewrites history and deletes commits permanently
> Use carefully in shared environments

---

## 🛠️ Implementation Steps

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/beta
```

---

## 2️⃣ Check Commit History

```bash
git log --oneline
```

👉 Example output

```bash
79d9bfb revert beta
4dfb080 add data.txt file
2f4bb96 initial commit
```

---

## 3️⃣ Identify Target Commit

We need to reset to

```bash
add data.txt file
```

👉 Commit hash

```bash
4dfb080
```

---

## 4️⃣ Perform Hard Reset

```bash
git reset --hard 4dfb080
```

👉 Result

* HEAD moved to `add data.txt file`
* All newer commits removed locally

---

## 5️⃣ Verify Commit History

```bash
git log --oneline
```

👉 Output:

```bash
4dfb080 add data.txt file
2f4bb96 initial commit
```

✅ Only 2 commits remain

---

## 6️⃣ Force Push Changes to Remote

```bash
git push origin master --force
```

👉 Why force?

* Remote still has old commits
* History must be overwritten

---

## 🧪 Verification

```bash
git log --oneline
```

👉 Confirm only

```bash
add data.txt file
initial commit
```

---

## 🚨 Troubleshooting

### If push is rejected

```bash
git push origin master --force
```

---

### If repo shows unsafe directory

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/beta
```

---

### Check remote

```bash
git remote -v
```

---

## 🔍 Key Differences

| Command            | Behavior                    |
| ------------------ | --------------------------- |
| `git revert`       | Safe, keeps history         |
| `git reset --soft` | Keeps changes staged        |
| `git reset --hard` | Deletes commits + changes ❗ |

---

## 💡 Key Learnings

* How to clean Git history using hard reset
* Difference between revert vs reset
* Importance of force push after history rewrite
* Risks of rewriting shared repository history
* Real-world cleanup scenarios

---

## 🔁 Git Reset Workflow

```bash
latest commits ❌ → reset --hard → clean history → force push → updated remote
```

---

## 🏁 Final Outcome

* Repository reset to desired commit
* Only 2 commits retained
* Unwanted history removed
* Remote repository updated successfully

---

## 🚀 Summary

Used **git reset --hard** to clean up commit history and restore repository to a specific stable point — a powerful but risky operation often used in controlled environments.

---
