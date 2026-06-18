# 🚀 Linux Administration - Task 11 | Configure Password-less Sudo for User `john`

## 📌 Objective

Provide **sudo access** to the user **`john`** on **all application servers** and configure **password-less sudo**.

### ✅ Requirements

* Add `john` to sudoers.
* User should execute sudo commands **without entering a password**.
* Perform on:

  * 🖥️ stapp01
  * 🖥️ stapp02
  * 🖥️ stapp03

---

# 🖥️ Step 1: Login to stapp01

```bash id="5a3o9k"
ssh tony@stapp01
```

Switch to root:

```bash id="5trm5w"
sudo su -
```

---

# Step 2: Create Sudoers Entry

**Recommended method (KodeKloud friendly):**

```bash id="b8g59y"
echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john
```

Set proper permissions:

```bash id="6c3yui"
sudo chmod 440 /etc/sudoers.d/john
```

---

# 🖥️ Repeat on stapp02

```bash id="edav72"
ssh steve@stapp02

echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john

sudo chmod 440 /etc/sudoers.d/john
```

---

# 🖥️ Repeat on stapp03

```bash id="mzkvmq"
ssh banner@stapp03

echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john

sudo chmod 440 /etc/sudoers.d/john
```

---

# ⚡ Shortcut Commands

### stapp01

```bash id="r7yzje"
ssh tony@stapp01 "echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john && sudo chmod 440 /etc/sudoers.d/john"
```

### stapp02

```bash id="c1ogwl"
ssh steve@stapp02 "echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john && sudo chmod 440 /etc/sudoers.d/john"
```

### stapp03

```bash id="l90fjv"
ssh banner@stapp03 "echo 'john ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/john && sudo chmod 440 /etc/sudoers.d/john"
```

---

# 🧪 Verification

Check the sudoers file:

```bash id="mbnzzn"
sudo cat /etc/sudoers.d/john
```

Expected:

```text id="n8j3h8"
john ALL=(ALL) NOPASSWD: ALL
```

---

## Verify Password-less Sudo

Switch to john:

```bash id="ttv0ui"
su - john
```

Run:

```bash id="80r4rx"
sudo ls /root
```

Expected:

```text id="ftxtou"
No password prompt
```

---

# 📚 Understanding the Sudoers Entry

```text id="fjlu79"
john ALL=(ALL) NOPASSWD: ALL
```

Breakdown:

| Part     | Meaning              |
| -------- | -------------------- |
| john     | Username             |
| ALL      | Any host             |
| (ALL)    | Run as any user      |
| NOPASSWD | No password required |
| ALL      | All commands         |

---

# ⚠️ Why Use `/etc/sudoers.d/` Instead of `/etc/sudoers`?

Best Practice:

```bash id="wx1o2n"
/etc/sudoers.d/
```

Reasons:

* Easier management
* Avoids editing main sudoers file
* Safer
* Modular configuration

---

# 🔍 Validate Sudoers Syntax

Always check:

```bash id="ovikux"
sudo visudo -c
```

Expected:

```text id="z8xj3x"
/etc/sudoers: parsed OK
/etc/sudoers.d/john: parsed OK
```

---

# 🎯 Key Takeaways

✅ Password-less sudo:

```bash id="h1ogmb"
john ALL=(ALL) NOPASSWD: ALL
```

---

✅ Store custom rules in:

```bash id="f5yx6v"
/etc/sudoers.d/
```

---

✅ Correct permission:

```bash id="0jx40h"
440
```

---

✅ Validate:

```bash id="u98tv5"
visudo -c
```

---

# 🎤 Interview Questions

### Q1. What is sudo?

**Answer:**

`sudo` allows a permitted user to execute commands as another user, usually root.

---

### Q2. What does this entry mean?

```text id="9fjz3h"
john ALL=(ALL) NOPASSWD: ALL
```

**Answer:**

User john can run any command as any user without entering a password.

---

### Q3. Where is sudo configuration stored?

Main file:

```bash id="jlwmie"
/etc/sudoers
```

Additional files:

```bash id="g1khie"
/etc/sudoers.d/
```

---

### Q4. What is the safest way to edit sudoers?

```bash id="qjlwmg"
visudo
```

Because:

* Performs syntax check
* Prevents simultaneous edits
* Avoids sudo lockout

---

### Q5. What permissions should sudoers files have?

```text id="nlj5ui"
440
```

Example:

```bash id="udbn6r"
chmod 440 /etc/sudoers.d/john
```

---

### Q6. How do you validate sudo configuration?

```bash id="rrjz3s"
visudo -c
```

---

### Q7. Difference between sudo and su?

| sudo                    | su                   |
| ----------------------- | -------------------- |
| Run one command as root | Switch to root shell |
| Audited                 | Less granular        |
| More secure             | Full root access     |

---

# 🌟 Task Status

✅ Sudo Access Granted to john on stapp01
✅ Sudo Access Granted to john on stapp02
✅ Sudo Access Granted to john on stapp03
✅ Password-less Sudo Configured
✅ Sudoers Validated Successfully 🚀
