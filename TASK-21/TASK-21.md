# ✅ Task-21: Encrypt and Decrypt Files Using GPG

## 📌 Problem Statement

On the Storage Server:

* Encrypt `/home/encrypt_me.txt` to `/home/encrypted_me.asc`
* Decrypt `/home/decrypt_me.asc` to `/home/decrypted_me.txt`
* Use user ID:

```text
kodekloud@kodekloud.com
```

* Passphrase:

```text
kodekloud
```

---

## Step 1: Verify Available Files

```bash
ls -la /home
```

Expected:

```text
decrypt_me.asc
encrypt_me.txt
private_key.asc
public_key.asc
```

---

## Step 2: Import GPG Keys

### Import Public Key

```bash
gpg --import /home/public_key.asc
```

### Import Private Key

```bash
gpg --import /home/private_key.asc
```

---

## Step 3: Verify Imported Keys

```bash
gpg --list-keys

gpg --list-secret-keys
```

Expected:

```text
pub   rsa2048
uid   kodekloud <kodekloud@kodekloud.com>
sub   rsa2048
```

---

## Step 4: Encrypt the File

Initially:

```bash
gpg --armor \
--output /home/encrypted_me.asc \
--recipient "kodekloud@kodekloud.com" \
--encrypt /home/encrypt_me.txt
```

Received:

```text
Permission denied
```

Reason:

* `natasha` did not have permission to create files directly under `/home`.

---

## Step 5: Import Keys for Root User

```bash
sudo gpg --import /home/public_key.asc

sudo gpg --import /home/private_key.asc
```

Verify:

```bash
sudo gpg --list-keys
```

---

## Step 6: Encrypt File Successfully

```bash
sudo gpg --yes \
--trust-model always \
--armor \
-r kodekloud@kodekloud.com \
-o /home/encrypted_me.asc \
-e /home/encrypt_me.txt
```

---

## Step 7: Decrypt File

```bash
sudo gpg --batch --yes \
--passphrase kodekloud \
--output /home/decrypted_me.txt \
--decrypt /home/decrypt_me.asc
```

Output:

```text
gpg: AES.CFB encrypted data
gpg: encrypted with 1 passphrase
```

---

## Step 8: Verify Output Files

```bash
ls -l /home/encrypted_me.asc

ls -l /home/decrypted_me.txt
```

Expected:

```text
-rw-r--r-- root root ... encrypted_me.asc
-rw-r--r-- root root ... decrypted_me.txt
```

---

## 🔍 Troubleshooting Commands Used

### Check Imported Keys

```bash
gpg --list-keys

gpg --list-secret-keys
```

---

### Check Root Keyring

```bash
sudo gpg --list-keys

sudo gpg --list-secret-keys
```

---

### Check File Permissions

```bash
ls -ld /home

ls -l /home
```

---

## 🧠 Key Learnings

* GPG Public Key Encryption
* GPG Private Key Decryption
* ASCII Armored Output (`.asc`)
* GPG Key Import
* Root vs User GPG Keyrings
* File Permission Troubleshooting

---

## 🎤 Interview Questions

### Q1. What is GPG?

GPG (GNU Privacy Guard) is an implementation of OpenPGP used for:

* Encryption
* Decryption
* Digital Signatures
* Key Management

---

### Q2. Difference between Public and Private Keys?

| Public Key          | Private Key         |
| ------------------- | ------------------- |
| Used for Encryption | Used for Decryption |
| Shared with others  | Kept Secret         |
| Encrypts data       | Decrypts data       |

---

### Q3. List Imported Keys

```bash
gpg --list-keys

gpg --list-secret-keys
```

---

### Q4. Encrypt a File

```bash
gpg --armor \
-r user@example.com \
-o encrypted.asc \
-e file.txt
```

---

### Q5. Decrypt a File

```bash
gpg --decrypt encrypted.asc
```

---

✅ **Task Status:** Completed Successfully 🚀
