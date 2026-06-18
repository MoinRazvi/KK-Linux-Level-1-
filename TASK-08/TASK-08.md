# 🚀 Linux Administration - Task 08 | Install Ansible 4.8.0 using pip3

## 📌 Objective

Install **Ansible version 4.8.0** on the **Jump Host** using **pip3 only**.

### Requirements

✅ Install using `pip3`

✅ Version must be exactly **4.8.0**

✅ Ansible command should be available globally for all users.

---

# 🖥️ Step 1: Login to Jump Host

```bash
ssh thor@jump_host
```

Verify:

```bash
whoami
```

Output:

```text
thor
```

---

# 🔍 Step 2: Check Python and pip3

```bash
python3 --version

pip3 --version
```

Example:

```text
Python 3.x.x

pip 21.x
```

---

# 📦 Step 3: Install Ansible 4.8.0

Install globally using sudo:

```bash
sudo pip3 install ansible==4.8.0
```

This installs:

* ansible 4.8.0
* ansible-core compatible version

---

# 🔍 Step 4: Verify Installation

```bash
ansible --version
```

Expected:

```text
ansible [core 2.11.x]

ansible 4.8.0
```

---

# 🧪 Step 5: Verify Global Availability

Switch to another user:

```bash
sudo su -

ansible --version
```

or

```bash
sudo su - root

ansible --version
```

If it displays the version successfully, then Ansible is available globally.

---

# 🚨 If You Get "ansible: command not found"

Check installation path:

```bash
sudo pip3 show ansible
```

or

```bash
which ansible
```

Example:

```text
/usr/local/bin/ansible
```

---

# Add to Global PATH (if required)

```bash
echo 'export PATH=$PATH:/usr/local/bin' | sudo tee /etc/profile.d/ansible.sh

source /etc/profile.d/ansible.sh
```

---

# Verify Again

```bash
ansible --version
```

---

# ⚡ One-Line Exam Solution

```bash
sudo pip3 install ansible==4.8.0

ansible --version
```

This is usually sufficient for the KodeKloud task.

---

# 📚 What is Ansible?

**Ansible** is an open-source **Configuration Management** and **Automation** tool.

It is used for:

* Server configuration
* Application deployment
* Package installation
* User management
* Infrastructure automation

---

# 📚 Ansible Architecture

```text
          Control Node
         (Jump Host)
               |
    -----------------------
    |         |          |
stapp01    stapp02    stapp03
 Managed    Managed    Managed
  Node       Node       Node
```

No agents are required on managed nodes.

---

# 📚 Why Ansible is Popular?

✅ Agentless

✅ Uses SSH

✅ YAML Playbooks

✅ Easy to learn

✅ Idempotent

---

# 🎯 Key Takeaways

✅ Install:

```bash
sudo pip3 install ansible==4.8.0
```

✅ Verify:

```bash
ansible --version
```

✅ Check binary:

```bash
which ansible
```

✅ Global binary path:

```bash
/usr/local/bin/ansible
```

---

# 🎤 Interview Questions

### Q1. What is Ansible?

**Answer:**

Ansible is an open-source automation and configuration management tool that automates server provisioning, configuration, and application deployment using SSH.

---

### Q2. Why is Ansible called Agentless?

**Answer:**

Ansible does not require any software (agent) to be installed on managed nodes.

It communicates using:

* SSH (Linux)
* WinRM (Windows)

---

### Q3. What are the components of Ansible?

| Component    | Description                        |
| ------------ | ---------------------------------- |
| Control Node | Machine where Ansible is installed |
| Managed Node | Target servers                     |
| Inventory    | List of hosts                      |
| Playbook     | YAML automation file               |
| Module       | Unit of work                       |

---

### Q4. What is an Inventory file?

It contains the list of servers managed by Ansible.

Example:

```ini
[appservers]
stapp01
stapp02
stapp03
```

---

### Q5. What is a Playbook?

A YAML file containing automation tasks.

Example:

```yaml
---
- hosts: appservers
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present
```

---

### Q6. What protocol does Ansible use?

**SSH**

Default port:

```text
22
```

---

### Q7. What is Idempotency in Ansible?

**Answer:**

