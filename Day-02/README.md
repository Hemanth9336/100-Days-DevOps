# 📅 Day 2: Create User with Expiry Date (Linux)

---

## 🧠 Task

Create a temporary user named `yousuf` on **App Server 1** with an expiry date.

---

## 🏢 Infrastructure Details

| Server       | Hostname | User   | Purpose                |
| ------------ | -------- | ------ | ---------------------- |
| App Server 1 | stapp01  | tony   | Nautilus Application 1 |
| App Server 2 | stapp02  | steve  | Nautilus Application 2 |
| App Server 3 | stapp03  | banner | Nautilus Application 3 |

---

## 🎯 Objective

* Create user: `yousuf`
* Ensure username is **lowercase**
* Set expiry date: `2027-03-28`

---

## 🚀 Steps to Execute

### 1. Connect to Server

```bash
ssh tony@stapp01
```

---

### 2. Switch to Root

```bash
sudo su -
```

---

### 3. Create User with Expiry Date

```bash
useradd -e 2027-03-28 yousuf
```

---

### 4. Verify User Expiry

```bash
chage -l yousuf
```

Expected Output (partial):

```
Account expires : Mar 28, 2027
```

---

## 💡 What I Learned Today

### Creating Users with Expiry Date

Linux allows setting an expiration date for users, which is useful for temporary access.

### Importance of Temporary Users

Temporary accounts help in managing short-term access securely without manual cleanup.

### Account Expiry Management

Using tools like `chage`, we can verify and manage password and account expiry details.

---

## 🛠️ What I Built / Practiced

* Connected to Application Server (`stapp01`)
* Created a temporary user `yousuf`
* Set an expiry date for the account
* Verified expiry using `chage`

---

## ⚠️ Challenges

* Remembering the correct command option for expiry (`-e`)
* Date format confusion (`YYYY-MM-DD`)

---

## 🔧 Fix / Learning

* Learned correct syntax: `useradd -e YYYY-MM-DD`
* Understood how Linux handles account expiration

---

## 🧩 Key Takeaway

Temporary user accounts improve security and simplify access management.

---

## 🧩 Summary

```bash
Create a user 'yousuf' with expiry date 2027-03-28 on stapp01
```

---

## ✅ Outcome

Successfully created a temporary user with controlled access duration.
