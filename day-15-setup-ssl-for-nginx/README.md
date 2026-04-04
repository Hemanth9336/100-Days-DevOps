---

# 🔐 Day 15: Setup SSL for Nginx (HTTPS Configuration)

## 🧠 Problem Statement

The system admin team needs to prepare **App Server 2** for application deployment by configuring a secure web server using **Nginx with SSL**.

We are provided with -

* A self-signed certificate
* A private key

---

## 🎯 Objective

* Install and configure **Nginx**
* Configure **SSL (HTTPS)** using provided certificate
* Serve a simple webpage
* Validate secure access from Jump Host

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname  | User  | Purpose        |
| -------------------- | --------- | ----- | -------------- |
| Application Server 2 | stapp02   | steve | Nginx hosting  |
| Jump Host            | jump-host | thor  | Testing access |

---

## 📁 Provided Files

| File            | Location            |
| --------------- | ------------------- |
| SSL Certificate | `/tmp/nautilus.crt` |
| SSL Key         | `/tmp/nautilus.key` |

---

## ⚙️ Prerequisites

* Root or sudo access on **stapp02**
* Network access from jump host

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **stapp02**

---

### 1️⃣ Install Nginx

```bash
yum install nginx -y
```

---

### 2️⃣ Start and Enable Nginx

```bash
systemctl start nginx
systemctl enable nginx
```

---

### 3️⃣ Move SSL Certificate and Key

```bash
mkdir -p /etc/nginx/ssl

mv /tmp/nautilus.crt /etc/nginx/ssl/
mv /tmp/nautilus.key /etc/nginx/ssl/
```

---

### 4️⃣ Create Index Page

```bash
echo "Welcome!" > /usr/share/nginx/html/index.html
```

---

### 5️⃣ Configure Nginx for SSL

Edit configuration file:

```bash
vi /etc/nginx/nginx.conf
```

---

### 🔽 Add/Update Server Block

```nginx
server {
    listen              443 ssl;
    server_name         stapp02;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    location / {
        root   /usr/share/nginx/html;
        index  index.html;
    }
}
```

---

### 6️⃣ Validate Configuration

```bash
nginx -t
```

👉 Expected:

```bash
syntax is ok
test is successful
```

---

### 7️⃣ Restart Nginx

```bash
systemctl restart nginx
```

---

## 🧪 Verification

### From Jump Host

```bash
curl -Ik https://stapp02
```

👉 Expected:

* `HTTP/1.1 200 OK`
* SSL connection established

---

## 🚫 Important Notes

* Self-signed certificate may show warning (expected)
* Ensure correct SSL file paths
* No firewall changes required for this setup

---

## 💡 Key Learnings

* Installing and configuring Nginx
* Setting up HTTPS using SSL certificates
* Understanding Nginx server blocks
* Handling file permissions and secure locations
* Testing HTTPS endpoints using curl

---

## 🏁 Final Outcome

* Nginx successfully installed and running
* SSL configured using provided certificate
* Secure HTTPS access enabled
* Webpage accessible via:

```bash
https://stapp02
```

---

## 🚀 Summary

Configured Nginx with SSL to enable secure HTTPS communication, ensuring encrypted and secure application access.

---
