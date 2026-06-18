# 🚀 Linux Administration - Task 07 | Install Samba Package on All App Servers

## 📌 Objective

Install the **`samba`** package on all Nautilus application servers.

### Servers

| 🖥️ Server | 👤 User |
| ---------- | ------- |
| stapp01    | tony    |
| stapp02    | steve   |
| stapp03    | banner  |

---

# 🖥️ Step 1: Login to stapp01

```bash
ssh tony@stapp01
```

Install samba:

```bash
sudo yum install -y samba
```

If the server uses DNF:

```bash
sudo dnf install -y samba
```

Verify:

```bash
rpm -q samba
```

Example Output:

```text
samba-4.x.x-x.el8.x86_64
```

Exit:

```bash
exit
```

---

# 🖥️ Step 2: Login to stapp02

```bash
ssh steve@stapp02
```

Install:

```bash
sudo yum install -y samba
```

Verify:

```bash
rpm -q samba
```

Exit:

```bash
exit
```

---

# 🖥️ Step 3: Login to stapp03

```bash
ssh banner@stapp03
```

Install:

```bash
sudo yum install -y samba
```

Verify:

```bash
rpm -q samba
```

---

# ⚡ Faster Method (One-Liner from Jump Host)

If password-less SSH is already configured from **Task-05**, you can run:

```bash
ssh tony@stapp01 "sudo yum install -y samba"
ssh steve@stapp02 "sudo yum install -y samba"
ssh banner@stapp03 "sudo yum install -y samba"
```

---

# ✅ Validation

Check package on each server:

```bash
rpm -q samba
```

Expected:

```text
samba-<version>
```

---

## Alternative Verification

```bash
yum list installed samba
```

or

```bash
dnf list installed samba
```

---

# 📚 What is Samba?

**Samba** is an open-source implementation of the **SMB/CIFS** protocol.

It allows:

* 📂 File Sharing
* 🖨️ Printer Sharing
* 🖥️ Windows ↔ Linux file sharing
* 👥 Active Directory integration

---

# 🧪 Check Samba Version

```bash
smbd --version
```

Example:

```text
Version 4.15.x
```

---

# 🎯 Key Takeaways

✅ Install package:

```bash
sudo yum install -y samba
```

---

✅ Verify package:

```bash
rpm -q samba
```

---

✅ Check installed packages:

```bash
rpm -qa | grep samba
```

---

# 🎤 Interview Questions

### Q1. What is Samba?

**Answer:**

Samba is a software suite that enables file and printer sharing between Linux/Unix and Windows systems using the SMB/CIFS protocol.

---

### Q2. Which protocol does Samba use?

* SMB (**Server Message Block**)
* CIFS (**Common Internet File System**)

Default ports:

| Port | Protocol |
| ---- | -------- |
| 139  | NetBIOS  |
| 445  | SMB      |

---

### Q3. How do you install Samba?

```bash
sudo yum install -y samba
```

or

```bash
sudo dnf install -y samba
```

---

### Q4. How do you check if Samba is installed?

```bash
rpm -q samba
```

or

```bash
rpm -qa | grep samba
```

---

### Q5. What are the main Samba services?

| Service  | Purpose                   |
| -------- | ------------------------- |
| smbd     | File and printer sharing  |
| nmbd     | NetBIOS name service      |
| winbindd | AD and domain integration |

---

### Q6. What is the Samba configuration file?

```bash
/etc/samba/smb.conf
```

---

### Q7. How do you start Samba service?

```bash
sudo systemctl start smb
sudo systemctl enable smb
```

Check:

```bash
systemctl status smb
```

---

# 🌟 Task Status

✅ Samba Installed on stapp01
✅ Samba Installed on stapp02
✅ Samba Installed on stapp03
✅ Package Verified Successfully 🚀

---

## 📂 GitHub Repository Structure

```text
Linux/
└── Task-07-Install-Samba/
    ├── README.md
    └── screenshots/
        ├── samba-install-stapp01.png
        ├── samba-install-stapp02.png
        ├── samba-install-stapp03.png
        └── package-verification.png
```
