# 🚀 Linux Administration - Task 02 | Update Message of the Day (MOTD)

## 📌 Objective

During the monthly compliance audit, the security team found that application servers do not have the approved login banner.

Your task is to **copy the approved banner file** from the jump host to **all Nautilus application servers** and configure it as the **Message of the Day (MOTD)**.

---

## 🏗️ Environment

| 🖥️ Server | 👤 User |
| ---------- | ------- |
| stapp01    | tony    |
| stapp02    | steve   |
| stapp03    | banner  |

📂 Approved banner file on Jump Host:

```bash
/home/thor/nautilus_banner
```

---

# 🔍 Step 1: Verify the Banner File on Jump Host

```bash
cat /home/thor/nautilus_banner
```

or

```bash
ls -l /home/thor/nautilus_banner
```

---

# 📤 Step 2: Copy Banner to stapp01

From the jump host:

```bash
scp /home/thor/nautilus_banner tony@stapp01:/tmp/
```

Login:

```bash
ssh tony@stapp01
```

Move the file to `/etc/motd`:

```bash
sudo cp /tmp/nautilus_banner /etc/motd
```

Verify:

```bash
cat /etc/motd
```

Exit:

```bash
exit
```

---

# 📤 Step 3: Copy Banner to stapp02

```bash
scp /home/thor/nautilus_banner steve@stapp02:/tmp/
```

Login:

```bash
ssh steve@stapp02
```

Copy:

```bash
sudo cp /tmp/nautilus_banner /etc/motd
```

Verify:

```bash
cat /etc/motd
```

Exit:

```bash
exit
```

---

# 📤 Step 4: Copy Banner to stapp03

```bash
scp /home/thor/nautilus_banner banner@stapp03:/tmp/
```

Login:

```bash
ssh banner@stapp03
```

Copy:

```bash
sudo cp /tmp/nautilus_banner /etc/motd
```

Verify:

```bash
cat /etc/motd
```

Exit:

```bash
exit
```

---

# ⚡ One-Liner Alternative

After logging into each server:

```bash
sudo cp /tmp/nautilus_banner /etc/motd
```

---

# ✅ Validation

### Check MOTD File

```bash
cat /etc/motd
```

Output should exactly match:

```bash
cat /home/thor/nautilus_banner
```

---

## 🧪 Test Login Banner

Logout and login again:

```bash
exit
ssh tony@stapp01
```

After successful login, you should see:

```text
<Contents of nautilus_banner>
```

---

# 📂 What is MOTD?

**MOTD** stands for:

> **Message Of The Day**

It is a text file displayed to users **after successful login**.

Location:

```bash
/etc/motd
```

---

# 📁 Important Banner Files in Linux

| File             | Purpose                      |
| ---------------- | ---------------------------- |
| `/etc/motd`      | Displayed after login        |
| `/etc/issue`     | Displayed before local login |
| `/etc/issue.net` | Displayed before SSH login   |
| `/etc/profile`   | Global shell environment     |
| `/etc/bashrc`    | Global bash settings         |

---

# 🎯 Key Takeaways

✅ MOTD = Message Of The Day

✅ MOTD file location:

```bash
/etc/motd
```

✅ Copy file:

```bash
cp source destination
```

✅ Secure copy between servers:

```bash
scp file user@host:path
```

✅ MOTD is displayed **after successful login**.

---

# 🎤 Interview Questions

## Q1. What is MOTD in Linux?

**Answer:**

MOTD stands for **Message Of The Day**. It is a text message displayed to users after they successfully log in to a Linux system.

---

## Q2. Where is the MOTD file located?

```bash
/etc/motd
```

---

## Q3. What is the difference between `/etc/motd` and `/etc/issue`?

| `/etc/motd`                | `/etc/issue`           |
| -------------------------- | ---------------------- |
| Displayed after login      | Displayed before login |
| User already authenticated | User not authenticated |
| Used for announcements     | Used for login banners |

---

## Q4. What is SCP?

**SCP (Secure Copy)** is used to securely copy files between Linux systems over SSH.

Example:

```bash
scp file.txt user@server:/tmp/
```

---

## Q5. How do you copy a file in Linux?

```bash
cp source destination
```

Example:

```bash
cp /tmp/nautilus_banner /etc/motd
```

---

## Q6. How do you display the contents of a file?

```bash
cat filename
```

Example:

```bash
cat /etc/motd
```

---

## Q7. What is the difference between SCP and CP?

| SCP                       | CP               |
| ------------------------- | ---------------- |
| Copies files over network | Copies locally   |
| Uses SSH                  | Does not use SSH |
| Secure                    | Local only       |

---

# 🌟 Task Status

✅ Approved Banner Verified
✅ Banner Copied to stapp01
✅ Banner Copied to stapp02
✅ Banner Copied to stapp03
✅ `/etc/motd` Updated Successfully
✅ Compliance Requirement Met 🚀

---

## 📌 GitHub Repository Structure

```text
Linux/
└── Task-02-MOTD-Banner/
    ├── README.md
    └── screenshots/
        ├── banner-file.png
        ├── motd-update.png
        └── login-banner.png
```
