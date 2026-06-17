# 🚀 Linux Administration - Task 04 | File Manipulation using `grep` and `sed`

## 📌 Objective

On **Nautilus App Server 1**, modify the file `/home/BSD.txt` according to the following requirements:

### ✅ Task Requirements

1. **Delete all lines containing the word `copyright`**

   * Case-sensitive
   * Save output to:

     ```bash
     /home/BSD_DELETE.txt
     ```

2. **Replace all occurrences of the word `from` with `for`**

   * Replace only the exact word `from`
   * Do NOT replace words like:

     * `fromage`
     * `transform`
     * `from123`
   * Save output to:

     ```bash
     /home/BSD_REPLACE.txt
     ```

---

# 🖥️ Step 1: Login to App Server 1

```bash
ssh tony@stapp01
```

---

# 🔍 Step 2: Check the Original File

```bash
cat /home/BSD.txt
```

or

```bash
less /home/BSD.txt
```

---

# 🗑️ Task A - Delete Lines Containing `copyright`

Use:

```bash
grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt
```

### Explanation

| Option | Meaning                               |
| ------ | ------------------------------------- |
| `grep` | Search text                           |
| `-v`   | Invert match (exclude matching lines) |
| `>`    | Redirect output                       |

---

## Verify

```bash
grep 'copyright' /home/BSD_DELETE.txt
```

Expected:

```text
No output
```

or

```bash
cat /home/BSD_DELETE.txt
```

---

# 🔄 Task B - Replace `from` with `for`

⚠️ The question specifically says:

> Do not alter words containing the string itself.

Therefore, use **word boundaries**.

```bash
sed 's/\<from\>/for/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```

---

## Explanation

```text
s      → substitute
\<from\> → exact word "from"
for    → replacement
g      → replace all occurrences in a line
```

---

### Example

Original:

```text
Data is copied from server.
transform operation.
```

After replacement:

```text
Data is copied for server.
transform operation.
```

Notice:

✅ `from` → changed

❌ `transform` → unchanged

---

# 🔍 Verify Replacement

Search remaining word:

```bash
grep -w from /home/BSD_REPLACE.txt
```

Expected:

```text
No output
```

---

# ⚡ Final Commands (Exam Shortcut)

```bash
grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt

sed 's/\<from\>/for/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```

These two commands are enough to pass the KodeKloud task. ✅

---

# 📂 Validate Files

Check both files:

```bash
ls -l /home/BSD_*
```

Expected:

```text
BSD_DELETE.txt
BSD_REPLACE.txt
```

---

# 🧪 Validate Task A

```bash
grep copyright /home/BSD_DELETE.txt
```

Expected:

```text
No output
```

---

# 🧪 Validate Task B

```bash
grep -w from /home/BSD_REPLACE.txt
```

Expected:

```text
No output
```

---

# 🎯 Key Takeaways

✅ `grep -v`

Excludes matching lines.

Example:

```bash
grep -v error file.txt
```

Shows all lines except those containing `error`.

---

✅ `sed`

Stream editor used for:

* Replace text
* Delete lines
* Insert text
* Edit files non-interactively

---

✅ Word Boundary

```bash
\<word\>
```

or

```bash
\bword\b
```

Ensures only exact words are matched.

---

# 📚 Common grep Commands

| Command             | Meaning           |
| ------------------- | ----------------- |
| `grep word file`    | Find word         |
| `grep -i word file` | Ignore case       |
| `grep -v word file` | Exclude word      |
| `grep -w word file` | Match exact word  |
| `grep -n word file` | Show line numbers |

---

# 📚 Common sed Commands

### Replace first occurrence

```bash
sed 's/old/new/'
```

---

### Replace all occurrences

```bash
sed 's/old/new/g'
```

---

### Delete lines

```bash
sed '/error/d'
```

---

### Edit file directly

```bash
sed -i 's/old/new/g' file.txt
```

---

# 🎤 Interview Questions

## Q1. What does grep -v do?

**Answer:**

`grep -v` prints all lines that do **not** match the given pattern.

Example:

```bash
grep -v error app.log
```

Displays all lines except those containing `error`.

---

## Q2. Difference between grep and sed?

| grep                    | sed                 |
| ----------------------- | ------------------- |
| Search text             | Edit text           |
| Filter lines            | Modify lines        |
| Output matching content | Replace/Delete/Edit |

---

## Q3. What does `-w` mean in grep?

```bash
grep -w from file.txt
```

Matches only the exact word:

✅ from

❌ transform

❌ fromage

---

## Q4. Explain this command

```bash
grep -v 'copyright' BSD.txt > BSD_DELETE.txt
```

**Answer:**

* Search BSD.txt
* Exclude lines containing `copyright`
* Save output to BSD_DELETE.txt

---

## Q5. Explain this sed command

```bash
sed 's/\<from\>/for/g'
```

**Answer:**

* `s` → substitute
* `\<from\>` → exact word match
* `for` → replacement
* `g` → replace all occurrences

---

## Q6. What does `>` do in Linux?

```bash
command > file
```

Redirects command output to a file.

If the file exists, it will be overwritten.

---

## Q7. Difference between `>` and `>>`?

| Operator | Meaning        |
| -------- | -------------- |
| `>`      | Overwrite file |
| `>>`     | Append to file |

Example:

```bash
echo hello > a.txt
echo world >> a.txt
```

Output:

```text
hello
world
```

---

# 🌟 Task Status

✅ Removed lines containing `copyright`
✅ Created `BSD_DELETE.txt`
✅ Replaced exact word `from` with `for`
✅ Created `BSD_REPLACE.txt`
✅ File Manipulation Completed Successfully 🚀

---

## 📂 GitHub Repository Structure

