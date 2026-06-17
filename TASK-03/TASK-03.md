# 🚀 Linux Administration - Task 03 | Collaborative Directory Setup

## 📌 Objective

The Nautilus team wants to create a **secure collaborative directory** on **App Server 3** that can only be accessed by members of the **sysops** group.

### ✅ Requirements

* Create directory: `/sysops/data`
* Group owner: `sysops`
* Files created inside should automatically belong to `sysops`
* User and group should have **rwx** permissions
* Others should have **no access**

---

# 🖥️ Step 1: Login to App Server 3

From jump host:

```bash
ssh banner@stapp03
```

---

# 📁 Step 2: Create the Directory

```bash
sudo mkdir -p /sysops/data
```

### Verify

```bash
ls -ld /sysops/data
```

---

# 👥 Step 3: Change Group Ownership

Assign the directory to the **sysops** group:

```bash
sudo chgrp sysops /sysops/data
```

OR

```bash
sudo chown :sysops /sysops/data
```

Verify:

```bash
ls -ld /sysops/data
```

Expected:

```text
drwxr-xr-x root sysops ...
```

---

# 🔒 Step 4: Set Permissions

Give:

* Owner → rwx (7)
* Group → rwx (7)
* Others → --- (0)

```bash
sudo chmod 770 /sysops/data
```

---

# 🔄 Step 5: Enable SGID Bit

This is the **most important step**.

To ensure files created inside inherit the **sysops** group:

```bash
sudo chmod g+s /sysops/data
```

or

```bash
sudo chmod 2770 /sysops/data
```

---

# ✅ Verify Final Permissions

```bash
ls -ld /sysops/data
```

Expected:

```text
drwxrws--- 2 root sysops ... /sysops/data
```

Notice:

```text
rws
 ^
SGID bit is set
```

---

# 🎯 Final Commands (Shortcut)

```bash
sudo mkdir -p /sysops/data
sudo chown :sysops /sysops/data
sudo chmod 2770 /sysops/data
```

That's all you need for the KodeKloud exam. ✅

---

# 🧪 Validation

Check:

```bash
ls -ld /sysops/data
```

Expected:

```text
drwxrws--- root sysops /sysops/data
```

---

# 📚 Understanding Permission 2770

```text
2 770

2 → SGID bit
7 → Owner rwx
7 → Group rwx
0 → Others ---
```

---

# 🔥 Why Use SGID?

Without SGID:

```text
user1 creates file
→ file group = user1's primary group
```

With SGID:

```text
user1 creates file in /sysops/data
→ file group = sysops
```

This is how teams share files safely.

---

# 🖼️ Permission Breakdown

```text
drwxrws---

d     → Directory
rwx   → Owner permissions
rws   → Group permissions + SGID
---   → Others no access
```

---

# 📋 Validation Checklist

✅ Directory exists

```bash
ls -ld /sysops/data
```

✅ Group owner is sysops

```bash
stat -c "%G" /sysops/data
```

Expected:

```text
sysops
```

✅ SGID enabled

```bash
ls -ld /sysops/data
```

Should show:

```text
drwxrws---
```

---

# 🎯 Key Takeaways

✅ `mkdir -p` → Creates directories recursively.

✅ `chgrp` or `chown :group` → Changes group ownership.

✅ `chmod 770` → Owner and Group full access.

✅ `chmod g+s` → Enables SGID.

✅ `chmod 2770` → Combines SGID + permissions in one command.

---

# 🎤 Interview Questions

### Q1. What is SGID in Linux?

**Answer:**

SGID (Set Group ID) on a directory ensures that all files and subdirectories created inside inherit the parent directory's group ownership.

Example:

```bash
chmod g+s /shared
```

or

```bash
chmod 2770 /shared
```

---

### Q2. What is the difference between SUID and SGID?

| SUID                                   | SGID                                   |
| -------------------------------------- | -------------------------------------- |
| Affects executable files               | Mostly used on directories             |
| Runs with owner's permissions          | Files inherit directory group          |
| Permission shown as `s` in owner field | Permission shown as `s` in group field |

---

### Q3. What does permission 770 mean?

```text
770

Owner → rwx = 7
Group → rwx = 7
Others → --- = 0
```

Only owner and group members can access.

---

### Q4. What does 2770 mean?

```text
2 → SGID
7 → Owner rwx
7 → Group rwx
0 → Others no access
```

---

### Q5. Difference between chown and chgrp?

| Command | Purpose                |
| ------- | ---------------------- |
| chown   | Change owner and group |
| chgrp   | Change only group      |

Examples:

```bash
chown user:sysops file
chgrp sysops file
```

---

### Q6. How do you check file permissions?

```bash
ls -l
```

For directories:

```bash
ls -ld /sysops/data
```

---

### Q7. How do you check detailed file information?

```bash
stat /sysops/data
```

---

# 🌟 Task Status

✅ Directory Created
✅ Group Ownership Set to `sysops`
✅ Permissions Set to `2770`
✅ SGID Enabled
✅ Others Restricted
✅ Collaborative Directory Ready 🚀

---

## 📂 GitHub Repository Structure

```text
Linux/
└── Task-03-Collaborative-Directory/
    ├── README.md
    └── screenshots/
        ├── directory-created.png
        ├── permissions.png
        └── sgid-enabled.png
```
