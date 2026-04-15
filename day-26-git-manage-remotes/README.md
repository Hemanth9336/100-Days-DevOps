---

# 🔗 Day 26: Git Manage Remotes

## 🧠 Problem Statement

The development team introduced a new Git repository and requires updating remotes in an existing cloned repository.

Tasks include

* Adding a new remote
* Committing a new file
* Pushing changes to the new remote

---

## 🎯 Objective

* Add remote `dev_blog` → `/opt/xfusioncorp_blog.git`
* Copy `/tmp/index.html` into repo
* Add and commit changes to `master`
* Push `master` branch to new remote

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Repository exists at `/usr/src/kodekloudrepos/blog`
* File `/tmp/index.html` available
* Git installed

---

## 🛠️ Implementation Steps

> ⚠️ Performed on **Storage Server (ststor01)**

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/blog
```

---

## 2️⃣ Check Existing Remotes

```bash
git remote -v
```

👉 Output:

```bash
origin  /opt/blog.git (fetch)
origin  /opt/blog.git (push)
```

---

## 3️⃣ Add New Remote

```bash
git remote add dev_blog /opt/xfusioncorp_blog.git
```

---

## 4️⃣ Verify Remote

```bash
git remote -v
```

👉 Output:

```bash
dev_blog  /opt/xfusioncorp_blog.git (fetch)
dev_blog  /opt/xfusioncorp_blog.git (push)
origin    /opt/blog.git (fetch)
origin    /opt/blog.git (push)
```

---

## 5️⃣ Ensure Master Branch

```bash
git branch
```

👉 Output:

```bash
* master
```

---

## 6️⃣ Copy File into Repository

```bash
cp /tmp/index.html .
```

---

## 7️⃣ Check Status

```bash
git status
```

👉 Output:

```bash
Untracked files:
  index.html
```

---

## 8️⃣ Add File

```bash
git add .
```

---

## 9️⃣ Commit Changes

```bash
git commit -m "Add index.html"
```

👉 Output:

```bash
1 file changed, 10 insertions(+)
create mode 100644 index.html
```

---

## 🔟 Verify Commit Status

```bash
git status
```

👉 Output:

```bash
Your branch is ahead of 'origin/master' by 1 commit.
```

---

## 1️⃣1️⃣ Push to New Remote

```bash
git push dev_blog master
```

👉 Output:

```bash
[new branch] master -> master
```

---

## 🧪 Verification

### Check commit in remote repo

```bash
cd /opt/blog.git
git log --oneline
```

👉 Output:

```bash
initial commit
```

---

## 🚨 Issue Observed (Important)

Even after pushing to `dev_blog`, checking `/opt/blog.git` did NOT show the new commit.

---

## 🔍 Root Cause

* `/opt/blog.git` → linked to **origin**
* `/opt/xfusioncorp_blog.git` → linked to **dev_blog**

👉 Changes were pushed to **dev_blog**, not origin

---

## ✅ Correct Understanding

* `origin` ≠ `dev_blog`
* Each remote points to a **different repository**

---

## 🔍 Troubleshooting

### Check remotes

```bash
git remote -v
```

---

### Verify commits locally

```bash
git log --oneline
```

---

### Push to correct remote

```bash
git push dev_blog master
```

---

## 💡 Key Learnings

* Managing multiple Git remotes
* Difference between `origin` and custom remotes
* Understanding where code is pushed
* Local vs remote repository mapping
* Real-world debugging of Git push issues

---

## 🔗 Git Remote Workflow

```bash
add remote → commit → push to specific remote
```

---

## 🏁 Final Outcome

* Remote `dev_blog` added successfully
* File committed to `master`
* Changes pushed to new remote
* Understood difference between multiple remotes

---

## 🚀 Summary

Configured a new Git remote, committed changes, and pushed updates successfully while understanding how multiple remotes map to different repositories — a key real-world DevOps skill.

---
