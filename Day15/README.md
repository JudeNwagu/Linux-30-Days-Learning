# Day 15 – File Permissions and Ownership in Linux

## Objective

Today’s focus was understanding how Linux controls access to files and directories using permissions and ownership.

Linux file permissions form the foundation of the system’s security model. They define who can read, write, or execute files and directories, ensuring that only authorized users or processes can access sensitive data.

The goal was to clearly understand how Linux:

* controls access using read, write, and execute permissions
* assigns ownership to users and groups
* manages access through permission groups
* protects files in a multi-user environment

This is critical when working with shared systems, servers, and production environments where access control directly impacts security.

---

## What I Learned

### 1) The Three Basic Permissions

<img width="719" height="358" alt="Screenshot 2026-04-17 130443" src="https://github.com/user-attachments/assets/32d2a0f5-5893-4d79-aa2a-d314d322e935" />
<br><br>

Every file or directory has three types of permissions:

| Letter | Definition                                        |
| ------ | ------------------------------------------------- |
| r      | Read – view file contents or list directory files |
| w      | Write – modify file contents or add/delete files  |
| x      | Execute – run a file or access a directory        |

---

### 2) Ownership and Permission Groups

<img width="722" height="357" alt="Screenshot 2026-04-17 130902" src="https://github.com/user-attachments/assets/b20d8d35-b53a-49c4-96a7-72c2c35f62f7" />
<br><br>

Permissions are assigned to three categories of users:

```
rwx     rwx     rwx
user    group   others
```

| Reference | Class  | Description                        |
| --------- | ------ | ---------------------------------- |
| u         | user   | Applies to the file owner          |
| g         | group  | Applies to users in the group      |
| o         | others | Applies to all other users         |
| a         | all    | Applies to user, group, and others |

**Permission Operators**

| Operator | Meaning              |
| -------- | -------------------- |
| +        | Add permission       |
| -        | Remove permission    |
| =        | Set exact permission |

---

### 3) Understanding File Permission Output

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -l fruits.txt
-rw-r--r-- 1 judoski judoski 122 Apr 11 08:56 fruits.txt
```

Breakdown:

1. `-` → file (`d` would mean directory)
2. `rw-r--r--` → permission structure
3. `judoski` → file owner
4. `judoski` → group owner
5. `122` → file size
6. `Apr 11 08:56` → last modified

---

### 4) Working with `chmod` (Permissions)

Basic commands:

```bash
chmod +rwx filename
chmod -rwx directoryname
chmod +x filename
chmod -wx filename
```

#### Example (Symbolic Mode)

```bash
chmod o+x fruits.txt
judoski@DESKTOP-6FUB9PD:~$ chmod o+x fruits.txt

-rwxr--r-x 1 judoski judoski     122 Apr 11 08:56 fruits.txt
```

Removing all permissions:

```bash
chmod ugo-rwx fruits.txt
judoski@DESKTOP-6FUB9PD:~$ chmod ugo-rwx fruits.txt

---------- 1 judoski judoski     122 Apr 11 08:56 fruits.txt
```

Restoring permissions:

```bash
judoski@DESKTOP-6FUB9PD:~$ chmod 766 fruits.t
-rwxrw-rw- 1 judoski judoski     122 Apr 11 08:56 fruits.txt
```

---

### 5) Numeric (Octal) Permissions

Example:

```bash
chmod 745 fruits.txt
```

Result:

```
-rwxr--r-x
```

| Category | Value | Meaning |
| -------- | ----- | ------- |
| Owner    | 7     | rwx     |
| Group    | 4     | r--     |
| Others   | 5     | r-x     |

#### Equivalent Numeric Table

| User Type | Permissions | Binary | Value |
| --------- | ----------- | ------ | ----- |
| Owner     | rwx         | 111    | 7     |
| Group     | rw-         | 110    | 6     |
| Others    | rw-         | 110    | 6     |

---

### 6) Common Permission Modes

| Mode | Owner | Group | Others | Use Case           |
| ---- | ----- | ----- | ------ | ------------------ |
| 700  | rwx   | ---   | ---    | Private script     |
| 711  | rwx   | --x   | --x    | Execute only       |
| 744  | rwx   | r--   | r--    | Personal scripts   |
| 750  | rwx   | r-x   | ---    | Team restricted    |
| 754  | rwx   | r-x   | r--    | Mixed access       |
| 755  | rwx   | r-x   | r-x    | Common default     |
| 775  | rwx   | rwx   | r-x    | Team collaboration |

---

### 7) Reverting Permission Changes

To restore permissions:

```bash
chmod 644 filename
```

* Owner → read + write
* Group → read
* Others → read

---

### 8) Special Permissions

```bash
chmod u+s program
chmod g+s directoryname
chmod +t directoryname
```

* **setuid** → run as file owner
* **setgid** → inherit group
* **sticky bit** → restrict deletion to owner

---

### 9) Working with `chown` (Ownership)

Syntax:

```bash
chown [options] new_owner[:new_group] file
```

#### Change Owner

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown judoski fruits.txt
```

