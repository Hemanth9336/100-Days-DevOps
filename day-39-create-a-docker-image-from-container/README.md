---

# 🐳 Day 39: Create a Docker Image from Container

## 🧠 Problem Statement

A Nautilus developer has made changes inside a running container and wants to preserve those changes by creating a new Docker image.

The container **`ubuntu_latest`** is running on **Application Server 3 (`stapp03`)**.

---

## 📋 Requirements

* Create a new image from the running container
* Image name: `media:xfusion`
* Source container: `ubuntu_latest`

---

## 🎯 Objective

* Capture container state as a new image
* Preserve changes made inside the container
* Verify the newly created image

---

## 🛠️ Implementation Steps

### 1️⃣ Connect to Application Server

```bash id="m1k8qz"
ssh banner@stapp03
```

---

### 2️⃣ Switch to Root User

```bash id="x4p9we"
sudo su -
```

---

### 3️⃣ Verify Running Container

```bash id="z8t2qy"
docker ps
```

Ensure `ubuntu_latest` is listed.

---

### 4️⃣ Create Image from Container

```bash id="c3v7nb"
docker commit ubuntu_latest media:xfusion
```

---

### 5️⃣ Verify Image Creation

```bash id="p9w2kl"
docker images
```

Expected output should include:

```id="v2x7gd"
media   xfusion
```

---

## 🧪 Verification

```bash id="k7m3sa"
docker images | grep media
```

---

## 🏁 Final Outcome

* Image `media:xfusion` successfully created
* Container state preserved as an image
* Verified image availability locally

---

## 🚀 Summary

Created a Docker image from a running container using `docker commit`, allowing changes inside the container to be saved and reused — a useful technique for quick backups and testing scenarios in DevOps workflows.
