---

# ⚖️ Day 16: Install and Configure Nginx as a Load Balancer (LBR)

## 🧠 Problem Statement

Due to increased traffic, the application is experiencing performance issues.
To improve availability and scalability, the team decided to implement a **Load Balancer (LBR)** using Nginx.

The goal is to distribute traffic across multiple application servers.

---

## 🎯 Objective

* Install and configure **Nginx on LBR server (stlb01)**
* Configure load balancing across all app servers
* Ensure Apache is running on all backend servers
* Access application via load balancer

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname | User   | Purpose             |
| -------------------- | -------- | ------ | ------------------- |
| Application Server 1 | stapp01  | tony   | Backend server      |
| Application Server 2 | stapp02  | steve  | Backend server      |
| Application Server 3 | stapp03  | banner | Backend server      |
| Load Balancer        | stlb01   | loki   | Nginx Load Balancer |

---

## ⚙️ Prerequisites

* Apache (`httpd`) must be running on all app servers
* No changes to Apache port configuration
* Root or sudo access on LBR server

---

## 🛠️ Implementation Steps

> ⚠️ Perform all steps on **Load Balancer server (stlb01)**

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

### 3️⃣ Configure Load Balancing

Edit main config file:

```bash
vi /etc/nginx/nginx.conf
```

---

### 🔽 Add Configuration Inside `http` Block

```nginx
upstream backend {
    server stapp01:80;
    server stapp02:80;
    server stapp03:80;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}
```

---

## 🔍 Configuration Explanation

* **upstream backend** → Defines backend servers
* **proxy_pass** → Forwards client requests to backend
* **round-robin** → Default load balancing method

---

### 4️⃣ Validate Configuration

```bash
nginx -t
```

👉 Expected:

```bash
syntax is ok
test is successful
```

---

### 5️⃣ Restart Nginx

```bash
systemctl restart nginx
```

---

## 🧪 Verification

From Jump Host:

```bash
curl http://stlb01
```

👉 Expected:

* Response from one of the app servers
* Requests distributed across servers

---

## 🚫 Important Notes

* ❌ Do NOT change Apache ports on backend servers
* ✅ Ensure Apache is running on all app servers
* ✅ Only modify `/etc/nginx/nginx.conf`

---

## 🔍 Troubleshooting

### Check Apache on app servers:

```bash
systemctl status httpd
```

---

### Check Nginx on LBR:

```bash
systemctl status nginx
```

---

### Test backend connectivity:

```bash
curl http://stapp01
curl http://stapp02
curl http://stapp03
```

---

## 💡 Key Learnings

* Setting up Nginx as a Load Balancer
* Understanding upstream and proxy_pass
* Distributing traffic using round-robin
* Importance of high availability architecture
* Debugging multi-server setups

---

## 🏁 Final Outcome

* Nginx successfully configured as Load Balancer
* Traffic distributed across all app servers
* Improved application availability

---

## 🚀 Summary

Implemented load balancing using Nginx to distribute incoming traffic across multiple backend servers, ensuring better performance and high availability.

---
