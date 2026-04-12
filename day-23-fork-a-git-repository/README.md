---

# 🍴 Day 23: Fork a Git Repository (Gitea)

## 🧠 Problem Statement

A new developer **Jon** has joined the team and needs to start working on an existing project.

To begin development safely without affecting the original repository, he must **fork the repository** using the Gitea UI.

---

## 🎯 Objective

* Access Gitea UI
* Login as user `jon`
* Fork repository `sarah/story-blog`
* Create a personal copy under Jon’s account

---

## 🏗️ Infrastructure Details

| Service      | User | Purpose                   |
| ------------ | ---- | ------------------------- |
| Gitea Server | jon  | Git repository management |

---

## ⚙️ Prerequisites

* Access to Gitea UI (via browser)
* Valid credentials for user `jon`
* Repository `sarah/story-blog` must exist

---

## 🛠️ Implementation Steps

---

## 1️⃣ Open Gitea UI

* Click on **Gitea UI button** from the top bar
* OR open in browser:

```
http://<gitea-server-url>
```

---

## 2️⃣ Login to Gitea

* **Username:** `jon`
* **Password:** `[Credentials]`

---

## 3️⃣ Search for Repository

* In the search bar, type:

```
sarah/story-blog
```

* Open the repository

---

## 4️⃣ Fork the Repository

* Click on **"Fork"** button (top-right corner)
* Select user: `jon`
* Confirm fork

---

## 📁 Result

👉 A new repository will be created:

```
jon/story-blog
```

✔ This is a **copy of the original repo**
✔ Jon can safely make changes

---

## 🧪 Verification

* Navigate to Jon’s profile
* Check repositories

👉 Expected:

```
story-blog (forked from sarah/story-blog)
```

---

## 🔍 Troubleshooting

### Cannot find repository:

* Ensure correct name: `sarah/story-blog`

---

### Fork button not visible:

* Check login status
* Refresh page

---

### Login issues:

* Verify username/password

---

## 💡 Key Learnings

* Difference between **fork vs clone**
* Why forking is used in team workflows
* Safe development without affecting original code
* Role of Git UI tools like Gitea
* Foundation for pull request workflow

---

## 🔁 Fork vs Clone

| Feature   | Fork             | Clone       |
| --------- | ---------------- | ----------- |
| Location  | Server-side copy | Local copy  |
| Use case  | Collaboration    | Development |
| Ownership | New user         | Same repo   |

---

## 🏁 Final Outcome

* Repository successfully forked
* Jon has his own working copy
* Ready for development without affecting original repo

---

## 🚀 Summary

Forked a repository using Gitea UI to create an isolated development environment, enabling safe collaboration and independent code changes.

---
