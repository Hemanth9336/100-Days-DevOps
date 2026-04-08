---

# 🌐 Day 19: Install and Configure Web Application (Apache)

## 🧠 Problem Statement

The team needs to prepare **App Server 1** to host two static websites

* `media`
* `apps`

The website backups are available on the **Jump Host**, and Apache must be configured to serve them on specific paths.

---

## 🎯 Objective

* Install Apache (`httpd`)
* Configure Apache to run on port **3004**
* Deploy two websites:

  * `/media` → `http://localhost:3004/media/`
  * `/apps` → `http://localhost:3004/apps/`
* Verify access using `curl`

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname  | User | Purpose           |
| -------------------- | --------- | ---- | ----------------- |
| Application Server 1 | stapp01   | tony | Web Server        |
| Jump Host            | jump-host | thor | Source of backups |

---

## 📁 Source Files

| Directory | Location           |
| --------- | ------------------ |
| media     | `/home/thor/media` |
| apps      | `/home/thor/apps`  |

---

## ⚙️ Prerequisites

* Access to both:

  * App Server (`stapp01`)
  * Jump Host (`jump-host`)
* Root or sudo privileges
* Apache not already running on conflicting port

---

## 🛠️ Implementation Steps

---

### 1️⃣ Install Apache (httpd)

```bash
ssh tony@stapp01
sudo su -

yum install httpd -y
```

---

### 2️⃣ Configure Apache to Run on Port 3004

Edit config:

```bash
vi /etc/httpd/conf/httpd.conf
```

Update:

```bash
Listen 3004
```

❗ Comment default port:

```bash
#Listen 80
```

---

### 3️⃣ Start and Enable Apache

```bash
systemctl start httpd
systemctl enable httpd
```

---

### 4️⃣ Copy Website Files from Jump Host

From **App Server**:

```bash
scp -r thor@jump-host:/home/thor/media /var/www/html/
scp -r thor@jump-host:/home/thor/apps /var/www/html/
```

---

### 5️⃣ Set Proper Permissions

```bash
chown -R apache:apache /var/www/html/media
chown -R apache:apache /var/www/html/apps

chmod -R 755 /var/www/html/
```

---

### 6️⃣ Configure Apache Aliases

Edit config:

```bash
vi /etc/httpd/conf/httpd.conf
```

Add at the end:

```apache
Alias /media /var/www/html/media
<Directory /var/www/html/media>
    Require all granted
</Directory>

Alias /apps /var/www/html/apps
<Directory /var/www/html/apps>
    Require all granted
</Directory>
```

---

### 7️⃣ Validate Configuration

```bash
httpd -t
```

---

### 8️⃣ Restart Apache

```bash
systemctl restart httpd
```

---

## 🧪 Verification

Run on **App Server**:

```bash
curl http://localhost:3004/media/
curl http://localhost:3004/apps/
```

👉 Expected:

* Both endpoints return content successfully

---

## 🚫 Important Notes

* Ensure Apache is running on **port 3004**
* Do NOT use default port 80
* Ensure correct file permissions
* Alias paths must match directories

---

## 🔍 Troubleshooting

### Check Apache status:

```bash
systemctl status httpd
```

---

### Check port:

```bash
ss -tulnp | grep 3004
```

---

### Check logs:

```bash
journalctl -xeu httpd
```

---

## 💡 Key Learnings

* Configuring Apache on custom ports
* Hosting multiple applications using aliases
* Copying data securely using `scp`
* Managing file permissions for web servers
* Debugging web server issues

---

## 🏁 Final Outcome

* Apache installed and configured
* Running on port **3004**
* Two websites successfully hosted:

  * `/media`
  * `/apps`
* Verified using curl

---

## 🚀 Summary

Configured Apache to host multiple static websites on a custom port using aliases, enabling structured and scalable web hosting.

---
