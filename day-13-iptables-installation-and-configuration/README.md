---

# 🔐 Day 13: IPtables Installation and Configuration (Port 3004)

## 🧠 Problem Statement

The security team identified that **application port 3004 is open to all traffic**, which is a security risk.

To secure the infrastructure, we need to -

* Restrict access to this port
* Allow only trusted traffic from Load Balancer
* Ensure rules persist after reboot

---

## 🎯 Objective

* Install `iptables` on all application servers
* Allow access to port `3004` only from **Load Balancer (stlb01)**
* Block access for all other sources
* Persist rules after reboot

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname | User   | Purpose                |
| -------------------- | -------- | ------ | ---------------------- |
| Application Server 1 | stapp01  | tony   | App hosting            |
| Application Server 2 | stapp02  | steve  | App hosting            |
| Application Server 3 | stapp03  | banner | App hosting            |
| Load Balancer        | stlb01   | loki   | Trusted traffic source |

---

## ⚙️ Prerequisites

* Root or sudo access on all app servers
* Load Balancer IP address

👉 Example:

```bash
10.244.81.32   # stlb01 IP
```

---

## 🛠️ Implementation Steps

> ⚠️ Perform on all app servers (stapp01, stapp02, stapp03)

---

### 1️⃣ Install Required Packages

```bash
yum install iptables iptables-services -y
```

---

### 2️⃣ Start and Enable iptables

```bash
systemctl start iptables
systemctl enable iptables
```

---

### 3️⃣ Configure Firewall Rules

⚠️ Use **IP address (not hostname)**

```bash
# Allow Load Balancer
iptables -I INPUT 1 -p tcp -s 10.244.81.32 --dport 3004 -j ACCEPT

# Block others
iptables -I INPUT 2 -p tcp --dport 3004 -j DROP
```

---

### 4️⃣ Verify Rule Order

```bash
iptables -L INPUT -n --line-numbers
```

✅ Expected:

```text
1 ACCEPT tcp -- 10.244.81.32 ... dpt:3004
2 DROP   tcp -- 0.0.0.0/0 ... dpt:3004
```

---

### 5️⃣ Save Rules (Persistence)

```bash
iptables-save > /etc/sysconfig/iptables
```

---

### 6️⃣ Restart Service

```bash
systemctl restart iptables
```

---

## 🔍 Verification

### ❌ From Jump Host (Should Fail)

```bash
curl stapp01:3004
```

👉 Expected: Connection blocked

---

### ✅ From Load Balancer (Should Work)

```bash
ssh loki@stlb01
curl http://stapp01:3004
```

👉 Expected: Successful response

---

## 🚫 Common Mistakes (Faced During Setup)

* ❌ Installing only `iptables-services` without `iptables`
* ❌ Using hostname instead of IP (`stlb01` vs `10.244.x.x`)
* ❌ Incorrect rule order (DROP before ACCEPT)
* ❌ Applying rules on wrong server
* ❌ Using `service` instead of `systemctl`

---

## 💡 Key Learnings

* Importance of firewall rule order (top-down execution)
* Difference between `iptables` and `iptables-services`
* Real-world debugging of firewall issues
* Restricting access using source IP
* Ensuring persistence of rules across reboots

---

## 🏁 Final Outcome

* Port **3004 secured across all app servers**
* Only Load Balancer can access the service
* Firewall rules persist after reboot

---

## 🚀 Summary

Successfully implemented network-level security by restricting port access using iptables, ensuring only trusted traffic is allowed while blocking all others.

---
