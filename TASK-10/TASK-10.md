# 🚀 Linux Administration - Task 10 | Install and Enable Squid on All App Servers

## 📌 Objective

As part of the new application release, install and configure the **Squid Proxy Server** on all Nautilus application servers.

### ✅ Requirements

* Install **squid** package on:

  * 🖥️ stapp01
  * 🖥️ stapp02
  * 🖥️ stapp03

* Ensure the **squid service is enabled** to start automatically during boot.

---

# 🖥️ Step 1: Login to App Server 1

```bash
ssh tony@stapp01
```

Install Squid:

```bash
sudo yum install -y squid
```

For CentOS Stream 9:

```bash
sudo dnf install -y squid
```

Enable the service:

```bash
sudo systemctl enable squid
```

Verify:

```bash
systemctl is-enabled squid
```

Expected:

```text
enabled
```

Exit:

```bash
exit
```

---

# 🖥️ Step 2: Login to App Server 2

```bash
ssh steve@stapp02
```

Install:

```bash
sudo yum install -y squid
```

Enable:

```bash
sudo systemctl enable squid
```

Verify:

```bash
systemctl is-enabled squid
```

Expected:

```text
enabled
```

Exit:

```bash
exit
```

---

# 🖥️ Step 3: Login to App Server 3

```bash
ssh banner@stapp03
```

Install:

```bash
sudo yum install -y squid
```

Enable:

```bash
sudo systemctl enable squid
```

Verify:

```bash
systemctl is-enabled squid
```

Expected:

```text
enabled
```

---

# ⚡ Shortcut Commands

### stapp01

```bash
ssh tony@stapp01 "sudo yum install -y squid && sudo systemctl enable squid"
```

### stapp02

```bash
ssh steve@stapp02 "sudo yum install -y squid && sudo systemctl enable squid"
```

### stapp03

```bash
ssh banner@stapp03 "sudo yum install -y squid && sudo systemctl enable squid"
```

---

# 🧪 Validation Commands

### Check Package Installation

```bash
rpm -q squid
```

Expected:

```text
squid-<version>
```

---

### Check Service Status

```bash
systemctl status squid
```

---

### Check if Enabled

```bash
systemctl is-enabled squid
```

Expected:

```text
enabled
```

---

# 📚 Understanding `enable` vs `start`

| Command                        | Purpose                                   |
| ------------------------------ | ----------------------------------------- |
| `systemctl start squid`        | Starts service immediately                |
| `systemctl enable squid`       | Starts service automatically after reboot |
| `systemctl enable --now squid` | Enable + Start immediately                |

---

## Important Note for This Task

The requirement says:

> **Make sure it is enabled to start during boot**

This means:

```bash
sudo systemctl enable squid
```

is sufficient.

You do **not** need:

```bash
sudo systemctl start squid
```

unless specifically mentioned.

---

# 🎯 Key Takeaways

✅ Install package:

```bash
yum install -y squid
```

---

✅ Enable service:

```bash
systemctl enable squid
```

---

✅ Check if enabled:

```bash
systemctl is-enabled squid
```

---

✅ Check installed package:

```bash
rpm -q squid
```

---

# 🎤 Interview Questions

### Q1. What is Squid?

**Answer:**

Squid is a **proxy caching server** used to:

* Cache web pages
* Improve performance
* Reduce bandwidth usage
* Filter internet access

---

### Q2. What is the default configuration file of Squid?

```bash
/etc/squid/squid.conf
```

---

### Q3. What port does Squid use by default?

```text
3128
```

Example:

```bash
http_port 3128
```

---

### Q4. Difference between `enable` and `start`?

| Command        | Meaning                     |
| -------------- | --------------------------- |
| `start`        | Start now                   |
| `enable`       | Start automatically at boot |
| `enable --now` | Both start and enable       |

---

### Q5. How do you check whether a service is enabled?

```bash
systemctl is-enabled squid
```

Output:

```text
enabled
```

---

### Q6. How do you list all enabled services?

```bash
systemctl list-unit-files --state=enabled
```

---

### Q7. How do you check package installation?

```bash
rpm -q squid
```

or

```bash
dnf list installed squid
```

---

# 🌟 Task Status

✅ Squid Installed on stapp01
✅ Squid Installed on stapp02
✅ Squid Installed on stapp03
✅ Service Enabled on Boot
✅ Validation Completed Successfully 🚀
