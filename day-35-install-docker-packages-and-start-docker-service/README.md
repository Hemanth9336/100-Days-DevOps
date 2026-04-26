---

# 🐳 Day 35: Install Docker & Start Docker Service

## 🧠 Problem Statement

The DevOps team plans to containerize applications and needs to prepare **App Server 2** by

* Installing Docker (`docker-ce`)
* Installing Docker Compose
* Starting Docker service

---

## 🎯 Objective

* Install Docker Engine
* Install Docker Compose
* Enable and start Docker service
* Verify installation

---

## 🏗️ Infrastructure Details

| Server Name        | Hostname | User  | Purpose                       |
| ------------------ | -------- | ----- | ----------------------------- |
| Application Server | stapp02  | steve | Docker Installation & Testing |

---

## ⚙️ Prerequisites

* Access to server (`stapp02`)
* Root or sudo privileges
* Internet access (for package installation)

---

## 🧠 What is Docker?

Docker is a containerization platform that allows applications to run in isolated environments called containers.

---

## 🛠️ Implementation Steps

---

## 1️⃣ Connect to App Server 2

```bash id="z4sx3b"
ssh steve@stapp02
```

---

## 2️⃣ Switch to Root User

```bash id="q7j7ec"
sudo su -
```

---

## 3️⃣ Install Required Packages

```bash id="cxnt5o"
yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

---

## 4️⃣ Start Docker Service

```bash id="3y66xk"
systemctl start docker
```

---

## 5️⃣ Enable Docker Service

```bash id="r0o0yx"
systemctl enable docker
```

---

## 6️⃣ Verify Docker Status

```bash id="9z1f1c"
systemctl status docker
```

👉 Expected:

```
active (running)
```

---

## 7️⃣ Verify Docker Installation

```bash id="lqwh6y"
docker --version
```

---

## 8️⃣ Verify Docker Compose

```bash id="tnvxpk"
docker compose version
```

---

## 🧪 Testing

Run a test container:

```bash id="k9o3p4"
docker run hello-world
```

👉 Expected:

* Docker pulls image
* Container runs successfully

---

## 🚨 Troubleshooting

### Docker not found

```bash id="9tqkdb"
yum install docker-ce -y
```

---

### Service not starting

```bash id="2l6m0r"
systemctl restart docker
journalctl -xeu docker
```

---

### Permission issue

```bash id="d8u4rx"
usermod -aG docker steve
```

Then re-login

---

## 🔍 Key Concepts

| Concept        | Description                      |
| -------------- | -------------------------------- |
| Docker         | Containerization platform        |
| Container      | Lightweight isolated environment |
| Image          | Blueprint for container          |
| Docker Compose | Multi-container management tool  |

---

## 💡 Key Learnings

* Installing Docker and dependencies
* Managing services using `systemctl`
* Verifying container runtime setup
* Running test containers
* Basics of containerization

---

## 🔁 Workflow

```bash id="kl8t5f"
install docker → start service → enable → verify → run container
```

---

## 🏁 Final Outcome

* Docker successfully installed
* Docker service started and enabled
* Docker Compose installed
* Test container executed successfully

---

## 🚀 Summary

Set up Docker environment on App Server 2 to begin containerization — a foundational step in modern DevOps workflows and application deployment.

---
