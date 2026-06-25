# 🚀 Task-24: Install and Configure iptables Firewall

## 🎯 Objective

On the **Backup Server**:

* Install **iptables**.
* Allow incoming traffic on **Nginx (8096)**.
* Block incoming traffic on **Apache (3002)**.
* Make the rules **persistent**.

---

## 🖥️ Server Details

| Server  | User                                       |
| ------- | ------------------------------------------ |
| stbkp01 | clint *(or the user provided in your lab)* |

---

## 📌 Step 1: Login

```bash
ssh clint@stbkp01
sudo su -
```

---

## 📦 Step 2: Install iptables

Check first:

```bash
rpm -q iptables iptables-services
```

If not installed:

```bash
yum install -y iptables iptables-services
```

---

## ▶️ Step 3: Enable and Start iptables

```bash
systemctl enable iptables
systemctl start iptables
```

Verify:

```bash
systemctl status iptables
```

---

## 🧹 Step 4: Flush Existing Rules (Optional)

```bash
iptables -F
```

---

## 🔓 Step 5: Allow Nginx Port (8096)

```bash
iptables -A INPUT -p tcp --dport 8096 -j ACCEPT
```

---

## 🚫 Step 6: Block Apache Port (3002)

```bash
iptables -A INPUT -p tcp --dport 3002 -j DROP
```

> **Note:** Use `DROP` unless the lab explicitly asks for `REJECT`.

---

## 💾 Step 7: Save Rules Permanently

```bash
service iptables save
```

or on some systems:

```bash
iptables-save > /etc/sysconfig/iptables
```

---

## 🔄 Step 8: Restart iptables

```bash
systemctl restart iptables
```

---

## ✅ Step 9: Verify Rules

```bash
iptables -L -n
```

Expected:

```text
ACCEPT tcp -- 0.0.0.0/0 0.0.0.0/0 tcp dpt:8096

DROP tcp -- 0.0.0.0/0 0.0.0.0/0 tcp dpt:3002
```

---

## 🔍 Validation Commands

Check iptables service:

```bash
systemctl status iptables
```

View rules:

```bash
iptables -L -n --line-numbers
```

Verify listening ports:

```bash
ss -tlnp | grep -E "3002|8096"
```

Expected:

```text
Apache → 3002
Nginx  → 8096
```

---

## 🛠️ Troubleshooting

Check if iptables package is installed:

```bash
rpm -q iptables iptables-services
```

Check service status:

```bash
systemctl status iptables
```

List current rules:

```bash
iptables -L -n -v
```

Show saved configuration:

```bash
cat /etc/sysconfig/iptables
```

---

## 🧠 Key Learnings

* Install and manage **iptables**.
* Configure port-based firewall rules.
* Difference between **ACCEPT** and **DROP** actions.
* Save firewall rules so they persist after reboot.
* Verify firewall configuration using `iptables -L`.

---

## 🎤 Interview Questions

### ❓ What is iptables?

`iptables` is a Linux firewall utility used to filter network traffic based on rules.

---

### ❓ Difference between DROP and REJECT?

* **DROP:** Silently discards the packet; the client receives no response.
* **REJECT:** Rejects the packet and sends an error back to the client.

---

### ❓ How do you make iptables rules persistent?

On RHEL/CentOS systems:

```bash
service iptables save
```

or

```bash
iptables-save > /etc/sysconfig/iptables
```

---

### ❓ How do you list all firewall rules?

```bash
iptables -L -n -v
```

---

## 🎉 Task Status

* ✅ Installed `iptables`
* ✅ Allowed **Nginx (8096)**
* ✅ Blocked **Apache (3002)**
* ✅ Saved rules permanently
* ✅ Firewall configuration completed successfully 🚀
