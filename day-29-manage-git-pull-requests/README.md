---


# 🚀 Day 29 – Managing Git Pull Requests (PR)


## 📌 Objective


Ensure code quality and review process by **preventing direct pushes to the `master` branch** and enforcing changes via **Pull Requests (PRs)**.


---


## 🧠 Scenario


Max has added a new story (`The Fox and Grapes 🦊🍇`) in a feature branch.
We need to:


* Verify repository contents
* Create a Pull Request
* Assign a reviewer
* Approve and merge changes


---


## 🛠️ Task Breakdown


### 🔐 Step 1: Access Storage Server


Login using SSH


```bash
ssh max@ststor01
# Password: [Credentials]
```


Navigate to Max’s home directory and locate the cloned repository.


---


### 📂 Step 2: Verify Repository Contents


Check available files


```bash
ls
```


View commit history:\


```bash
git log
```


✅ Validate


* Author name (Max / Sarah)
* Commit messages
* Branch history


---

Optional
