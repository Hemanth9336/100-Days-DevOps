---

# 🐳 Day 38: Pull Docker Image and Re-Tag

## 🧠 Problem Statement

The Nautilus DevOps team needs to prepare a container image for testing on

```bash id="b2k91z"
Application Server 2 (stapp02)
```

### Requirement

* Pull Docker image: `busybox:musl`
* Create a new tag: `busybox:blog`

---

## 🎯 Objective

* Pull image from Docker registry
* Create a new tag from existing image
* Verify both images locally

---

## 🏗️ Infrastructure Details

| Server Name        | Hostname | User  | Purpose                 |
| ------------------ | -------- | ----- | ----------------------- |
| Application Server | stapp02  | steve | Docker Image Management |

---

## ⚙️ Prerequisites

* Docker installed and running
* Access to `stapp02`
* Root or sudo privileges

---

## 🧠 Key Concepts

* **Docker Image** → Read-only template used to create containers
* **Tagging** → Creating another reference name for the same image
* **busybox** → Lightweight Linux image used for testing

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash id="k4q7ne"
ssh steve@stapp02
```

---

### 2️⃣ Switch to Root User

```bash id="p9l2vd"
sudo su -
```

---

### 3️⃣ Verify Docker Service

```bash id="q1n5sz"
systemctl status docker
```

Ensure it shows:

```id="2q9wke"
active (running)
```

---

### 4️⃣ Pull Required Image

```bash id="1g9y1c"
docker pull busybox:musl
```

---

### 5️⃣ Re-Tag the Image

```bash id="wq2k3l"
docker tag busybox:musl busybox:blog
```

---

### 6️⃣ Verify Images

```bash id="6zv5ma"
docker images
```

👉 Expected output should include:

```id="czf8qe"
busybox   musl
busybox   blog
```

---

## 🧪 Verification

```bash id="n5k2ab"
docker images | grep busybox
```

---

## 🚨 Troubleshooting

### 🔹 Image not found

```bash id="1w2e0g"
docker pull busybox:musl
```

---

### 🔹 Docker not running

```bash id="3l0rzn"
systemctl start docker
```

---

### 🔹 Permission issues

```bash id="r3l9ow"
usermod -aG docker steve
```

(Re-login required)

---

## 🔍 Key Concepts

| Concept     | Description                        |
| ----------- | ---------------------------------- |
| docker pull | Downloads image from registry      |
| docker tag  | Creates new tag for existing image |
| Repository  | Collection of tagged images        |

---

## 💡 Key Learnings

* Pulling images from Docker Hub
* Tagging images for different use cases
* Managing local Docker images
* Understanding image naming conventions

---

## 🔁 Workflow

```bash id="5l2g7k"
pull image → tag image → verify
```

---

## 🏁 Final Outcome

* Image `busybox:musl` successfully pulled
* New tag `busybox:blog` created
* Both images verified locally

---

## 🚀 Summary

Pulled a Docker image and created a custom tag for testing — a common practice in container workflows to manage versions and environments efficiently.

---
