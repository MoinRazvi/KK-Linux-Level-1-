# 🚀 Linux Administration - Task 05 | Password-less SSH Authentication

## 📌 Objective

Configure **password-less SSH authentication** from:

| Source    | Destination | User   |
| --------- | ----------- | ------ |
| Jump Host | stapp01     | tony   |
| Jump Host | stapp02     | steve  |
| Jump Host | stapp03     | banner |

After configuration:

```bash
ssh tony@stapp01
```

should log in **without asking for a password**.

---

# 🏗️ Architecture

```text
             Jump Host
             (thor)
                |
    -------------------------
    |           |           |
stapp01      stapp02      stapp03
 tony         steve        banner
```

---

# 🔑 Step 1: Login to Jump Host

You are already logged in as:

```bash
thor@jump-host
```

Check:

```bash
whoami
```

Output:

```text
thor
```

---

# 🔑 Step 2: Generate SSH Key Pair

Check if keys already exist:

```bash
ls -la ~/.ssh
```

If `id_rsa` and `id_rsa.pub` are present, **skip this step**.

Otherwise create:

```bash
ssh-keygen -t rsa
```

Press:

```text
Enter
Enter
Enter
```

No passphrase.

---

## Verify

```bash
ls ~/.ssh
```

Expected:

```text
id_rsa
id_rsa.pub
```

---

# 🖥️ Step 3: Copy Public Key to stapp01

```bash
ssh-copy-id tony@stapp01
```

Enter password once.

Expected:

```text
Number of key(s) added: 1
```

---

# 🖥️ Step 4: Copy Key to stapp02

```bash
ssh-copy-id steve@stapp02
```

Enter password.

---

# 🖥️ Step 5: Copy Key to stapp03

```bash
ssh-copy-id banner@stapp03
```

Enter password.

---

# 🧪 Step 6: Verify Password-less Login

### stapp01

```bash
ssh tony@stapp01
```

Expected:

```text
Last login: ...
[tony@stapp01 ~]$
```

No password prompt.

---

### stapp02

```bash
ssh steve@stapp02
```

---

### stapp03

```bash
ssh banner@stapp03
```

---

# ⚡ One-Line Alternative

If `ssh-copy-id` is not available:

For stapp01:

```bash
cat ~/.ssh/id_rsa.pub | ssh tony@stapp01 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

For stapp02:

```bash
cat ~/.ssh/id_rsa.pub | ssh steve@stapp02 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

For stapp03:

```bash
cat ~/.ssh/id_rsa.pub | ssh banner@stapp03 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

---

# 📂 How Password-less SSH Works

```text
thor generates:

Private Key:
~/.ssh/id_rsa

Public Key:
~/.ssh/id_rsa.pub


Public Key copied to:

~/.ssh/authorized_keys

When thor connects:

ssh tony@stapp01

↓

Server checks:

authorized_keys

↓

If matching public key exists

↓

