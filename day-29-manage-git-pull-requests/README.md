````markdown
# 🚀 Day 29 – Managing Git Pull Requests (PR)

## 📌 Objective
Restrict direct pushes to `master` and enforce changes through Pull Requests with review and approval.

---

## 🧠 Scenario
Max created a story **“The Fox and Grapes 🦊🍇”** in a feature branch.

Goal:
- Verify repo and commits  
- Create PR  
- Assign reviewer  
- Approve & merge into `master`  

---

## 🛠️ Steps

### 🔐 1. Connect to Server
```bash
ssh max@ststor01
````

---

### 📂 2. Verify Repository

```bash
ls
git log
```

---

### 🌿 3. Check Branch

```bash
git branch -a
```

Feature branch: `story/fox-and-grapes`

---

### 🔁 4. Create Pull Request

Login to Gitea:

```
Username: max
Password: [Credentials]
```

PR Details:

* Title: **Added fox-and-grapes story**
* Source: `story/fox-and-grapes`
* Target: `master`

---

### 👀 5. Add Reviewer

* Open PR
* Add **tom** as reviewer

---

### 🔄 6. Review & Merge

Login as:

```
Username: tom
Password: [Credentials]
```

* Review PR
* Approve
* Merge

---

## 🎉 Result

* ✅ Code merged to `master`
* ✅ Reviewed before merge
* ✅ Proper Git workflow followed

---

## 💡 Key Learnings

* Avoid direct pushes to `master`
* Use feature branches
* Use Pull Requests for changes
* Always review before merging

```
```
