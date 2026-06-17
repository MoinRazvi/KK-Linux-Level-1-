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
