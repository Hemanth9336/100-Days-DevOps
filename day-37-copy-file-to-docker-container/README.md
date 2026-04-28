---

# 📦 Day 37: Copy File to Docker Container

## 🧠 Problem Statement

The Nautilus DevOps team has a confidential encrypted file on

```bash
/tmp/nautilus.txt.gpg
```

A container named **`ubuntu_latest`** is already running on **Application Server 3 (`stapp03`)**.

### Requirement:

* Copy the file into the container
* Destination path inside container: `/opt/`
* Ensure the file is **not modified** during transfer

---

## 🎯 Objective

* Copy file from host → container
* Preserve file integrity
* Verify file inside container

---

## 🏗️ Infrastructure Details

| Server Name        | Hostname | User   | Purpose              |
| ------------------ | -------- | ------ | -------------------- |
| Application Server | stapp03  | banner | Docker File Transfer |

---

## ⚙️ Prerequisites

* Docker installed and running
* Container `ubuntu_latest` is running
* File exists at `/tmp/nautilus.txt.gpg`

---

## 🧠 Key Concept

👉 Use `docker cp` to copy files between host and container

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash
ssh banner@stapp03
```

---

### 2️⃣ Switch to Root User

```bash
sudo su -
```

---

### 3️⃣ Verify Container is Running

```bash
docker ps
```

👉 Ensure container `ubuntu_latest` is listed

---

### 4️⃣ Copy File to Container

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
```

---

### 5️⃣ Verify File Inside Container

```bash
docker exec -it ubuntu_latest ls /opt/
```

👉 Expected output:

```bash
nautilus.txt.gpg
```

---

## 🧪 Verification

```bash
docker exec -it ubuntu_latest ls -l /opt/nautilus.txt.gpg
```

---

## 🚨 Troubleshooting

### 🔹 Container not found

```bash
docker ps -a
```

---

### 🔹 File not found on host

```bash
ls /tmp/nautilus.txt.gpg
```

---

### 🔹 Permission issue

```bash
sudo docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
```

---

### 🔹 Container not running

```bash
docker start ubuntu_latest
```

---

## 🔍 Key Concepts

| Concept        | Description                              |
| -------------- | ---------------------------------------- |
| docker cp      | Copy files between host and container    |
| Container Path | Destination inside container             |
| File Integrity | Ensuring no modification during transfer |

---

## 💡 Key Learnings

* Copying files into running containers
* Understanding host vs container filesystem
* Verifying file transfers
* Handling permissions in Docker

---

## 🔁 Workflow

```bash
host file → docker cp → container → verify
```

---

## 🏁 Final Outcome

* File successfully copied to container
* File integrity maintained
* Verified inside `/opt/` directory

---

## 🚀 Summary

Transferred a secure file from host to Docker container using `docker cp` — a common real-world task when managing containerized applications and sensitive data.

---
