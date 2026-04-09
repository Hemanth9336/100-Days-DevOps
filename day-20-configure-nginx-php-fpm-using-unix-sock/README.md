---

# ⚙️ Day 20: Configure Nginx + PHP-FPM Using Unix Socket

## 🧠 Problem Statement

The development team is deploying a **PHP-based application** on **App Server 1** and requires a properly configured environment using

* **Nginx (web server)**
* **PHP-FPM 8.1 (application processor)**
* Communication via **Unix socket**

---

## 🎯 Objective

* Install and configure **Nginx on port 8098**
* Set document root to `/var/www/html`
* Install **PHP-FPM 8.1**
* Configure PHP-FPM to use Unix socket `/var/run/php-fpm/default.sock`
* Integrate Nginx with PHP-FPM
* Verify PHP application

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname | User | Purpose              |
| -------------------- | -------- | ---- | -------------------- |
| Application Server 1 | stapp01  | tony | PHP Application Host |

---

## 📁 Application Files

| File      | Location        |
| --------- | --------------- |
| index.php | `/var/www/html` |
| info.php  | `/var/www/html` |

> ⚠️ Do NOT modify these files

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **App Server 1 (stapp01)**

---

## 1️⃣ Install Nginx

```bash
yum install nginx -y
```

---

## 2️⃣ Configure Nginx (Port + PHP + Upstream)

```bash
vi /etc/nginx/nginx.conf
```

---

### 🔽 Updated Configuration (with Upstream)

```nginx
# PHP-FPM upstream using Unix socket
upstream php-fpm {
    server unix:/var/run/php-fpm/default.sock;
}

server {
    listen       8098;
    server_name  stapp01;

    root   /var/www/html;
    index  index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include        fastcgi_params;
        fastcgi_pass   php-fpm;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    }
}
```

---

## 3️⃣ Install PHP-FPM 8.1

```bash
yum install php-fpm php-cli php-common -y
```

---

## 4️⃣ Configure PHP-FPM Socket (CRITICAL)

```bash
vi /etc/php-fpm.d/www.conf
```

---

### 🔽 Update Configuration

```ini
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```

---

## 5️⃣ Create Socket Directory

```bash
mkdir -p /var/run/php-fpm
chown -R nginx:nginx /var/run/php-fpm
```

---

## 6️⃣ Start and Enable Services

```bash
systemctl start php-fpm
systemctl enable php-fpm

systemctl start nginx
systemctl enable nginx
```

---

## 7️⃣ Validate Configuration

```bash
nginx -t
```

---

## 🧪 Verification

From Jump Host:

```bash
curl http://stapp01:8098/index.php
```

👉 Expected:

* PHP output displayed

---

## 🚨 Issues Faced (Real Debugging)

---

### ❌ Issue 1: 404 Not Found

```bash
curl localhost:8098 → 404 Not Found
```

### 🔍 Root Cause

* Nginx default index was `index.html`

### ✅ Fix

```nginx
index index.php index.html;
```

---

### ❌ Issue 2: PHP-FPM Socket Mismatch

```bash
php-fpm is not configured to use /var/run/php-fpm/default.sock
```

### 🔍 Root Cause

* PHP-FPM using default socket (`/run/php-fpm/www.sock`)

### ✅ Fix

```ini
listen = /var/run/php-fpm/default.sock
```

---

### 🔁 Restart Services

```bash
systemctl restart php-fpm
systemctl restart nginx
```

---

### 🔍 Verify Socket

```bash
ls -l /var/run/php-fpm/
```

👉 Expected:

```
default.sock
```

---

## 🔍 Troubleshooting Commands

```bash
systemctl status nginx
systemctl status php-fpm

ss -tulnp | grep 8098

ls -l /var/www/html
ls -l /var/run/php-fpm/

journalctl -xeu nginx
journalctl -xeu php-fpm
```

---

## 💡 Key Learnings

* Nginx + PHP-FPM integration using Unix socket
* Use of `upstream` block for cleaner configuration
* Importance of matching socket paths
* Debugging 404 vs backend issues
* Role of `index.php` in Nginx

---

## 🏁 Final Outcome

* Nginx running on **port 8098**
* PHP-FPM configured with correct socket
* Upstream optimization added
* PHP application working successfully

---

## 🚀 Summary

Configured Nginx with PHP-FPM using a Unix socket and upstream block for better structure, while resolving real-world issues like socket mismatch and incorrect index configuration.

---
