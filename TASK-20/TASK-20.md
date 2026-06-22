## ✅ Task-20: Configure Apache Security Headers 🔐

### 📌 Problem Statement

Harden the Apache Web Server on **App Server 3** by:

* Installing `httpd`
* Configuring Apache to run on **port 3004**
* Creating a sample webpage
* Enabling security response headers

---

### 🛠️ Install Apache

```bash
sudo yum install -y httpd
```

Verify:

```bash
rpm -q httpd
```

---

### 🔧 Configure Apache Port

Edit:

```bash
vi /etc/httpd/conf/httpd.conf
```

Change:

```text
Listen 80
```

to

```text
Listen 3004
```

Or use:

```bash
sed -i 's/^Listen.*/Listen 3004/' /etc/httpd/conf/httpd.conf
```

Verify:

```bash
grep "^Listen" /etc/httpd/conf/httpd.conf
```

Expected:

```text
Listen 3004
```

---

### 🌐 Create Website Content

```bash
echo "Welcome to the xFusionCorp Industries!" > /var/www/html/index.html
```

Verify:

```bash
cat /var/www/html/index.html
```

Expected:

```text
Welcome to the xFusionCorp Industries!
```

---

### 🔐 Configure Security Headers

Go to:

```bash
cd /etc/httpd/conf.d
```

Create:

```bash
vi security_headers.conf
```

Add:

```apache
Header always set X-XSS-Protection "1; mode=block"

Header always set X-Frame-Options "SAMEORIGIN"

Header always set X-Content-Type-Options "nosniff"
```

---

### ⚠️ Important Observation

Initially:

```bash
ls /etc/httpd/conf.d
```

Output:

```text
README
autoindex.conf
userdir.conf
welcome.conf
```

❗ `security_headers.conf` **does not exist by default**.

It must be **created manually**.

---

### 🔍 Verify Headers Module

```bash
httpd -M | grep headers
```

Expected:

```text
headers_module (shared)
```

---

### ✅ Validate Apache Configuration

```bash
httpd -t
```

Expected:

```text
Syntax OK
```

---

### 🚀 Start Apache

```bash
systemctl enable httpd

systemctl restart httpd
```

Check:

```bash
systemctl status httpd
```

Expected:

```text
active (running)
```

---

### 🔍 Verify Listening Port

```bash
ss -tulpn | grep 3004
```

Expected:

```text
LISTEN 0 128 *:3004
```

---

### 🌐 Verify Security Headers

```bash
curl -I http://localhost:3004
```

Expected:

```text
HTTP/1.1 200 OK

X-XSS-Protection: 1; mode=block

X-Frame-Options: SAMEORIGIN

X-Content-Type-Options: nosniff
```

---

### 🧠 Key Learnings

* Apache Installation using YUM
* Changing Apache Listening Port
* Apache Security Hardening
* HTTP Response Security Headers
* Configuration Validation with `httpd -t`
* Verifying HTTP Headers using `curl -I`

---

### 🎤 Interview Questions

**Q1. What is the purpose of X-XSS-Protection?**

```text
X-XSS-Protection: 1; mode=block
```

Protects against Cross-Site Scripting (XSS) attacks by blocking malicious scripts.

---

**Q2. What is X-Frame-Options SAMEORIGIN?**

Protects against **Clickjacking** attacks by allowing the page to be framed only from the same origin.

---

**Q3. What is X-Content-Type-Options nosniff?**

Prevents browsers from MIME type sniffing and forces them to use the declared content type.

---

**Q4. How do you test Apache configuration?**

```bash
httpd -t
```

---

**Q5. How do you verify HTTP response headers?**

```bash
curl -I http://localhost:3004
```

The `-I` option fetches only HTTP headers.

---

✅ **Task Status:** Completed Successfully 🚀
