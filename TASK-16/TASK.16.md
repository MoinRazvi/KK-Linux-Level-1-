## ✅ Task-16: Configure HAProxy Load Balancer ⚖️

### 📌 Problem Statement

Configure **HAProxy** on the **LBR Server** to load balance traffic across all Nautilus application servers.

**Requirements:**

* Install HAProxy using `yum` only.
* Configure HAProxy to listen on **port 80**.
* Add all app servers as backend servers.
* Apache is running on **port 6400** on all app servers.
* Do **not** remove:

```text
stats socket /var/lib/haproxy/stats
```

---

### 🛠️ Configuration

**Frontend**

```cfg
frontend http_front
    bind *:80
    mode http
    default_backend http_back
```

**Backend**

```cfg
backend http_back
    mode http
    balance roundrobin

    server app1 stapp01:6400 check
    server app2 stapp02:6400 check
    server app3 stapp03:6400 check
```

---

### 🚀 Commands Used

```bash
sudo yum install -y haproxy

sudo vi /etc/haproxy/haproxy.cfg

sudo haproxy -c -f /etc/haproxy/haproxy.cfg

sudo systemctl enable haproxy

sudo systemctl restart haproxy

sudo systemctl status haproxy
```

---

### 🔍 Validation

Check configuration:

```bash
haproxy -c -f /etc/haproxy/haproxy.cfg
```

Expected Output:

```text
Configuration file is valid
```

Verify service:

```bash
systemctl is-active haproxy
```

Expected:

```text
active
```

Test Load Balancer:

```bash
curl http://localhost:80
```

---

### 🧠 Key Learnings

* HAProxy Frontend and Backend configuration
* Round Robin Load Balancing
* Health Checks using `check`
* Service Management using `systemctl`
* Configuration Validation using `haproxy -c`

---

### 🎤 Interview Questions

**Q1. What is HAProxy?**

HAProxy is an open-source TCP/HTTP Load Balancer and Reverse Proxy used to distribute traffic across multiple backend servers.

**Q2. What is the difference between Load Balancer and Reverse Proxy?**

* Load Balancer → Distributes requests among multiple servers.
* Reverse Proxy → Acts as a single entry point and forwards requests to backend servers.

**Q3. What does `balance roundrobin` do?**

It distributes incoming requests sequentially among backend servers.

**Q4. How do you validate HAProxy configuration?**

```bash
haproxy -c -f /etc/haproxy/haproxy.cfg
```

**Q5. Where is the HAProxy configuration file located?**

```bash
/etc/haproxy/haproxy.cfg
```

---

✅ **Task Status:** Completed Successfully 🚀
