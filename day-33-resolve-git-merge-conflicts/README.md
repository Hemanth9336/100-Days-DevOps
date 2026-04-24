---

# 🚀 Day 33 – Resolve Git Merge Conflicts

## 📌 Task Overview

In this task, two developers — **Sarah** and **Max** — were collaborating on a repository named

```
story-blog
```

Max attempted to push recent changes but encountered **merge conflicts** due to concurrent updates.

---

## 🧩 Problem Statement

* Repository located at

  ```
  /home/max/story-blog
  ```
* Max is unable to push changes due to conflicts with remote (`origin`)
* Required fixes:

  * Resolve merge conflicts
  * Ensure `story-index.txt` contains **titles of all 4 stories**
  * Fix typo:

    ```
    Mooose ❌ → Mouse ✅
    ```
* Changes must be successfully pushed to remote repository

---

## 🌐 Access Details

### 🔐 SSH Access

```bash
ssh max@ststor01
```

### 🖥️ Git UI Access

Platform: Gitea

* URL: (via UI button in lab)
* Credentials:

  * Username: `max` / `sarah`
  * Password: Provided in lab

---

## 🏗️ Infrastructure Details

| Server Name    | Hostname  | User    | Purpose           |
| -------------- | --------- | ------- | ----------------- |
| Storage Server | ststor01  | natasha | Stores repository |
| Jump Host      | jump-host | thor    | Secure access     |

---

## ⚙️ Steps to Resolve Merge Conflict

### 1️⃣ Navigate to Repository

```bash
cd /home/max/story-blog
```

---

### 2️⃣ Check Git Status

```bash
git status
```

---

### 3️⃣ Pull Latest Changes (Triggers Conflict)

```bash
git pull origin master
```

---

### 4️⃣ Identify Conflicted Files

```bash
git status
```

Look for files marked as

```
both modified
```

---

### 5️⃣ Open and Resolve Conflicts

Example conflict:

```text
<<<<<<< HEAD
The Lion and the Mooose
=======
The Lion and the Mouse
>>>>>>> origin/master
```

### ✅ Fix

```text
The Lion and the Mouse
```

---

### 6️⃣ Update `story-index.txt`

Ensure it contains all **4 story titles**.

Example:

```text
1. The Lion and the Mouse
2. Story Title 2
3. Story Title 3
4. Story Title 4
```

---

### 7️⃣ Mark Conflict as Resolved

```bash
git add .
```

---

### 8️⃣ Commit Changes

```bash
git commit -m "Resolved merge conflicts and fixed typo in story"
```

---

### 9️⃣ Push to Remote

```bash
git push origin master
```

---

## 📸 Verification

* Confirm changes in Gitea UI
* Ensure:

  * No merge conflicts remain
  * `story-index.txt` is correct
  * Typo is fixed

---

## 💡 Key Learnings

* Handling **Git merge conflicts**
* Understanding conflict markers:

  ```
  <<<<<<< HEAD
  =======
  >>>>>>> branch
  ```
* Importance of:

  * Pull before push
  * Reviewing conflicting changes carefully
* Maintaining clean and accurate repository data

---

## 🧠 Best Practices

* Always run:

  ```bash
  git pull origin master
  ```

  before making changes

* Use meaningful commit messages

* Communicate with team members to avoid conflicts

---

## 🎯 Outcome

✔ Successfully resolved merge conflicts
✔ Fixed typo in story
✔ Updated index file
✔ Changes pushed to remote repository

---
