---

# 🐳 Day 36: Deploy Nginx Container on Application Server

## 🧠 Problem Statement

The Nautilus DevOps team is testing container-based deployments and needs to run an **Nginx container** on

```bash
Application Server 1 (stapp01)
```

### Requirement

* Create a container named `nginx_1`
* Use image: `nginx:alpine`
* Ensure the container is **running**

---

## 🎯 Objective

* Pull the required Docker image
* Run Nginx container
* Verify container is up and running

---

## 🏗️ Infrastructure Details

| Server Name        | Hostname | User | Purpose                      |
| ------------------ | -------- | ---- | ---------------------------- |
| Application Server | stapp01  | tony | Container Deployment Testing |

---

## ⚙️ Prerequisites

* Docker installed and running
* Access to server `stapp01`
* Root or sudo privileges

---

## 🧠 What is `nginx:alpine`?

* Lightweight version of Nginx
* Smaller image size → faster deployment
* Ideal for container environments

---

## 🛠️ Implementation Steps

### 1️⃣ Connect to Application Server

```bash
ssh tony@stapp01
```

---

### 2️⃣ Switch to Root User

```bash
sudo su -
```

---

### 3️⃣ Verify Docker Service

```bash
systemctl status docker
```

👉 Ensure it shows:

```
active (running)
```

---

### 4️⃣ Pull Nginx Alpine Image

```bash
docker pull nginx:alpine
```

---

### 5️⃣ Create and Run Container

```bash
docker run -d --name nginx_1 nginx:alpine
```

---

### 6️⃣ Verify Running Container

```bash
docker ps
```

👉 Expected output should include

```
nginx_1   Up ...
```

---

## 🧪 Verification

```bash
docker inspect nginx_1
```

---

## 🚨 Troubleshooting

### 🔹 Container not running

```bash
docker ps -a
docker logs nginx_1
```

---

### 🔹 Docker service not running

```bash
systemctl start docker
```

---

### 🔹 Image not found

```bash
docker pull nginx:alpine
```

---

### 🔹 Permission issues

```bash
usermod -aG docker tony
```

(Re-login required)

---

## 🔍 Key Concepts

| Concept       | Description                         |
| ------------- | ----------------------------------- |
| Container     | Running instance of an image        |
| Image         | Blueprint for container             |
| nginx:alpine  | Lightweight Nginx image             |
| Detached Mode | Runs container in background (`-d`) |

---

## 💡 Key Learnings

* How to run containers using Docker
* Difference between image and container
* Benefits of lightweight images
* Verifying container status
* Basic container lifecycle

---

## 🔁 Workflow

```
pull image → run container → verify → inspect
```

---

## 🏁 Final Outcome

* Nginx container `nginx_1` successfully created
* Container is running
* Deployment verified

---

## 🚀 Summary

Deployed an Nginx container using Docker on Application Server 1 — a foundational step in container-based application deployment and modern DevOps practices.

---
