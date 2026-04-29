---

# 🐳 Day 38: Pull Docker Image and Re-Tag

## 🧠 Problem Statement

The Nautilus DevOps team needs to prepare a container image for testing on **Application Server 2 (`stapp02`)**.

---

## 📋 Requirements

* Pull Docker image: `busybox:musl`
* Create a new tag: `busybox:blog`

---

## 🎯 Objective

* Pull the required image from Docker Hub
* Create a new tag from the existing image
* Verify both images locally

---

## 🛠️ Implementation Steps

### 1️⃣ Connect to Application Server

```bash id="t8w3h9"
ssh steve@stapp02
```

---

### 2️⃣ Switch to Root User

```bash id="q2y6mz"
sudo su -
```

---

### 3️⃣ Verify Docker Service

```bash id="m1v8kp"
systemctl status docker
```

Ensure it shows:

```id="c6n9xd"
active (running)
```

---

### 4️⃣ Pull the Image

```bash id="a4k7sl"
docker pull busybox:musl
```

---

### 5️⃣ Re-Tag the Image

```bash id="z9d2fj"
docker tag busybox:musl busybox:blog
```

---

### 6️⃣ Verify Images

```bash id="p3x6rq"
docker images
```

Expected output should include:

```id="y8v1nb"
busybox   musl
busybox   blog
```

---

## 🏁 Final Outcome

* Image `busybox:musl` successfully pulled
* New tag `busybox:blog` created
* Both images verified locally

---

## 🚀 Summary

Successfully pulled a Docker image and created a custom tag, demonstrating how to manage and reuse images efficiently in containerized environments.
