## ✅ Task-17: Troubleshoot HAProxy Service 🔧

### 📌 Problem Statement

The monitoring team identified an issue with the **HAProxy service** on the LBR server (`stlb01`).

**Requirements:**

* Troubleshoot HAProxy service failure.
* Fix the configuration issue.
* Ensure HAProxy service is running.
* Verify the website using:

```bash
curl http://stlb01:80/
```

---

### 🔍 Issue Observed

Initially:

```bash
systemctl status haproxy
```

Output:

```text
Active: failed
```

Website check:

```bash
curl http://stlb01:80/
```

Output:

```html
503 Service Unavailable
No server is available to handle this request.
```

---

### 🛠️ Root Cause Analysis

Verified backend connectivity:

```bash
curl http://stapp01:6400
curl http://stapp02:6400
curl http://stapp03:6400
```

Output:

```text
Connection refused
```

Then checked Apache:

```bash
grep "^Listen" /etc/httpd/conf/httpd.conf
```

Output:

```text
Listen 8080
```

Backend servers were running on **8080**, while HAProxy was configured for **6400**.

---

### ✅ Solution

Updated HAProxy backend configuration:

```cfg
backend http_back
    mode http
    balance roundrobin

    server app1 stapp01:8080 check
    server app2 stapp02:8080 check
    server app3 stapp03:8080 check
```

---

### 🚀 Commands Used

```bash
sudo vi /etc/haproxy/haproxy.cfg

sudo haproxy -c -f /etc/haproxy/haproxy.cfg

sudo systemctl restart haproxy

sudo systemctl status haproxy

curl http://stlb01:80/
```

---

### 🔍 Validation

Check HAProxy:

```bash
systemctl is-active haproxy
```

Expected:

```text
active
```

Validate website:

```bash
curl http://stlb01:80/
```

Expected:

```html
<html>
...
Website Content
...
</html>
```

---

### 🧠 Key Learnings

* HAProxy Frontend and Backend concepts
* Backend Health Checks
* Load Balancer Troubleshooting
* Relationship between Load Balancer and App Servers
* Troubleshooting HTTP 503 Errors

---

### 🎤 Interview Questions

**Q1. Why do we get 503 Service Unavailable in HAProxy?**

Because HAProxy cannot reach any healthy backend server.

---

**Q2. What does this command do?**

```bash
curl http://stlb01:80/
```

It sends a request to HAProxy, which forwards it to one of the backend application servers.

---

**Q3. What is the purpose of `check` in HAProxy?**

```cfg
server app1 stapp01:8080 check
```

It enables health checks for backend servers.

---

**Q4. How do you validate HAProxy configuration?**

```bash
haproxy -c -f /etc/haproxy/haproxy.cfg
```

---

✅ **Task Status:** Completed Successfully 🚀
---

### 🔄 Relationship between `curl http://stlb01:80/` and App Servers

When you run:

```bash
curl http://stlb01:80/
```

You are **not accessing the website directly from the Load Balancer**.

The flow is:

```text
                 User

                   │

                   ▼

          curl http://stlb01:80

                   │

          +-----------------+
          | HAProxy (stlb01)|
          | Listening :80   |
          +-----------------+

           │        │        │

           ▼        ▼        ▼

     stapp01   stapp02   stapp03
       :8080     :8080     :8080

        Apache    Apache    Apache
```

HAProxy receives the request on **port 80** and forwards it to one of the backend servers.

Because your app servers were listening on:

```text
8080
```

you changed HAProxy:

```cfg
backend http_back
    balance roundrobin

    server app1 stapp01:8080 check
    server app2 stapp02:8080 check
    server app3 stapp03:8080 check
```

Now:

```bash
curl http://stlb01:80/
```

works because:

```text
stlb01:80
   ↓
HAProxy
   ↓
stapp01:8080 OR stapp02:8080 OR stapp03:8080
   ↓
Website Response
```

---
