# 🚀 Day 6: Create a Cron Job

## 📌 Task Overview

The Nautilus system admins team wants to automate daily tasks using cron jobs across all application servers in Stratos DC.

Before deploying real scripts, a sample cron job needs to be tested.

---

## 🎯 Objective

Perform the following steps on **all app servers**:

1. Install `cronie` package
2. Start and enable `crond` service
3. Add a cron job for the root user to run every 5 minutes

---

## 🖥️ Infrastructure Details

| Server Name          | Hostname | User   | Password | Purpose                      |
| -------------------- | -------- | ------ | -------- | ---------------------------- |
| Application Server 1 | stapp01  | tony   | Ir0nM@n  | Hosts Nautilus Application 1 |
| Application Server 2 | stapp02  | steve  | Am3ric@  | Hosts Nautilus Application 2 |
| Application Server 3 | stapp03  | banner | BigGr33n | Hosts Nautilus Application 3 |

---

## ⚙️ Step-by-Step Implementation

### 🔹 1. SSH into Each Server

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

---

### 🔹 2. Switch to Root User

```bash
sudo su -
```

---

### 🔹 3. Install `cronie` Package

```bash
yum install cronie -y
```

> 💡 For Ubuntu/Debian systems:

```bash
apt install cron -y
```

---

### 🔹 4. Start and Enable Cron Service

```bash
systemctl start crond
systemctl enable crond
```

---

### 🔹 5. Add Cron Job for Root User

Open crontab:

```bash
crontab -e
```

Add the following line:

```bash
*/5 * * * * echo hello > /tmp/cron_text
```

---

## ⏰ Cron Job Explanation

| Field | Value           |
| ----- | --------------- |
| */5   | Every 5 minutes |
| *     | Every hour      |
| *     | Every day       |
| *     | Every month     |
| *     | Every weekday   |

👉 This job runs every **5 minutes** and writes `hello` into `/tmp/cron_text`

---

## ✅ Verification

Check if cron job is working:

```bash
cat /tmp/cron_text
```

You should see:

```
hello
```

---

## 🔍 Troubleshooting

If not working:

```bash
systemctl status crond
```

Check logs:

```bash
journalctl -u crond
```

---

## 💡 Key Takeaways

✔ Cron jobs automate repetitive tasks
✔ `cronie` package manages cron service
✔ Always verify cron jobs after setup
✔ Root user cron ensures system-level execution

---

## 📅 Summary

* Installed cron service on all servers
* Enabled background scheduling
* Created a test cron job running every 5 minutes
* Verified successful execution

---

⭐ **Keep Learning DevOps — One Day at a Time!**
