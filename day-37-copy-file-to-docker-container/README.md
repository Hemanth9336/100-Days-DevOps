---

# 📦 Day 37: Copy File to Docker Container

## 🧠 Problem Statement

The Nautilus DevOps team has a confidential encrypted file located at

```bash
/tmp/nautilus.txt.gpg
```

A Docker container named **`ubuntu_latest`** is already running on **Application Server 3 (`stapp03`)**.

---

## 📋 Requirements

* Copy the file into the running container
* Destination path inside the container: `/opt/`
* Ensure the file is **not modified** during the transfer

---

## 🎯 Objective

* Transfer file from host → container
* Maintain file integrity
* Verify successful copy inside container

---

## 🛠️ Implementation Steps

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

Ensure `ubuntu_latest` is listed.

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

Expected output:

```
nautilus.txt.gpg
```

---

## 🧪 Verification

```bash
docker exec -it ubuntu_latest ls -l /opt/nautilus.txt.gpg
```

---

## 🏁 Final Outcome

* File successfully copied to container
* File integrity maintained
* Verified inside `/opt/` directory

---

## 🚀 Summary

Successfully copied an encrypted file from the host system to a running Docker container using `docker cp`, ensuring secure and reliable file transfer in a containerized environment.
