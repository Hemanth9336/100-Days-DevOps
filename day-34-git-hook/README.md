---

# 🪝 Day 34: Git Hooks (Post-Update Hook)

## 🧠 Problem Statement

The development team is working on a repository

```bash
/opt/cluster.git
```

Cloned at

```bash
/usr/src/kodekloudrepos/cluster
```

### Requirements

1. Merge `feature` branch into `master`
2. Create a **post-update Git hook**
3. On every push to `master`, automatically create a release tag

   ```
   release-YYYY-MM-DD
   ```
4. Test the hook by pushing changes
5. Do NOT modify permissions

---

## 🎯 Objective

* Merge feature → master
* Automate tagging using Git hook
* Ensure tag is created on push
* Push all changes to remote

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname | User    | Purpose        |
| -------------- | -------- | ------- | -------------- |
| Storage Server | ststor01 | natasha | Git Operations |

---

## ⚙️ Prerequisites

* Git installed
* Repository exists
* Feature branch available
* Access as `natasha` user

---

## 🧠 What is a Git Hook?

Git hooks are scripts that run automatically on certain Git events.

👉 In this task:

* We use **post-update hook**
* Triggered after a successful push
* Used to automate tagging

---

## 🛠️ Implementation Steps

---

## 1️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/cluster
```

---

## 2️⃣ Fix Safe Directory Issue (if needed)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/cluster
```

---

## 3️⃣ Merge Feature Branch into Master

```bash
git checkout master
git merge feature
```

---

## 4️⃣ Navigate to Bare Repository Hooks Directory

```bash
cd /opt/cluster.git/hooks
```

---

## 5️⃣ Create Post-Update Hook

```bash
vi post-update
```

---

## 6️⃣ Add Below Script

```bash
#!/bin/bash

while read oldrev newrev refname
do
    branch=$(echo $refname | sed 's|refs/heads/||')

    if [ "$branch" == "master" ]; then
        tag="release-$(date +%F)"
        git tag $tag $newrev
    fi
done
```

---

## 7️⃣ Make Hook Executable

```bash
chmod +x post-update
```

---

## 8️⃣ Push Changes to Trigger Hook

```bash
cd /usr/src/kodekloudrepos/cluster
git push origin master
```

---

## 9️⃣ Verify Tag Creation

```bash
cd /opt/cluster.git
git tag
```

👉 Expected output

```bash
release-YYYY-MM-DD
```

---

## 🧪 Testing

* Push to `master`
* Verify tag is created automatically
* Ensure correct date format

---

## 🚨 Troubleshooting

### Hook not executing

```bash
chmod +x /opt/cluster.git/hooks/post-update
```

---

### Wrong path issue

Ensure:

```bash
/opt/cluster.git/hooks/post-update
```

---

### Tag not created

```bash
git tag
```

Check script syntax

---

### Safe directory issue

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/cluster
```

---

## 🔍 Key Concepts

| Concept     | Description                    |
| ----------- | ------------------------------ |
| Git Hook    | Script triggered by Git events |
| post-update | Runs after push                |
| Tagging     | Marking release versions       |
| Automation  | Eliminates manual tagging      |

---

## 💡 Key Learnings

* How Git hooks automate workflows
* Working with server-side hooks
* Automating release tagging
* Importance of executable scripts
* Real-world CI/CD-like behavior

---

## 🔁 Workflow

```bash
feature → merge → push → hook triggers → tag created
```

---

## 🏁 Final Outcome

* Feature branch merged into master
* Post-update hook configured
* Automatic release tag created
* Changes successfully pushed

---

## 🚀 Summary

Implemented a **Git post-update hook** to automate release tagging on every push to master — simulating real-world CI/CD automation and improving workflow efficiency.

---
