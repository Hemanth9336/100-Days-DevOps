---

# 🚀 Day 28 Git Cherry-Pick

## 📌 Task Overview

The Nautilus development team is working on a repository

```bash
/opt/apps.git
```

Cloned at

```bash
/usr/src/kodekloudrepos/apps
```

### 🧩 Requirement

* Two branches

  * `master`
  * `feature`

* A developer wants to move **only one specific commit** to `master`

* Target commit message

```bash
Update info.txt
```

* Push the final changes to remote

---

## 🛠️ Step-by-Step Execution

### 🔹 1. Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/apps
```

---

### 🔹 2. Verify Files

```bash
ls -l
```

Files present

* `info.txt`
* `welcome.txt`

Check content

```bash
cat info.txt
```

Output

```
Welcome to xFusionCorp Industries!
```

---

### 🔹 3. Check Branches

```bash
git branch
```

Output

```
* feature
  master
```

---

### 🔹 4. Identify Required Commit

```bash
git log --oneline
```

Output

```
3f5ed40 Update welcome.txt
3f98248 Update info.txt   ✅ (Target Commit)
1d06d43 Add welcome.txt
0d48d52 initial commit
```

---

### 🔹 5. Switch to Master Branch

```bash
git checkout master
```

---

### 🔹 6. Cherry-Pick the Commit

```bash
git cherry-pick 3f98248
```

Output

```
[master 72d85aa] Update info.txt
1 file changed, 1 insertion(+), 1 deletion(-)
```

---

### 🔹 7. Push Changes

```bash
git push origin master
```

Output

```
To /opt/apps.git
   1d06d43..72d85aa  master -> master
```

---

## ✅ Final Verification

### 🔸 Check Files

```bash
ls -l
```

```bash
cat info.txt
```

Output

```
Welcome to xFusionCorp Industries!
```

---

### 🔸 Verify Commit History

```bash
git log --oneline
```

Output

```
72d85aa Update info.txt   ✅ (Cherry-picked)
1d06d43 Add welcome.txt
0d48d52 initial commit
```

---

## 🎯 Result

* Successfully cherry-picked only required commit
* Avoided merging incomplete feature branch
* Changes pushed to remote repository
* Clean Git history maintained

---

## 🧠 Key Learnings

### 🔹 What is Cherry-Pick

* Applies a **specific commit** from one branch to another

### 🔹 Why Use It

* Selective changes
* Avoid full branch merge
* Useful for hotfixes and partial deployments

---

## ⚠️ Common Issues

| Issue          | Solution                                                      |
| -------------- | ------------------------------------------------------------- |
| Merge conflict | Resolve manually → `git add .` → `git cherry-pick --continue` |
| Wrong commit   | Use `git log --oneline` carefully                             |
| Push rejected  | Pull latest changes → retry push                              |

---

## 🏗️ Infrastructure Snapshot

| Server         | Hostname | Purpose        |
| -------------- | -------- | -------------- |
| Storage Server | ststor01 | Repo hosting   |
| Jenkins Server | jenkins  | CI/CD          |
| DB Server      | stdb01   | Database       |
| LB Server      | stlb01   | Load balancing |

---

## 📎 Summary

This task demonstrates

* Practical use of `git cherry-pick`
* Working with branches safely
* Maintaining clean production-ready history

---
