````markdown
# 🚀 Day 28 – Git Cherry-Pick

## 📌 Objective
Apply a **specific commit** from one branch to another without merging the entire branch.

---

## 🧠 Scenario
- Repository: `/opt/apps.git`  
- Local path: `/usr/src/kodekloudrepos/apps`  
- Branches: `feature`, `master`  
- Target commit: **"Update info.txt"**  

---

## 🛠️ Steps

### 🔹 1. Navigate to Repo
```bash
cd /usr/src/kodekloudrepos/apps
````

---

### 🔹 2. Verify Files

```bash
ls
cat info.txt
```

---

### 🔹 3. Check Branches

```bash
git branch
```

---

### 🔹 4. Find Commit

```bash
git log --oneline
```

Target commit: `Update info.txt`

---

### 🔹 5. Switch to Master

```bash
git checkout master
```

---

### 🔹 6. Cherry-Pick Commit

```bash
git cherry-pick <commit-id>
```

---

### 🔹 7. Push Changes

```bash
git push origin master
```

---

## 🎉 Result

* ✅ Selected commit applied to `master`
* ✅ No full branch merge required
* ✅ Clean commit history maintained

---

## 💡 Key Learnings

* Cherry-pick applies a **single commit**
* Useful for **hotfixes & selective updates**
* Helps avoid unnecessary merges

---

```
```
