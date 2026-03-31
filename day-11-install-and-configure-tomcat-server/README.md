---

# 🚀 Day 11: Install and Configure Tomcat Server

## 🧠 Problem Statement

The Nautilus development team has built a Java-based application and wants to deploy it using a **Tomcat server** on **App Server 2**.

The setup should ensure:

* Tomcat is installed and configured
* Runs on a custom port (`8085`)
* Application is deployed as ROOT
* Accessible via base URL

---

## 🎯 Objective

Set up Tomcat on:

```bash
App Server 2 (stapp02)
```

And ensure:

* Tomcat runs on **port 8085**
* `ROOT.war` is deployed
* Application is accessible via:

```bash
http://stapp02:8085
```

---

## 🏗️ Infrastructure Details

| Server Name          | Hostname  | User  | Purpose                |
| -------------------- | --------- | ----- | ---------------------- |
| Application Server 2 | stapp02   | steve | Hosts Java application |
| Jump Host            | jump-host | thor  | Contains ROOT.war file |

---

## ⚙️ Prerequisites

* Access to App Server 2 (`steve` user)
* Access to Jump Host (`thor` user)
* Java must be installed

### Install Java (if not installed)

```bash
sudo yum install java -y     # RHEL/CentOS
# OR
sudo apt install default-jdk -y   # Ubuntu
```

---

## 📦 Step 1: Install Tomcat

```bash
sudo yum install tomcat -y      # RHEL/CentOS
# OR
sudo apt install tomcat9 -y     # Ubuntu
```

---

## ⚙️ Step 2: Configure Tomcat Port

Edit Tomcat configuration:

```bash
sudo vi /etc/tomcat/server.xml
```

Find the connector port:

```xml
<Connector port="8080" protocol="HTTP/1.1"
```

Change it to:

```xml
<Connector port="8085" protocol="HTTP/1.1"
```

---

## 📁 Step 3: Copy ROOT.war from Jump Host

Login to App Server 2 and copy the file:

```bash
scp thor@jump-host:/tmp/ROOT.war /tmp/
```

---

## 🚀 Step 4: Deploy Application

Move the WAR file to Tomcat webapps:

```bash
sudo cp /tmp/ROOT.war /var/lib/tomcat/webapps/
```

> 📌 Tomcat will automatically extract and deploy it as ROOT application

---

## 🔄 Step 5: Start and Enable Tomcat

```bash
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

---

## 🧪 Step 6: Verify Deployment

```bash
curl http://stapp02:8085
```

✅ Expected Output: Application response should be displayed

---

## 🔐 Permissions & Notes

* Ensure correct permissions on `/var/lib/tomcat/webapps/`
* WAR file must be named `ROOT.war` to serve on base URL
* Make sure port `8085` is allowed in firewall (if applicable)

---

## 🚫 Important Notes

* Ensure Tomcat service is running
* Verify no service conflict on port 8085
* Deployment happens automatically when WAR is placed in `webapps`

---

## 💡 Key Learnings

* Installing and configuring Tomcat server
* Changing default service ports
* Deploying Java applications using WAR files
* Using `scp` for file transfer across servers
* Understanding how ROOT context works in Tomcat

---

## 🏁 Outcome

* Tomcat successfully installed on **stapp02**
* Running on **port 8085**
* Application deployed and accessible via:

```bash
http://stapp02:8085
```

---
