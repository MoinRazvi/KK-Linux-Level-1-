Absolutely. Here is the **GitHub README for Task-22** in the same style as your previous KodeKloud tasks with **emojis, objectives, validation, troubleshooting, key learnings, and interview questions**.

---

# 🚀 Task-22: Install HAProxy and Configure Log Rotation

## 🎯 Objective

The Nautilus DevOps team needs to:

✅ Install **HAProxy** on all App Servers
✅ Configure **logrotate** for HAProxy logs
✅ Rotate logs **monthly**
✅ Retain only **3** rotated log files

---

## 🖥️ Servers Used

| Server  | User   |
| ------- | ------ |
| stapp01 | tony   |
| stapp02 | steve  |
| stapp03 | banner |

---

## 📦 Step 1: Install HAProxy

### App Server 1

```bash
sudo yum install -y haproxy
```

### App Server 2

```bash
sudo yum install -y haproxy
```

### App Server 3

```bash
sudo yum install -y haproxy
```

---

## 🔍 Verify Installation

```bash
rpm -q haproxy
```

Example:

```text
haproxy-2.8.x
```

---

## 📂 Step 2: Check Logrotate Configuration

```bash
ls -l /etc/logrotate.d | grep haproxy
```

Possible output:

```text
haproxy
```

or

```text
haproxy.disabled
```

---

## 🛠️ Step 3: Enable Logrotate File

If disabled:

```bash
mv /etc/logrotate.d/haproxy.disabled /etc/logrotate.d/haproxy
```

---

## ✏️ Step 4: Configure Log Rotation

Edit:

```bash
vi /etc/logrotate.d/haproxy
```

Update:

```text
/var/log/haproxy.log {
    monthly
    rotate 3
    compress
    missingok
    notifempty
    copytruncate
}
```

---

## ✅ Verification

Check:

```bash
cat /etc/logrotate.d/haproxy
```

Expected:

```text
monthly
rotate 3
```

---

## 🧪 Validation Commands

### Verify HAProxy

```bash
rpm -q haproxy
```

### Verify Logrotate

```bash
grep -E "monthly|rotate" /etc/logrotate.d/haproxy
```

Expected:

```text
monthly
rotate 3
```

---

## 🔧 Troubleshooting Commands

### Check package

```bash
rpm -q haproxy
```

### Check logrotate file

```bash
ls -l /etc/logrotate.d
```

### View configuration

```bash
cat /etc/logrotate.d/haproxy
```

### Search specific settings

```bash
grep -E "monthly|rotate" /etc/logrotate.d/haproxy
```

---

## 🧠 Key Learnings

🔹 Installing HAProxy using Yum
🔹 Understanding Linux Log Rotation
🔹 Monthly log rotation strategy
🔹 Retaining limited log history (`rotate 3`)
🔹 Compressing archived logs
🔹 Managing logs efficiently in Production

---

## 🎤 Interview Questions

### ❓ What is Logrotate?

Logrotate is a Linux utility used to:

* Rotate log files
* Compress old logs
* Remove older archives
* Manage disk usage efficiently

---

### ❓ What does `rotate 3` mean?

It keeps:

* Current active log
* Last 3 archived log files

Older log archives are automatically removed.

---

### ❓ What does `monthly` mean?

```text
monthly
```

The logs are rotated once every month.

---

### ❓ What does `copytruncate` do?

```text
copytruncate
```

* Copies the current log to a rotated file.
* Truncates the original log file.
* Allows the application to continue writing without restart.

---

## 🎉 Task Status

✅ HAProxy Installed on all App Servers
✅ Logrotate Configured
✅ Monthly Rotation Enabled
✅ Retaining Last 3 Logs Only
✅ Task Completed Successfully 🚀
