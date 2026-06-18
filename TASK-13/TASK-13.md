# 🚀 Linux Administration - Task 13 | Configure Firewalld on App Server 3

## 📌 Objective

Configure **firewalld** on **App Server 3 (`stapp03`)** with the following requirements:

### ✅ Requirements

| Service | Port | Action |
| ------- | ---: | ------ |
| Nginx   |   80 | Allow  |
| Apache  | 8085 | Block  |

Additional requirements:

* Rules must be **permanent**
* Use **public** zone
* Ensure **Nginx** and **Apache** services are running

---

# 🖥️ Step 1: Login to App Server 3

```bash id="98pk0h"
ssh banner@stapp03
```

Become root:

```bash id="sqcv4w"
sudo su -
```

---

# 🔍 Step 2: Check Firewalld Status

```bash id="u8wyic"
systemctl status firewalld
```

If not running:

```bash id="aotbqh"
systemctl enable firewalld --now
```

Verify:

```bash id="bjlsu8"
firewall-cmd --state
```

Expected:

```text id="9ejxya"
running
```

---

# 🌐 Step 3: Allow Port 80 for Nginx

```bash id="fawyeu"
firewall-cmd --permanent --zone=public --add-port=80/tcp
```

Expected:

```text id="xhgwtw"
success
```

---

# 🚫 Step 4: Block Port 8085 for Apache

If port 8085 is already allowed:

```bash id="d6vtss"
firewall-cmd --permanent --zone=public --remove-port=8085/tcp
```

Expected:

```text id="w86dfy"
success
```

If you get:

```text id="pybz9j"
Warning: NOT_ENABLED
```

That's perfectly fine—the port is already blocked.

---

# 🔄 Step 5: Reload Firewalld

```bash id="xrfx4r"
firewall-cmd --reload
```

Expected:

```text id="8l7yd2"
success
```

---

# 🖥️ Step 6: Start Apache Service

Check:

```bash id="jlwmm5"
systemctl status httpd
```

If inactive:

```bash id="0l4jca"
systemctl start httpd
```

Verify:

```bash id="zjlwmn"
systemctl is-active httpd
```

Expected:

```text id="suf0q2"
active
```

---

# 🌐 Step 7: Start Nginx Service

Check:

```bash id="sr0fth"
systemctl status nginx
```

If inactive:

```bash id="2qk6iu"
systemctl start nginx
```

Verify:

```bash id="56jlwm"
systemctl is-active nginx
```

Expected:

```text id="yjbzzu"
active
```

---

# 🧪 Step 8: Verify Firewall Rules

Check public zone:

```bash id="g4s59s"
firewall-cmd --zone=public --list-ports
```

Expected:

```text id="2njmyy"
80/tcp
```

**Important:** You should **NOT** see:

```text id="4lj50w"
8085/tcp
```

---

# ⚡ Quick KodeKloud Solution

```bash id="kwnf9u"
sudo su -

systemctl enable firewalld --now

firewall-cmd --permanent --zone=public --add-port=80/tcp

firewall-cmd --permanent --zone=public --remove-port=8085/tcp

firewall-cmd --reload

systemctl start httpd

systemctl start nginx
```

---

# 🧪 Final Verification

### Firewall Status

```bash id="ay5ct1"
firewall-cmd --state
```

Expected:

```text id="fg5e4h"
running
```

---

### Allowed Ports

```bash id="5s6cye"
firewall-cmd --zone=public --list-ports
```

Expected:

```text id="axxmxh"
80/tcp
```

---

### Apache Status

```bash id="i5r1mr"
systemctl is-active httpd
```

Expected:

```text id="f4huxc"
active
```

---

### Nginx Status

```bash id="2gk44r"
systemctl is-active nginx
```

Expected:

```text id="j4zhqh"
active
```

---

# 📚 What is Firewalld?

`firewalld` is a dynamic firewall management service that manages:

* Ports
* Services
* Rich rules
* Zones

---

# 📚 What is a Zone?

A zone is a predefined firewall trust level.

Common zones:

| Zone     | Description          |
| -------- | -------------------- |
| public   | Public networks      |
| home     | Trusted home network |
| work     | Office network       |
| internal | Internal network     |
| trusted  | All traffic allowed  |

---

# 📚 Permanent vs Runtime Rules

| Runtime           | Permanent       |
| ----------------- | --------------- |
| Lost after reboot | Survives reboot |
| Immediate         | Requires reload |

Example:

```bash id="jlwm76"
firewall-cmd --add-port=80/tcp
```

Temporary.

---

```bash id="jlwm77"
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --reload
```

Permanent.

---

# 🎯 Key Takeaways

✅ Allow port:

```bash id="jlwm78"
firewall-cmd --permanent --add-port=80/tcp
```

---

✅ Remove port:

```bash id="jlwm79"
firewall-cmd --permanent --remove-port=8085/tcp
```

---

✅ Reload firewall:

```bash id="jlwm80"
firewall-cmd --reload
```

---

✅ List allowed ports:

```bash id="jlwm81"
firewall-cmd --list-ports
```

---

# 🎤 Interview Questions

### Q1. What is firewalld?

**Answer:**

`firewalld` is a dynamic firewall management daemon that manages firewall rules using zones and services.

---

### Q2. Difference between Runtime and Permanent rules?

| Runtime           | Permanent       |
| ----------------- | --------------- |
| Temporary         | Persistent      |
| Lost after reboot | Survives reboot |

---

### Q3. How do you allow a port permanently?

```bash id="jlwm82"
firewall-cmd --permanent --add-port=80/tcp

firewall-cmd --reload
```

---

### Q4. How do you block a port?

```bash id="jlwm83"
firewall-cmd --permanent --remove-port=8085/tcp
```

---

### Q5. How do you check the active zone?

```bash id="jlwm84"
firewall-cmd --get-active-zones
```

---

### Q6. How do you list allowed ports?

```bash id="jlwm85"
firewall-cmd --list-ports
```

---

### Q7. Difference between iptables and firewalld?

| iptables       | firewalld       |
| -------------- | --------------- |
| Static rules   | Dynamic rules   |
| Complex syntax | Easy management |
| No zones       | Supports zones  |

---

# 🌟 Task Status

✅ Firewalld Enabled
✅ Port 80 Allowed
✅ Port 8085 Blocked
✅ Rules Made Permanent
✅ Apache Running
✅ Nginx Running
✅ Task Completed Successfully 🚀
