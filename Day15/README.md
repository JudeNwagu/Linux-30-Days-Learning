
# Day 15 – File Permissions and Ownership in Linux

## Objective

Today’s focus was on understanding how Linux controls access to files and directories using permissions and ownership.

Linux is a multi-user system, which means different users can interact with the same files. Without proper control, this can easily lead to security issues or accidental changes. The goal for today was to understand how Linux:

* controls who can read, write, or execute files
* assigns ownership to users and groups
* manages access using permission rules
* protects sensitive files from unauthorized access

This is especially important when working with:

* shared systems
* production servers
* data pipelines
* team-based environments

Because at the core of Linux security is a simple idea: **who can do what on a file**.

---

## What I Learned

### 1) The Three Basic Permissions

Every file and directory in Linux has three core permissions:

| Permission    | Meaning                                             |
| ------------- | --------------------------------------------------- |
| `r` (read)    | View file contents or list directory files          |
| `w` (write)   | Modify a file or add/delete files in a directory    |
| `x` (execute) | Run a file as a script/program or enter a directory |

These three permissions are the building blocks of access control in Linux.

---

### 2) User Categories (Who Permissions Apply To)

Permissions are not just about actions—they are also about **who those actions apply to**.

Linux divides access into three groups:

```
rwx     rwx     rwx
user    group   others
```

| Symbol | Applies To | Description               |
| ------ | ---------- | ------------------------- |
| `u`    | User       | The owner of the file     |
| `g`    | Group      | Users in the file’s group |
| `o`    | Others     | Everyone else             |
| `a`    | All        | User + Group + Others     |

This structure makes it easy to control access at scale instead of managing users one by one.

---

### 3) Understanding File Permission Output

Using:

```bash
ls -l fruits.txt
```

Output:

```
-rw-r--r-- 1 judoski judoski 122 Apr 11 08:56 fruits.txt
```

Breakdown:

* `-` → file (`d` would mean directory)
* `rw-r--r--` → permissions
* `judoski` → file owner
* `judoski` → group owner
* `122` → file size
* `Apr 11 08:56` → last modified

This single line shows both **permission and ownership in one view**.

---

### 4) Working with chmod (Changing Permissions)

The `chmod` command is used to control access to files.

#### Basic Examples:

```bash
chmod +x file.txt      # make executable
chmod -wx file.txt     # remove write and execute
chmod ugo-rwx file.txt # remove all permissions
```

---

### 5) Numeric (Octal) Permissions

Instead of symbols, permissions can be set using numbers:

| Number | Permission |
| ------ | ---------- |
| 7      | rwx        |
| 6      | rw-        |
| 5      | r-x        |
| 4      | r--        |

Example:

```bash
chmod 745 fruits.txt
```

Breakdown:

| Category | Value | Meaning              |
| -------- | ----- | -------------------- |
| Owner    | 7     | read, write, execute |
| Group    | 4     | read only            |
| Others   | 5     | read + execute       |

Result:

```
-rwxr--r-x
```

---

### 6) Common Permission Modes

| Mode | Owner | Group | Others | Use Case            |
| ---- | ----- | ----- | ------ | ------------------- |
| 700  | rwx   | ---   | ---    | Private files       |
| 744  | rwx   | r--   | r--    | Personal scripts    |
| 755  | rwx   | r-x   | r-x    | Executable programs |
| 775  | rwx   | rwx   | r-x    | Team collaboration  |

---

### 7) Symbolic Permission Changes

Symbolic mode allows targeted changes:

```bash
chmod o+x fruits.txt
```

This adds execute permission for others.

You can also combine actions:

```bash
chmod ugo-rwx fruits.txt
```

This removes all access.

---

### 8) Special Permissions

Linux also supports advanced permissions:

| Permission | Command     | Purpose                     |
| ---------- | ----------- | --------------------------- |
| setuid     | `chmod u+s` | Run file as owner           |
| setgid     | `chmod g+s` | Inherit group permissions   |
| sticky bit | `chmod +t`  | Only owner can delete files |

These are often used in shared or secure environments.

---

### 9) Working with chown (Changing Ownership)

The `chown` command controls **who owns a file**.

#### Syntax:

```bash
chown user:group file
```

#### Examples:

Change owner:

```bash
sudo chown judoski fruits.txt
```

Change group:

```bash
sudo chown :zenith_user data_pipeline.py
```

Change both:

```bash
sudo chown judoski:zenith_user fruits.txt
```

---

### 10) Useful chown Options

| Option | Purpose                      |
| ------ | ---------------------------- |
| `-c`   | Show only when changes occur |
| `-v`   | Show all changes (verbose)   |
| `-f`   | Suppress permission errors   |

Example:

```bash
sudo chown -v judoski:docker data_pipeline.py
```

---

## What I Built / Practiced

Today felt very practical. I worked on:

* checking file permissions using `ls -l`
* modifying permissions with both symbolic and numeric methods
* testing different permission levels (644, 755, 775)
* removing and restoring access
* changing file ownership between users and groups
* creating shared access using group ownership
* experimenting with real scenarios like project files

This felt like working on a real system where access control matters.

---

## Challenges Faced

One of the main challenges was understanding **when to use numeric vs symbolic permissions**.

At first, numbers like `755` or `644` felt abstract, but after breaking them down into `rwx`, they became easier to understand.

Another challenge was ownership errors:

* trying to assign a file to a user that doesn’t exist
* forgetting to use `sudo` when required

This made it clear that Linux validates everything against system records.

---

## Key Takeaways

A few important lessons stood out today:

* File permissions are the backbone of Linux security
* Every file has both **permissions and ownership**
* Groups make access management easier in teams
* Numeric permissions are faster once you understand them
* Ownership must match real system users
* `sudo` is required for most ownership changes
* Small mistakes in permissions can lead to big security risks

This knowledge is directly useful for:

* system administration
* DevOps workflows
* cloud environments
* data engineering systems

---

## Resources

* DEC Resources
*Geeksforgeeks
* Practice files created during learning
* Terminal experimentation

---

## Output

By the end of today, I can:

* confidently read and interpret file permissions
* assign correct access levels using `chmod`
* manage file ownership using `chown`
* create secure and controlled file environments

This feels like a major step forward, because understanding permissions is what separates basic Linux usage from real system-level control.


