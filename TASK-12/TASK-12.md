# 🚀 Linux Administration - Task 12 | Configure Google Public DNS on App Server 3

## 📌 Objective

The Nautilus team identified DNS resolution issues on **App Server 3 (`stapp03`)**.

As a temporary fix, configure **Google Public DNS (IPv4)** on the server.

### ✅ Google Public DNS Servers

```text id="p9vw9e"
8.8.8.8
8.8.4.4
```

---

# 🖥️ Step 1: Login to App Server 3

```bash id="y8nmbm"
ssh banner@stapp03
```

Become root:

```bash id="8vth26"
sudo su -
```

---

# 🔍 Step 2: Check Existing DNS Configuration

```bash id="97tkws"
cat /etc/resolv.conf
```

Example:

```text id="3ykhcg"
nameserver 127.0.0.53
```

or

```text id="1gr0mb"
nameserver 10.x.x.x
```

---

# ✏️ Step 3: Add Google DNS Entries

Edit:

```bash id="jlwm9a"
vi /etc/resolv.conf
```

Add:

```text id="wofz26"
nameserver 8.8.8.8
nameserver 8.8.4.4
```

Save:

```text id="eq3y3o"
Esc
:wq
```

---

# ⚡ Faster Method

You can directly append:

```bash id="r7lyqk"
echo "nameserver 8.8.8.8" >> /etc/resolv.conf

echo "nameserver 8.8.4.4" >> /etc/resolv.conf
```

---

# 🧪 Verification

Check:

```bash id="zvv0to"
cat /etc/resolv.conf
```

Expected:

```text id="ehloi4"
nameserver 8.8.8.8
nameserver 8.8.4.4
```

---

# 🔍 Test DNS Resolution

Ping Google:

```bash id="uslgkx"
ping -c 3 google.com
```

Example:

```text id="t7rqil"
PING google.com ...

3 packets transmitted, 3 received
```

---

# Alternative Test

```bash id="9r5ygh"
nslookup google.com
```

or

```bash id="4bq3j4"
host google.com
```

---

# 📚 What is `/etc/resolv.conf`?

It is the DNS resolver configuration file.

Location:

```bash id="t6r7kr"
/etc/resolv.conf
```

It contains:

```text id="vmflqg"
nameserver 8.8.8.8
nameserver 8.8.4.4
```

The system queries these DNS servers to resolve domain names.

---

# 📚 DNS Resolution Flow

```text id="0yjlwm"
google.com

    ↓

/etc/resolv.conf

    ↓

8.8.8.8

    ↓

Returns IP Address

142.250.x.x
```

---

# 📚 Popular Public DNS Servers

| Provider             | DNS            |
| -------------------- | -------------- |
| Google               | 8.8.8.8        |
| Google Secondary     | 8.8.4.4        |
| Cloudflare           | 1.1.1.1        |
| Cloudflare Secondary | 1.0.0.1        |
| OpenDNS              | 208.67.222.222 |

---

# 🎯 Key Takeaways

✅ DNS configuration file:

```bash id="jlwmyy"
/etc/resolv.conf
```

---

✅ Google DNS:

```text id="womr0q"
8.8.8.8
8.8.4.4
```

---

✅ Check DNS:

```bash id="k4m4tx"
cat /etc/resolv.conf
```

---

✅ Test DNS:

```bash id="gns9jl"
ping google.com
```

or

```bash id="lyrqwi"
nslookup google.com
```

---

# 🎤 Interview Questions

### Q1. What is DNS?

**Answer:**

DNS (**Domain Name System**) translates domain names into IP addresses.

Example:

```text id="q0j9v4"
google.com

↓

142.250.x.x
```

---

### Q2. Which file stores DNS servers in Linux?

```bash id="0wr0xw"
/etc/resolv.conf
```

---

### Q3. What are Google's public DNS servers?

```text id="bmyjlwm"
8.8.8.8
8.8.4.4
```

---

### Q4. How do you verify DNS resolution?

```bash id="xucskw"
nslookup google.com
```

or

```bash id="s67f4s"
host google.com
```

---

### Q5. Difference between DNS and `/etc/hosts`?

| DNS                           | `/etc/hosts`         |
| ----------------------------- | -------------------- |
| Network-based name resolution | Local static mapping |
| Centralized                   | Local machine only   |
| Dynamic                       | Manual entries       |

---

### Q6. What happens if DNS is not working?

* Domain names cannot be resolved.
* Internet connectivity by IP may still work.
* Applications depending on hostnames may fail.

---

### Q7. How do you test connectivity to DNS server?

```bash id="o8c0ja"
ping 8.8.8.8
```

If successful:

* Network is working.
* DNS issue may be only name resolution.

---

# 🌟 Task Status

✅ Logged into stapp03
✅ Google Public DNS Added
✅ `/etc/resolv.conf` Updated
✅ DNS Resolution Verified
✅ Task Completed Successfully 🚀