Login succeeds without password
```

---

# 🔍 Verify Authorized Keys

On remote server:

```bash
cat ~/.ssh/authorized_keys
```

You should see:

```text
ssh-rsa AAAAB3Nza...
```

---

# 📋 Validation Checklist

✅ Key pair exists

```bash
ls ~/.ssh
```

---

✅ Password-less login works

```bash
ssh tony@stapp01
```

No password prompt.

---

✅ Check permissions

```bash
ls -ld ~/.ssh
ls -l ~/.ssh/authorized_keys
```

Expected:

```text
drwx------ .ssh
-rw------- authorized_keys
```

---

# 🎯 Key Takeaways

✅ `ssh-keygen`

Creates SSH key pair.

---

✅ `ssh-copy-id`

Copies public key to remote server.

```bash
ssh-copy-id user@host
```

---

✅ Private Key

```bash
~/.ssh/id_rsa
```

Never share it.

---

✅ Public Key

```bash
~/.ssh/id_rsa.pub
```

Copied to servers.

---

✅ Authorized Keys

```bash
~/.ssh/authorized_keys
```

Stores trusted public keys.

---

# 🎤 Interview Questions

### Q1. How does Password-less SSH work?

**Answer:**

SSH uses **public key cryptography**.

* Client stores private key.
* Server stores public key in:

```bash
~/.ssh/authorized_keys
```

During authentication, SSH verifies that the client owns the matching private key.

---

### Q2. What is the difference between id_rsa and id_rsa.pub?

| File       | Purpose     |
| ---------- | ----------- |
| id_rsa     | Private key |
| id_rsa.pub | Public key  |

Private key must never be shared.

---

### Q3. Where are SSH keys stored?

```bash
~/.ssh/
```

Common files:

```text
id_rsa
id_rsa.pub
authorized_keys
known_hosts
config
```

---

### Q4. What does ssh-copy-id do?

```bash
ssh-copy-id user@host
```

Copies your public key to:

```bash
~/.ssh/authorized_keys
```

on the remote server.

---

### Q5. How do you manually copy SSH keys?

```bash
cat ~/.ssh/id_rsa.pub | ssh user@host "cat >> ~/.ssh/authorized_keys"
```

---

### Q6. What is authorized_keys?

A file containing public keys allowed to log in.

Location:

```bash
~/.ssh/authorized_keys
```

---

### Q7. What permissions should .ssh directory have?

```text
~/.ssh             → 700
authorized_keys    → 600
id_rsa             → 600
id_rsa.pub         → 644
```

---

# 🌟 Task Status

✅ SSH Key Generated
✅ Public Key Copied to stapp01
✅ Public Key Copied to stapp02
✅ Public Key Copied to stapp03
✅ Password-less Authentication Enabled
✅ Task Completed Successfully 🚀

---

This is because of the **difference between an absolute path and your home directory**.

You created:

```bash
/ecommerce
```

Notice the **leading slash `/`**.

This means:

```text
/ecommerce
```

is created directly under the **root filesystem**, NOT inside:

```text
/home/steve
```

---

## Check Your Current Directory

Run:

```bash
pwd
```

If you are logged in as steve, you will see:

```text
/home/steve
```

Now list files:

```bash
ls
```

You won't see `/ecommerce` because it is **not inside your home directory**.

---

## How to View `/ecommerce`

Run:

```bash
cd /
ls
```

You should see:

```text
bin
boot
dev
ecommerce
etc
home
opt
tmp
usr
var
```

Or directly:

```bash
ls -ld /ecommerce
```

---

## Verify PHP Files Were Copied

### Method 1 - List all copied PHP files

```bash
find /ecommerce -type f -name "*.php"
```

Example:

```text
/ecommerce/var/www/html/ecommerce/index.php
/ecommerce/var/www/html/ecommerce/admin/config.php
/ecommerce/var/www/html/ecommerce/modules/cart/cart.php
```

---

### Method 2 - Count files

Source:

```bash
find /var/www/html/ecommerce -type f -name "*.php" | wc -l
```

Destination:

```bash
find /ecommerce -type f -name "*.php" | wc -l
```

Both counts should be the same.

Example:

```text
5
5
```

---

### Method 3 - View Directory Tree

If `tree` is installed:

```bash
tree /ecommerce
```

Otherwise:

```bash
find /ecommerce
```

---

## Important: Which Command Did You Use?

If you used:

```bash
find /var/www/html/ecommerce -type f -name "*.php" -exec cp --parents {} / \;
```

then files are copied like:

```text
/var/www/html/ecommerce/index.php
```

to:

```text
/var/www/html/ecommerce/index.php
```

which is **not what the task asks**.

---

## Correct KodeKloud Command

```bash
sudo mkdir -p /ecommerce

cd /var/www/html

find ecommerce -type f -name "*.php" -exec cp --parents {} /ecommerce \;
```

This creates:

```text
/ecommerce/ecommerce/index.php
/ecommerce/ecommerce/admin/config.php
/ecommerce/ecommerce/modules/cart/cart.php
```

---

## Quick Verification Command

Run this:

```bash
find /ecommerce -type f | head
```

and:

```bash
find /ecommerce -type f -name "*.php" | wc -l
```

If files appear, the task is completed successfully.

---

### Small Linux Tip 💡

* `/ecommerce` → Directory under root (`/`)
* `ecommerce` → Directory under your current location
* `~/ecommerce` → `/home/steve/ecommerce`
* `/home/steve/ecommerce` → Explicit path inside steve's home

This distinction between **absolute paths (`/`)** and **relative paths** is a very common Linux interview question.
