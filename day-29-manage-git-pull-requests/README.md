````markdown
# 🚀 Day 29 – Managing Git Pull Requests (PR)


## 📌 Objective
Enforce a proper Git workflow by **restricting direct pushes to the `master` branch** and ensuring all changes go through a **Pull Request (PR) with review and approval**.


---


## 🧠 Scenario
Max has written a new story **“The Fox and Grapes 🦊🍇”** and pushed it to a feature branch.


Goal:
- Verify repository and commit history  
- Create a Pull Request  
- Assign a reviewer  
- Approve and merge changes into `master`  


---


## 🛠️ Step-by-Step Implementation


### 🔐 1. SSH into Storage Server


```bash
ssh max@ststor01
# Password: [Credentials]
````


Navigate to the repository in Max's home directory.


---


### 📂 2. Verify Repository Contents


List files:


```bash
ls
```


Check commit history:


```bash
git log
```


✅ Validate:


* Author details (Max / Sarah)
* Commit messages
* Existing changes in repository


---


### 🌿 3. Verify Feature Branch


Max pushed changes to:


```
story/fox-and-grapes
```


Check branches:


```bash
git branch -a
```





