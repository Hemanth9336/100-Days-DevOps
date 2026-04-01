---

# 🔧 Day 12: Linux Network Services – Troubleshooting Apache (Port 8084)

## 🧠 Problem Statement

The monitoring system reported that **Apache service is not reachable on port 8084** on one of the application servers in Stratos Datacenter.

Possible causes:

* Apache service not running
* Incorrect port configuration
* Port conflict
* Firewall blocking access
* Fix applied on wrong server

---

## 🎯 Objective

* Identify and fix the issue on **App Server 3 (stapp03)**
* Ensure Apache runs on **port 8084**
* Ensure accessibility from **Jump Host**
* Validate using:

```bash
curl http://stapp03:8084
```

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname  | User   | Purpose                       |
| -------------------- | --------- | ------ | ----------------------------- |
| Application Server 3 | stapp03   | banner | Hosts Apache service          |
| Jump Host            | jump-host | thor   | Used for testing connectivity |

---

## 🚨 Root Cause Identified

During troubleshooting:

* Apache was correctly configured ❌ but on **wrong server (stapp01)**
* Port 8084 was not properly set on **stapp03**
* Firewall rules were not allowing traffic

---

## 🛠️ Final Fix (Step-by-Step)

> ⚠️ Perform all steps on **stapp03**

---

### 1️⃣ Login to Correct Server

```bash
ssh banner@stapp03
```

---

### 2️⃣ Stop Conflicting Service (if running)

```bash
systemctl stop sendmail
systemctl disable sendmail
```

---

### 3️⃣ Configure Apache to Use Port 8084

```bash
vi /etc/httpd/conf/httpd.conf
```

Update:

```bash
Listen 8084
```

❗ Important:

```bash
# Comment/remove default port
#Listen 80
```

---

### 4️⃣ Validate Configuration

```bash
httpd -t
```

✅ Expected:

```bash
Syntax OK
```

---

### 5️⃣ Restart Apache

```bash
systemctl restart httpd
systemctl enable httpd
```

---

### 6️⃣ Allow Port in Firewall

```bash
iptables -I INPUT -p tcp --dport 8084 -j ACCEPT
```

---

### 7️⃣ Verify Apache is Listening

```bash
ss -tulnp | grep 8084
```

✅ Expected:

```bash
*:8084 → httpd
```

---

### 8️⃣ Test Locally

```bash
curl http://localhost:8084
```

---

### 9️⃣ Final Test from Jump Host

```bash
curl http://stapp03:8084
```

✅ Expected: Webpage response

---

## 🔍 Debugging Commands Used

```bash
ss -tulnp | grep 8084
systemctl status httpd
httpd -t
journalctl -u httpd
telnet stapp03 8084
curl http://stapp03:8084
```

---

## 🚫 Important Notes

* ❌ Do NOT modify `index.html`
* ✅ Ensure fix is applied on correct server (**stapp03**)
* ✅ Apache must bind to `0.0.0.0`
* ✅ Only required port should be open

---

## 💡 Key Learnings

* Importance of verifying the correct target server
* Troubleshooting service vs network vs firewall issues
* Identifying and resolving port conflicts
* Understanding service binding (`127.0.0.1` vs `0.0.0.0`)
* Using tools like `ss`, `telnet`, and `curl` effectively

---

## 🏁 Final Outcome

* Apache successfully running on **port 8084** on **stapp03**
* Firewall configured correctly
* Service accessible from Jump Host

```bash
curl http://stapp03:8084
```

---

## 🚀 Summary

Resolved Apache accessibility issue by identifying incorrect server configuration, fixing port settings, allowing firewall access, and ensuring proper deployment on the correct server.

---
