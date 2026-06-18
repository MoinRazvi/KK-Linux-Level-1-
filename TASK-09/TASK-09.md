# 🚀 Linux Administration - Task 09 | Configure Local YUM Repository

## 📌 Objective

Configure a **Local YUM Repository** on the **Nautilus Backup Server** and install the **samba** package from that repository.

### ✅ Requirements

* Repository Name: `epel_local`
* Repository ID: `epel_local`
* Package Location:

```bash
/packages/downloaded_rpms/
```

* Install:

```bash
samba
```

from the newly created repository.

---

# 🖥️ Step 1: Login to Backup Server

```bash
ssh clint@stbkp01
```

Verify:

```bash
hostname
```

Expected:

```text
stbkp01
```

---

# 🔍 Step 2: Verify Package Directory

```bash
ls -ld /packages/downloaded_rpms

ls -l /packages/downloaded_rpms
```

Expected:

```text
drwxr-xr-x root root /packages/downloaded_rpms
```

---

# ⚠️ Important Observation (CentOS Stream 9)

While performing this task, the following error appeared:

```text
tee: /etc/yum.repos.d/epel_local.repo: No such file or directory
```

This means:

```text
/etc/yum.repos.d
```

directory was missing on the server.

---

# 🛠️ Step 3: Create yum.repos.d Directory

Verify:

```bash
sudo ls -ld /etc/yum.repos.d
```

If not found:

```bash
sudo mkdir -p /etc/yum.repos.d
```

Verify:

```bash
ls -ld /etc/yum.repos.d
```

---

# 📂 Step 4: Create Repository File

Create:

```bash
sudo tee /etc/yum.repos.d/epel_local.repo <<EOF
[epel_local]
name=epel_local
baseurl=file:///packages/downloaded_rpms
enabled=1
gpgcheck=0
EOF
```

---

# 🔍 Verify Repository File

```bash
cat /etc/yum.repos.d/epel_local.repo
```

Expected:

```ini
[epel_local]
name=epel_local
baseurl=file:///packages/downloaded_rpms
enabled=1
gpgcheck=0
```

---

# 🔄 Step 5: Refresh Repository Metadata

Since the server is:

```text
CentOS Stream 9
```

Use **DNF**:

```bash
sudo dnf clean all

sudo dnf repolist
```

Expected:

```text
repo id        repo name

epel_local     epel_local
```

---

# 📦 Step 6: Install Samba from Local Repository

```bash
sudo dnf install samba -y
```

---

# 🧪 Verification

### Verify Installed Package

```bash
rpm -q samba
```

Example:

```text
samba-4.x.x
```

---

### Verify Repository

```bash
sudo dnf repolist
```

Expected:

```text
epel_local
```

---

### Check Package Source

```bash
dnf info samba
```

Expected:

```text
From repo : epel_local
```

---

# 📚 Explanation of Repository File

```ini
[epel_local]
name=epel_local
baseurl=file:///packages/downloaded_rpms
enabled=1
gpgcheck=0
```

| Parameter      | Description              |
| -------------- | ------------------------ |
| `[epel_local]` | Repository ID            |
| `name`         | Repository Name          |
| `baseurl`      | Local RPM location       |
| `enabled=1`    | Enable repo              |
| `gpgcheck=0`   | Disable GPG verification |

---

# 🎯 Key Takeaways

✅ Repository files are stored in:

```bash
/etc/yum.repos.d/
```

---

✅ Local repository uses:

```bash
file:///path
```

Example:

```bash
file:///packages/downloaded_rpms
```

---

✅ Refresh repositories:

```bash
dnf clean all

dnf repolist
```

---

✅ Install package:

```bash
dnf install samba -y
```

---

✅ Verify installed package:

```bash
rpm -q samba
```

---

# ⚠️ Troubleshooting Faced During This Task

### Error:

```text
tee: /etc/yum.repos.d/epel_local.repo: No such file or directory
```

### Cause:

The directory:

```bash
/etc/yum.repos.d
```

was missing.

### Fix:

```bash
sudo mkdir -p /etc/yum.repos.d
```

After creating the directory, the repository file was created successfully and the task passed.

---

# 🎤 Interview Questions

### Q1. What is a Local YUM Repository?

**Answer:**

A Local YUM Repository is a collection of RPM packages stored on the local server that can be used to install software without accessing internet repositories.

---

### Q2. Where are YUM repository files stored?

```bash
/etc/yum.repos.d/
```

---

### Q3. Explain this URL:

```bash
file:///packages/downloaded_rpms
```

**Answer:**

* `file://` → Use local filesystem.
* `/packages/downloaded_rpms` → Directory containing RPM packages.

---

### Q4. Difference between YUM and DNF?

| YUM                          | DNF                             |
| ---------------------------- | ------------------------------- |
| Older package manager        | Next generation package manager |
| Used in RHEL/CentOS 7        | Used in RHEL/CentOS 8/9         |
| Slower dependency resolution | Faster dependency resolution    |
| Python 2 based               | Python 3 based                  |

---

### Q5. Difference between `rpm` and `yum/dnf`?

| rpm                      | yum/dnf                             |
| ------------------------ | ----------------------------------- |
| Installs local RPM       | Installs from repositories          |
| No dependency resolution | Resolves dependencies automatically |
| Manual management        | Automatic package management        |

---

### Q6. What does `dnf repolist` do?

Displays all enabled repositories.

```bash
dnf repolist
```

---

### Q7. What is GPG Check?

GPG check verifies package authenticity.

```bash
gpgcheck=0
```

means:

Disable package signature verification.

---

# 🌟 Task Status

✅ Local Repository Created
✅ `epel_local` Repository Configured
✅ Missing `/etc/yum.repos.d` Directory Created
✅ Repository Verified Successfully
✅ Samba Installed from Local Repository
✅ Task Completed Successfully 🚀