#### Change Group

```bash
judoski@DESKTOP-6FUB9PD:~$ touch data_pipeline.py
judoski@DESKTOP-6FUB9PD:~$ sudo chown :zenith_user data_pipeline.py
```

Verify:

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -l data_pipeline.py
-rw-r--r-- 1 judoski zenith_user 0 Apr 17 16:47 data_pipeline.py
```

#### Change Owner and Group Together

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown judoski:zenith_user fruits.txt
```

---

### 10) `chown` Options in Practice

#### `-c` (only show changes)

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown -c data_engine:zenith_user fruits.txt
changed ownership of 'fruits.txt' from judoski:zenith_user to data_engine:zenith_user
```

#### `-v` (verbose output)

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown -v judoski:zenith_user data_pipeline.py
ownership of 'data_pipeline.py' retained as judoski:zenith_us

judoski@DESKTOP-6FUB9PD:~$ sudo chown -v judoski:docker data_pipeline.py
changed ownership of 'data_pipeline.py' from judoski:zenith_user to judoski:docker
```

#### Silent when no change

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown -c judoski:docker data_pipeline.py
```

#### Switching back

```bash
judoski@DESKTOP-6FUB9PD:~$ sudo chown -c judoski:zenith_user data_pipeline.py
changed ownership of 'data_pipeline.py' from judoski:docker to judoski:zenith_user
```

#### `-f` (force/suppress errors)

```bash
chown: invalid user: ‘ghost_user’

judoski@DESKTOP-6FUB9PD:~$ chown data_engine data_pipeline.py
chown: changing ownership of 'data_pipeline.py': Operation not permitted

judoski@DESKTOP-6FUB9PD:~$ sudo chown -f data_engine data_pipeline.py
```

---

## What I Built / Practiced

Today felt very practical. I worked on:

* inspecting file permissions using `ls -l`
* modifying permissions with `chmod` (symbolic and numeric)
* testing multiple permission levels (644, 755, 775)
* removing and restoring access
* assigning group-based access
* changing file ownership using `chown`
* verifying ownership changes with real terminal output

---

## Challenges Faced

### 1) Ghost User Error

```bash
chown: invalid user: ‘master’
```

Linux validates users against `/etc/passwd`. If the user doesn’t exist, the command fails.

---

### 2) Understanding `-f` Flag

* suppresses permission errors
* does NOT hide invalid user errors

---

### 3) Updating User and Group Together

```bash
sudo chown judoski:zenith_user script.py
```

This single command is cleaner and safer than running multiple commands.

---

## Key Takeaways

* File permissions are the backbone of Linux security
* Every file has both permissions and ownership
* Groups simplify access control in teams
* Numeric permissions become easier with practice
* Ownership must match real system users
* `sudo` is required for most ownership changes
* Choosing between `-v` and `-c` depends on your workflow (manual vs automation)

---

## Resources

* DEC Learning Materials
* GeeksforGeeks
* Linux terminal practice
* Personal test files

---

## Output

By the end of today, I can:

* confidently read and interpret file permissions
* modify access using `chmod`
* manage ownership using `chown`
* create secure file access structures

This feels like moving from just using Linux… to actually controlling it.

<img width="1362" height="716" alt="Screenshot 2026-04-17 140817" src="https://github.com/user-attachments/assets/e86b2c7a-1333-41de-a07f-d2d2d1013a43" />
<br><br>


<img width="1362" height="716" alt="Screenshot 2026-04-17 140817" src="https://github.com/user-attachments/assets/70a715b9-0517-4d01-adcb-5cd719a2b391" />
<br><br>


<img width="1366" height="714" alt="Screenshot 2026-04-17 175939" src="https://github.com/user-attachments/assets/731ab37a-6dce-43a9-be2e-5428a203d703" />
<br><br>


<img width="1366" height="715" alt="Screenshot 2026-04-17 180032" src="https://github.com/user-attachments/assets/4a3096e3-a5b8-4b2a-ac07-e75424941671" />
<br><br>


<img width="1363" height="717" alt="Screenshot 2026-04-17 180116" src="https://github.com/user-attachments/assets/8cc1fe6a-733e-46cd-98d1-1dd6ada03b83" />
<br><br>


<img width="1364" height="716" alt="Screenshot 2026-04-17 180133" src="https://github.com/user-attachments/assets/8b25f090-c801-42c3-a9bf-18b6b09a9a0b" />






