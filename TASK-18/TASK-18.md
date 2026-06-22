## ✅ Task-18: Troubleshoot MariaDB Service 🔧

### 📌 Problem Statement

The Nautilus application was unable to connect to the database because the **MariaDB service was down** on the Database Server (`stdb01`).

**Objective:**

* Identify the root cause.
* Fix the MariaDB startup issue.
* Ensure the service is running successfully.

---

### 🔍 Issue Observed

Check service:

```bash
systemctl status mariadb
```

Result:

```text
Active: failed
```

---

### 📋 Error Logs

```bash
journalctl -xeu mariadb.service
```

Error:

```text
Can't create/write to file '/run/mariadb/mariadb.pid'
Errcode: 13 "Permission denied"

Can't start server: can't create PID file: Permission denied
```

---

### 🛠️ Root Cause

MariaDB was unable to create the PID file:

```text
/run/mariadb/mariadb.pid
```

The directory:

```text
/run/mariadb
```

had incorrect ownership/permissions.

---

### ✅ Solution

Create the directory (if missing):

```bash
sudo mkdir -p /run/mariadb
```

Update ownership:

```bash
sudo chown mysql:mysql /run/mariadb
```

Update permissions:

```bash
sudo chmod 755 /run/mariadb
```

Restart MariaDB:

```bash
sudo systemctl restart mariadb
```

---

### 🚀 Verification

Check service:

```bash
systemctl status mariadb
```

or

```bash
systemctl is-active mariadb
```

Expected:

```text
active
```

Verify PID file:

```bash
ls -l /run/mariadb
```

Expected:

```text
mariadb.pid
```

owned by:

```text
mysql mysql
```

---

### ⚡ One-Line Fix

```bash
mkdir -p /run/mariadb && \
chown mysql:mysql /run/mariadb && \
chmod 755 /run/mariadb && \
systemctl restart mariadb
```

---

### 🧠 Key Learnings

* Troubleshooting failed systemd services
* Reading MariaDB error logs
* Understanding PID files
* Linux file ownership and permissions
* Service recovery using `systemctl`

---

### 🎤 Interview Questions

**Q1. What is a PID file?**

A PID (Process ID) file stores the process ID of a running service. It helps the operating system and service manager track and manage the process.

---

**Q2. Where is the MariaDB PID file generally located?**

```text
/run/mariadb/mariadb.pid
```

---

**Q3. Why would MariaDB fail with `Permission denied` on the PID file?**

* Directory ownership is incorrect.
* The `mysql` user does not have write permission.
* The directory does not exist.

---

**Q4. How do you troubleshoot a failed MariaDB service?**

```bash
systemctl status mariadb

journalctl -xeu mariadb

tail -50 /var/log/mariadb/mariadb.log
```

---

**Q5. Difference between `systemctl status` and `journalctl`?**

| systemctl status     | journalctl          |
| -------------------- | ------------------- |
| Shows service state  | Shows detailed logs |
| Quick health check   | Root cause analysis |
| Active/Failed status | Historical logs     |

---

✅ **Task Status:** Completed Successfully 🚀