Running the same playbook multiple times produces the same result without causing unwanted changes.

Example:

If nginx is already installed:

```yaml
state: present
```

Ansible won't reinstall it.

---

# 🌟 Task Status

✅ Ansible 4.8.0 Installed using pip3
✅ Global Binary Available
✅ Installation Verified Successfully 🚀

---

### Why cant we install through yum and what is the difference between pip and yum

This is an excellent Linux and DevOps interview question.

## Why can't we use `yum` in this task?

Because the task **explicitly says**:

> **"Install Ansible version 4.8.0 on Jump host using pip3 only."**

In KodeKloud exams, if the requirement says:

```text
using pip3 only
```

then even if `yum` works, **the task validation may fail** because the checker verifies the installation method and version.

---

## What if we use yum?

```bash
sudo yum install ansible -y
```

The problem is:

1. It installs the version available in the OS repository.
2. That version may not be **Ansible 4.8.0**.
3. KodeKloud tasks often require an **exact version**.

For example:

```bash
yum info ansible
```

might show:

```text
ansible-2.9
```

while the task requires:

```text
ansible==4.8.0
```

---

# Difference Between pip and yum

| Feature             | pip              | yum                |
| ------------------- | ---------------- | ------------------ |
| Used for            | Python packages  | OS packages        |
| Repository          | PyPI             | Linux repositories |
| Installs            | Python libraries | RPM packages       |
| Version flexibility | Very high        | Depends on repo    |
| Package type        | `.whl`, source   | `.rpm`             |
| Example             | ansible, boto3   | httpd, samba       |

---

## yum installs operating system packages

Example:

```bash
sudo yum install samba -y
```

This installs:

* samba
* rpm package
* OS dependencies

---

## pip installs Python packages

Example:

```bash
pip3 install boto3
```

This installs:

* boto3 library
* Python modules
* Packages from PyPI

---

# Why Ansible can be installed by both?

Because **Ansible is written in Python**.

Therefore:

### Method 1

```bash
sudo yum install ansible
```

Installs:

```text
ansible RPM package
```

---

### Method 2

```bash
sudo pip3 install ansible==4.8.0
```

Installs:

```text
ansible Python package from PyPI
```

---

# Real DevOps Practice

### Install system tools with yum

```bash
sudo yum install

git
docker
httpd
nginx
samba
```

---

### Install Python libraries with pip

```bash
pip3 install

ansible
boto3
requests
flask
django
```

---

# Where are packages installed?

### yum

```bash
rpm -ql samba
```

Output:

```text
/usr/sbin/smbd
/etc/samba/
/usr/share/doc/
```

---

### pip

```bash
pip3 show ansible
```

Output:

```text
Location:
/usr/local/lib/python3.x/site-packages
```

Binary:

```bash
which ansible
```

Example:

```text
/usr/local/bin/ansible
```

---

# Which one is preferred in companies?

### OS Packages (`yum`)

Used for:

* httpd
* nginx
* docker
* samba
* mariadb

Reason:

* Stable
* Vendor tested
* Security patches

---

### pip

Used for:

* Ansible specific versions
* boto3
* awscli
* Python applications
* Virtual environments

Reason:

* Easy version control

---

# Why DevOps engineers often prefer pip for Ansible?

Suppose:

```text
Server Repo → Ansible 2.9
Project requires → Ansible 4.8.0
```

With yum:

```bash
sudo yum install ansible
```

❌ Wrong version

With pip:

```bash
sudo pip3 install ansible==4.8.0
```

✅ Exact version installed

---

# Interview Question ⭐

### Q: Why install Ansible using pip instead of yum?

**Answer:**

* `yum` installs the version available in the operating system repositories.
* `pip` installs Python packages directly from PyPI and allows installing an exact version.
* DevOps teams often use `pip` to maintain version consistency across environments.

---

# Quick Memory Trick

```text
yum  → OS Package Manager
pip  → Python Package Manager

yum installs RPMs
pip installs Python packages

yum → samba, nginx, docker
pip → ansible, boto3, flask
```

This distinction between **OS package managers (`yum`, `dnf`, `apt`)** and **language package managers (`pip`, `npm`, `gem`)** is one of the most common DevOps interview topics.

