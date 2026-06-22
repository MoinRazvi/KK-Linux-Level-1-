# 🚀 Linux Administration - Task 15 | Troubleshoot Postfix Service Failure

## 📌 Objective

The **Postfix mail service is failing** on the Mail Server (`stmail01`).

Your task is:

1. Identify the root cause.
2. Fix the issue.
3. Ensure Postfix service is running successfully.

---

# 🖥️ Step 1: Login to Mail Server

```bash
ssh thor@jump-host

ssh groot@stmail01

sudo su -
```

Verify:

```bash
hostname
```

Expected:

```text
stmail01
```

---

# 🔍 Step 2: Check Postfix Status

```bash
systemctl status postfix
```

or

```bash
systemctl is-active postfix
```

You may see:

```text
failed
```

---

# 🔍 Step 3: Check Logs (MOST IMPORTANT)

```bash
journalctl -xeu postfix
```

or

```bash
tail -50 /var/log/maillog
```

This usually tells you exactly why Postfix failed.

---

# 🔍 Step 4: Check Postfix Configuration

Run:

```bash
postfix check
```

If there is a syntax issue, it will display errors.

Also verify:

```bash
postconf -n
```

---

# 🔍 Step 5: Check Main Configuration File

```bash
vi /etc/postfix/main.cf
```

Look for:

* Incorrect hostname
* Wrong mail directory
* Typo in parameters
* Duplicate entries

---

# Common KodeKloud Issues

### Case 1

```text
fatal: parameter inet_interfaces: no local interface found
```

Fix:

```bash
inet_interfaces = all
```

---

### Case 2

```text
fatal: bad string length
```

Check:

```bash
myhostname
mydomain
myorigin
```

---

### Case 3

```text
fatal: unknown configuration parameter
```

There is usually a typo in:

```bash
/etc/postfix/main.cf
```

---

# Step 6: Validate Configuration

```bash
postfix check
```

If no output:

✅ Configuration is OK.

---

# Step 7: Restart Service

```bash
systemctl restart postfix
```

Check:

```bash
systemctl status postfix

systemctl is-active postfix
```

Expected:

```text
active
```

---

# Useful Commands for Troubleshooting

### Check listening ports

```bash
ss -tulpn | grep :25
```

Expected:

```text
*:25
```

---

### Check postfix processes

```bash
ps -ef | grep postfix
```

---

### Check postfix configuration

```bash
postconf -n
```

---

# ⚡ Fast Troubleshooting Workflow

```bash
systemctl status postfix

journalctl -xeu postfix

postfix check

postconf -n

vi /etc/postfix/main.cf

systemctl restart postfix
```

---

# 🎯 What I Need From You

Please run these commands on **stmail01** and paste the output:

```bash
systemctl status postfix

journalctl -xeu postfix --no-pager | tail -20

postfix check
```

The KodeKloud Task-15 is intentionally a troubleshooting task, so the exact fix depends on the error shown in these commands. Once you share the output, I can give you the precise solution.
