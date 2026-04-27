---

# 🐳 Day 36: Deploy Nginx Container on Application Server

## 🧠 Problem Statement

The Nautilus DevOps team is testing container-based deployments and needs to run an **Nginx container** on **Application Server 1 (`stapp01`)**.

---

## 📋 Requirements

* Create a container named `nginx_1`
* Use the image `nginx:alpine`
* Ensure the container is in a **running state**

---

## 🎯 Objective

* Pull the required Docker image
* Create and run the container
* Verify that the container is running

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

Ensure it shows:

```
active (running)
```

---

### 4️⃣ Pull Nginx Alpine Image

```bash
docker pull nginx:alpine
```

---

### 5️⃣ Run the Container

```bash
docker run -d --name nginx_1 nginx:alpine
```

---

### 6️⃣ Verify Container Status

```bash
docker ps
```

Expected output should include:

```
nginx_1   Up ...
```

---

## 🧪 Verification

```bash
docker inspect nginx_1
```

---

## 🏁 Final Outcome

* Nginx container `nginx_1` successfully created
* Container is running
* Deployment verified

---

## 🚀 Summary

Successfully deployed an Nginx container using Docker on Application Server 1 — a key step toward container-based application deployment in real-world DevOps environments.