```text
Linux/
└── Task-04-File-Manipulation/
    ├── README.md
    └── screenshots/
        ├── original-file.png
        ├── grep-delete.png
        ├── sed-replace.png
        └── validation.png
```

### ISSUES
([tony@stapp01 ~]$ grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt -bash: /home/BSD_DELETE.txt: Permission denied [tony@stapp01 ~]$ sudo grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt -bash: /home/BSD_DELETE.txt: Permission denied [tony@stapp01 ~]$)

This is a very common Linux interview and real-world scenario.

The problem is **not with `grep`**. The problem is with the **shell redirection (`>`)**.

When you run:

```bash
sudo grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt
```

only the `grep` command runs with `sudo`.

The `>` redirection is executed by your current shell (`tony`), and **tony does not have permission to write to `/home/BSD_DELETE.txt`**.

---

## Step 1: Check Ownership and Permissions

Run:

```bash
ls -l /home/BSD.txt
ls -ld /home
```

Also check:

```bash
touch /home/testfile
```

If you get:

```text
Permission denied
```

then the `/home` directory is not writable by `tony`.

---

## Step 2: Use sudo with tee

This is the safest solution:

```bash
grep -v 'copyright' /home/BSD.txt | sudo tee /home/BSD_DELETE.txt > /dev/null
```

For the second file:

```bash
sed 's/\<from\>/for/g' /home/BSD.txt | sudo tee /home/BSD_REPLACE.txt > /dev/null
```

---

## Step 3: Alternative - Use sudo bash

```bash
sudo bash -c "grep -v 'copyright' /home/BSD.txt > /home/BSD_DELETE.txt"
```

and

```bash
sudo bash -c "sed 's/\<from\>/for/g' /home/BSD.txt > /home/BSD_REPLACE.txt"
```

---

## Step 4: Verify

```bash
ls -l /home/BSD_*
```

Expected:

```text
/home/BSD_DELETE.txt
/home/BSD_REPLACE.txt
```

---

### Why `sudo grep ... > file` fails?

Interview Question ⭐

**Q:** Why does this fail?

```bash
sudo grep text file > output.txt
```

**Answer:**

Because:

* `sudo` applies only to `grep`
* `>` is handled by the current shell
* The shell does not have permission to create/write the output file

**Correct approaches:**

```bash
grep text file | sudo tee output.txt
```

or

```bash
sudo bash -c "grep text file > output.txt"
```

---

Please run:

```bash
ls -ld /home
ls -l /home/BSD.txt
```

and share the output if the problem persists.

--- 
### what is the purpose of /dev/null
`/dev/null` is a **special device file in Linux** that acts like a **black hole** for data.

Anything you send to `/dev/null` is **discarded permanently**.

---

# 📌 Basic Idea

```bash
echo "hello" > /dev/null
```

The output:

```text
hello
```

is **not displayed** and **not stored anywhere**.

It simply disappears.

---

# Why did we use it here?

You ran:

```bash
grep -v 'copyright' /home/BSD.txt | sudo tee /home/BSD_DELETE.txt > /dev/null
```

Let's break it down:

### Without `/dev/null`

```bash
grep -v 'copyright' /home/BSD.txt | sudo tee /home/BSD_DELETE.txt
```

`tee` does two things:

1. Writes to `/home/BSD_DELETE.txt`
2. Prints the same content on the screen

So you'll see the entire file content on your terminal.

---

### With `/dev/null`

```bash
grep -v 'copyright' /home/BSD.txt | sudo tee /home/BSD_DELETE.txt > /dev/null
```

Now:

* `tee` writes to the file ✅
* Terminal output goes to `/dev/null` ❌ (discarded)

Result:

```text
Nothing printed on screen
File created successfully
```

---

# Common Uses of `/dev/null`

### 1. Hide standard output

```bash
ls > /dev/null
```

No output shown.

---

### 2. Hide errors

```bash
ls xyz 2>/dev/null
```

Normally:

```text
ls: cannot access xyz: No such file or directory
```

With `2>/dev/null`:

```text
No error shown
```

---

### 3. Hide both output and errors

```bash
command > /dev/null 2>&1
```

Example:

```bash
yum install nginx > /dev/null 2>&1
```

This hides:

* Standard Output (stdout)
* Standard Error (stderr)

---

# Understanding File Descriptors

Linux uses:

| Number | Stream                 |
| ------ | ---------------------- |
| 0      | stdin (keyboard input) |
| 1      | stdout (normal output) |
| 2      | stderr (error output)  |

Example:

```bash
command > /dev/null
```

is the same as:

```bash
command 1> /dev/null
```

---

### Hide only errors

```bash
command 2> /dev/null
```

---

### Hide everything

```bash
command > /dev/null 2>&1
```

Meaning:

1. Send stdout to `/dev/null`
2. Send stderr to wherever stdout is going (`/dev/null`)

---

# Real DevOps Examples

### Health check without displaying output

```bash
curl -s http://localhost:8080 > /dev/null
```

---

### Cron jobs

```bash
*/5 * * * * /opt/backup.sh > /dev/null 2>&1
```

This prevents cron from sending emails containing script output.

---

### Check service quietly

```bash
systemctl status nginx > /dev/null 2>&1
```

---

# Interview Question ⭐

### Q: What is `/dev/null`?

**Answer:**

`/dev/null` is a special virtual device file that discards all data written to it and returns EOF (End Of File) when read. It is commonly used to suppress command output or error messages.

---

# Quick Memory Trick

```text
/dev/null = Linux Recycle Bin ❌

Actually,

/dev/null = Linux BLACK HOLE 🕳️

Anything sent there disappears forever.
```

This is one of the most frequently asked Linux and DevOps interview topics, especially when discussing **shell scripting, cron jobs, CI/CD pipelines, and log management**.

