## ✅ Task-19: Create Bash Script for Website Archive 📦

### 📌 Problem Statement

Create a bash script named **`ecommerce_archive.sh`** on **App Server 2** to archive website content and copy it to the Storage Server.

**Requirements:**

* Create archive: `xfusioncorp_ecommerce.zip`
* Archive source: `/var/www/html/ecommerce`
* Save locally in: `/archives`
* Copy archive to Storage Server: `/archives`
* Script location: `/scripts/ecommerce_archive.sh`
* Passwordless SSH should be configured.
* Do not use `sudo` inside the script.

---

### 🛠️ Install zip Package

```bash
sudo yum install -y zip
```

Verify:

```bash
zip -v
```

---

### 📂 Create Script Directory

```bash
mkdir -p /scripts
```

---

### 📝 Bash Script

**File:** `/scripts/ecommerce_archive.sh`

```bash
#!/bin/bash

ARCHIVE="xfusioncorp_ecommerce.zip"

mkdir -p /archives

zip -r /archives/$ARCHIVE /var/www/html/ecommerce

scp /archives/$ARCHIVE natasha@ststor01:/archives/
```

---

### 🔑 Configure Passwordless SSH

Generate SSH key:

```bash
ssh-keygen
```

Copy public key to Storage Server:

```bash
ssh-copy-id natasha@ststor01
```

Test:

```bash
ssh natasha@ststor01
```

No password prompt should appear.

---

### 🚀 Make Script Executable

```bash
chmod +x /scripts/ecommerce_archive.sh
```

Run:

```bash
/scripts/ecommerce_archive.sh
```

---

### 🔍 Validation

Verify local archive:

```bash
ls -l /archives
```

Expected:

```text
xfusioncorp_ecommerce.zip
```

Verify Storage Server:

```bash
ssh natasha@ststor01

ls -l /archives
```

Expected:

```text
xfusioncorp_ecommerce.zip
```

---

### 🧠 Key Learnings

* Bash Scripting
* Zip Archive Creation
* Secure Copy (`scp`)
* SSH Key Authentication
* Passwordless File Transfer
* Script Execution Permissions

---

### 🎤 Interview Questions

**Q1. What does `zip -r` do?**

```bash
zip -r archive.zip directory/
```

* `-r` → Recursive
* Compresses directories and subdirectories.

---

**Q2. What is `scp`?**

Secure Copy command used to transfer files over SSH.

Example:

```bash
scp file.txt user@server:/path/
```

---

**Q3. Why configure Passwordless SSH?**

* Automation
* CI/CD pipelines
* Backup scripts
* Ansible connectivity

---

**Q4. Difference between `scp` and `rsync`?**

| scp                | rsync                      |
| ------------------ | -------------------------- |
| Copies entire file | Copies changed blocks only |
| Simple             | Faster for large files     |
| No synchronization | Supports synchronization   |

---

**Q5. What does `chmod +x` do?**

Makes a script executable.

Example:

```bash
chmod +x ecommerce_archive.sh
```

---

✅ **Task Status:** Completed Successfully 🚀
