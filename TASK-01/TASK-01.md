# 🚀 Linux Administration - Task 01 | Cron Job Automation

## 📌 Objective

The Nautilus System Admin team wants to test cron job automation before deploying production scripts on all application servers.

### ✅ Tasks Performed

* 📦 Install `cronie` package on all app servers.
* ▶️ Start and enable `crond` service.
* ⏰ Configure a cron job for the **root** user.
* 📝 Create `/tmp/cron_text` every **5 minutes** with the text **hello**.

---

## 🏗️ Environment

| Server      | User   |
| ----------- | ------ |
| 🖥️ stapp01 | tony   |
| 🖥️ stapp02 | steve  |
| 🖥️ stapp03 | banner |

---

## 🔐 Step 1: Login to Servers

### Connect to stapp01

```bash
ssh tony@stapp01
```

### Connect to stapp02

```bash
ssh steve@stapp02
```

### Connect to stapp03

```bash
ssh banner@stapp03
```

---

## 📦 Step 2: Install Cronie Package

### For RHEL/CentOS

```bash
sudo yum install -y cronie
```

### For Rocky Linux / RHEL 8+

```bash
sudo dnf install -y cronie
```

---

## ▶️ Step 3: Enable and Start Cron Service

```bash
sudo systemctl enable crond
sudo systemctl start crond
```

### Verify Service Status

```bash
sudo systemctl status crond
```

Expected Output:

```bash
Active: active (running)
```

---

## ⏰ Step 4: Add Cron Job for Root User

Edit root crontab:

```bash
sudo crontab -e
```

Add:

```cron
*/5 * * * * echo hello > /tmp/cron_text
```

Save and Exit.

---

## ⚡ Alternative Method

Add cron entry directly:

```bash
echo '*/5 * * * * echo hello > /tmp/cron_text' | sudo crontab -
```

---

## 🔍 Step 5: Verify Cron Entry

```bash
sudo crontab -l
```

Output:

```bash
*/5 * * * * echo hello > /tmp/cron_text
```

---

## 🧪 Step 6: Verify Cron Execution

Wait for 5 minutes and run:

```bash
cat /tmp/cron_text
```

Expected:

```bash
hello
```

---

# 📖 Understanding the Cron Schedule

```text
*/5 * * * * command
│
├── Minute (Every 5 minutes)
├── Hour (* = Every hour)
├── Day of Month (*)
├── Month (*)
└── Day of Week (*)
```

### Some Common Examples

| Cron Expression | Meaning               |
| --------------- | --------------------- |
| `* * * * *`     | Every minute          |
| `*/5 * * * *`   | Every 5 minutes       |
| `0 * * * *`     | Every hour            |
| `0 0 * * *`     | Every day at midnight |
| `0 9 * * 1-5`   | Weekdays at 9 AM      |

---

# 📋 Validation Checklist

### Verify Package

```bash
rpm -q cronie
```

### Verify Service

```bash
systemctl status crond
```

### Verify Cron Job

```bash
sudo crontab -l
```

### Verify File Creation

```bash
ls -l /tmp/cron_text
cat /tmp/cron_text
```

---

# 🎯 Key Takeaways

✅ Cron is a time-based job scheduler in Linux.

✅ `crond` is the daemon that executes cron jobs.

✅ Each user has their own crontab.

✅ Root user's cron jobs are managed using:

```bash
sudo crontab -e
```

✅ Cron logs can be checked using:

```bash
sudo grep CRON /var/log/cron
```

---

# 🎤 Interview Questions

## Q1. What is Cron in Linux?

**Answer:**
Cron is a time-based job scheduler used to automate repetitive tasks such as backups, cleanup scripts, report generation, and monitoring.

---

## Q2. What is the difference between cron and crond?

| cron                 | crond                   |
| -------------------- | ----------------------- |
| Scheduling mechanism | Daemon process          |
| Stores schedules     | Executes scheduled jobs |

---

## Q3. How do you edit cron jobs for the current user?

```bash
crontab -e
```

---

## Q4. How do you edit cron jobs for root?

```bash
sudo crontab -e
```

---

## Q5. How do you list cron jobs?

```bash
crontab -l
```

For root:

```bash
sudo crontab -l
```

---

## Q6. Where are cron jobs stored?

| Location            | Purpose          |
| ------------------- | ---------------- |
| `/var/spool/cron/`  | User crontabs    |
| `/etc/crontab`      | System cron file |
| `/etc/cron.daily/`  | Daily jobs       |
| `/etc/cron.hourly/` | Hourly jobs      |
| `/etc/cron.weekly/` | Weekly jobs      |

---

## Q7. Explain this cron expression

```bash
*/5 * * * * echo hello > /tmp/cron_text
```

**Answer:**

* `*/5` → Every 5 minutes
* `*` → Every hour
* `*` → Every day of month
* `*` → Every month
* `*` → Every day of week
* Command writes **hello** to `/tmp/cron_text`

---

## Q8. How do you check cron service status?

```bash
systemctl status crond
```

---

## Q9. Where can you check cron logs?

```bash
grep CRON /var/log/cron
```

or

```bash
journalctl -u crond
```

---

# 🌟 Task Status

✅ Cronie Installed
✅ crond Service Started
✅ Root Cron Configured
✅ File Created Every 5 Minutes
✅ Task Completed Successfully 🚀

---
