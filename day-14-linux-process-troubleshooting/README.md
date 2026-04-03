---

# 🔧 Day 14: Linux Process Troubleshooting – Apache Service (Port Conflict Fix)

## 🧠 Problem Statement

The monitoring system reported that **Apache service is unavailable on one of the application servers** in Stratos Datacenter.

We need to -

* Identify the faulty server
* Fix Apache service issue
* Ensure Apache is running on **all app servers**
* Configure Apache to run on **port 8082**

---

## 🎯 Objective

* Troubleshoot Apache failure
* Resolve port conflict issue
* Ensure Apache runs on port **8082** on all servers
* Verify service availability

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname | User   | Purpose     |
| -------------------- | -------- | ------ | ----------- |
| Application Server 1 | stapp01  | tony   | App hosting |
| Application Server 2 | stapp02  | steve  | App hosting |
| Application Server 3 | stapp03  | banner | App hosting |

---

## 🚨 Issue Identified

On **stapp01**, Apache failed to start:

```bash
(98) Address already in use
no listening sockets available
```

### 🔍 Root Cause

```bash
127.0.0.1:8082
```

* Port **8082 was already occupied by another process**
* Bound to **localhost (127.0.0.1)**
* Apache could not bind → service failed

---

## 🛠️ Final Fix (Step-by-Step)

> ⚠️ Perform on affected server (stapp01)

---

### 1️⃣ Identify Port Usage

```bash
ss -tulnp | grep 8082
```

---

### 2️⃣ Kill Process Using Port (Run as root)

```bash
sudo fuser -k 8082/tcp
```

---

### 3️⃣ Verify Port is Free

```bash
ss -tulnp | grep 8082
```

👉 Expected:

```bash
(no output)
```

---

### 4️⃣ Configure Apache Port

Edit config:

```bash
vi /etc/httpd/conf/httpd.conf
```

Ensure:

```bash
Listen 8082
```

❗ Remove old entries:

```bash
#Listen 80
#Listen 8080
```

---

### 5️⃣ Validate Configuration

```bash
httpd -t
```

---

### 6️⃣ Restart Apache

```bash
systemctl restart httpd
systemctl enable httpd
```

---

### 7️⃣ Verify Service

```bash
systemctl status httpd
```

👉 Expected:

```bash
Active: active (running)
```

---

### 8️⃣ Verify Port Binding

```bash
ss -tulnp | grep 8082
```

👉 Expected:

```bash
0.0.0.0:8082 → httpd
```

---

### 9️⃣ Test Locally

```bash
curl http://localhost:8082
```

---

### 🔟 Test from Jump Host

```bash
curl http://stapp01:8082
```

---

## ⚠️ Important Notes

* ❌ Port must NOT be used by any other service
* ✅ Always run port-kill commands as root
* ✅ Apache must bind to `0.0.0.0`, not `127.0.0.1`

---

## 🔍 Debugging Commands Used

```bash
ss -tulnp
fuser -k 8082/tcp
systemctl status httpd
httpd -t
journalctl -xeu httpd
curl http://localhost:8082
```

---

## 💡 Key Learnings

* Identifying port conflicts in Linux
* Understanding binding (`127.0.0.1` vs `0.0.0.0`)
* Importance of root permissions in process management
* Troubleshooting service startup failures
* Validating service health and accessibility

---

## 🏁 Final Outcome

* Apache successfully running on **all app servers**
* Configured on **port 8082**
* Port conflict resolved
* Service accessible successfully

---

## 🚀 Summary

Resolved Apache service failure by identifying port conflicts, freeing the occupied port, and ensuring proper configuration and service restart.

---
