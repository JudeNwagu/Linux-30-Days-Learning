````markdown
# Day 06 - Calendar, Command Location, and Disk Usage in Linux

## Objective
The goal for today was to move deeper into **Linux system visibility and diagnostics** by learning commands that help with:
- date and calendar awareness
- locating system binaries and manuals
- distinguishing between system tools and personal files
- checking disk usage and file system health
- understanding WSL storage behavior

Today’s focus shifted from file creation into **system inspection**, which is a major skill for Data Engineering environments, Linux servers, and storage-heavy workflows.

---

## What I Learned

I continued the Linux journey by exploring commands that help me understand **where tools live, how much storage I have, and how Linux represents time and file systems**.

---

### 22. `cal`
The `cal` command is used to display a **calendar directly in the terminal**.

This is useful for:
- quick date checks
- scheduling scripts
- cron job planning
- checking historical months
- year overview without opening GUI apps

#### Current Month
```bash
judoski@DESKTOP-6FUB9PD:~$ cal
     April 2026
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30
````

#### Specific Month and Year

```bash
judoski@DESKTOP-6FUB9PD:~$ cal 06 2026
     June 2026
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30
```

#### Other Useful Formats

```bash
cal -y
cal -3
cal -jy 2025
```

This command is simple, but very useful for **terminal-based scheduling awareness**.

---

### 23. `whereis`

The `whereis` command helps locate:

* binary executables
* source files
* manual pages

It searches predefined Linux system paths, so it is much faster than `find`.

#### Example

```bash
judoski@DESKTOP-6FUB9PD:~$ whereis python3
python3: /usr/bin/python3 /usr/lib/python3 /etc/python3 /usr/share/python3 /usr/share/man/man1/python3.1.gz
```

This showed me:

* where Python runs from
* where its libraries are stored
* where its documentation lives

That is extremely useful when setting up:

* Python environments
* Airflow
* dbt
* ETL scripts
* Docker containers

---

### `which` vs `whereis`

I also compared it with `which`.

```bash
judoski@DESKTOP-6FUB9PD:~$ which python3
/usr/bin/python3
```

The lesson:

* `whereis` = full biography
* `which` = exact executable path

That means:

* use `which` when running scripts
* use `whereis` when understanding installations

---

### `locate` for Personal Files

To compare system search vs personal file search, I used:

```bash
judoski@DESKTOP-6FUB9PD:~$ locate stranger_things
/home/judoski/fruits/stranger_things.txt
/home/judoski/netflix/tv_shows/sci_fi/stranger_things.txt
```

This taught me an important distinction:

> `whereis` is for system tools
> `locate` is for personal files and indexed file paths

That difference is very important.

---

### Useful `whereis` Options

| Option | Meaning                     |
| ------ | --------------------------- |
| `-b`   | Search binaries only        |
| `-m`   | Search manual pages only    |
| `-s`   | Search source files only    |
| `-u`   | Show unusual entries        |
| `-B`   | Custom binary path          |
| `-M`   | Custom manual path          |
| `-S`   | Custom source path          |
| `-f`   | End custom path declaration |

#### Examples

```bash
whereis -b grep
whereis -m ls
whereis -s bash
```

These options make `whereis` much more flexible.

---

### 24. `df`

The `df` command displays **disk usage of mounted file systems**.

This is one of the most practical Linux commands for:

* disk monitoring
* storage planning
* WSL diagnostics
* checking available space for datasets
* monitoring logs and PostgreSQL growth

#### Standard Output

```bash
judoski@DESKTOP-6FUB9PD:~$ df
Filesystem      1K-blocks      Used Available Use% Mounted on
/dev/sdd       1055762868   3960552 998098844   1% /
```

This confirmed that my Linux root drive is still almost empty.

---

### Check Specific Directory

```bash
judoski@DESKTOP-6FUB9PD:~$ df /home
Filesystem      1K-blocks    Used Available Use% Mounted on
/dev/sdd       1055762868 3960552 998098844   1% /
```

---

### Check a File’s File System

```bash
judoski@DESKTOP-6FUB9PD:~$ df fruits.txt
Filesystem      1K-blocks    Used Available Use% Mounted on
/dev/sdd       1055762868 3960552 998098844   1% /
```

This helps reveal which mounted partition a file belongs to.

---

### Human Readable Output

This was the most useful version:

```bash
judoski@DESKTOP-6FUB9PD:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
drivers         238G  215G   24G  91% /usr/lib/wsl/drivers
/dev/sdd       1007G  3.8G  952G   1% /
```

This instantly made the storage clearer.

Key insight:

* Linux storage is healthy
* Windows mounted drive is already **91% full**
* Linux side is better for storing larger datasets

This is highly relevant for Data Engineering work.

---

### Useful `df` Options

| Option    | Meaning                  |
| --------- | ------------------------ |
| `-a`      | Show all file systems    |
| `-h`      | Human readable           |
| `-i`      | Show inode usage         |
| `--total` | Grand total              |
| `-t TYPE` | Show specific type       |
| `-x TYPE` | Exclude type             |
| `-l`      | Show local file systems  |
| `-T`      | Show file system type    |
| `--sync`  | Refresh before reporting |

#### Useful Examples

```bash
df -h
df -i
df -T
df --total
```

---

## What I Built / Practiced

Today’s practice focused on:

* displaying month and year calendars
* checking future months
* locating Python installation files
* comparing `whereis`, `which`, and `locate`
* checking root disk storage
* checking `/home` storage
* checking a file’s mounted partition
* viewing human-readable disk sizes
* understanding Windows vs Linux storage inside WSL

This is directly useful for:

* dataset storage planning
* Linux server monitoring
* Docker volume checks
* Airflow logs management
* PostgreSQL disk growth tracking

---

## Challenges Faced

Today’s learning also had important logic lessons.

| Challenge                                | Lesson Learned                                            |
| ---------------------------------------- | --------------------------------------------------------- |
| Tried using `whereis` for personal files | It only works for system tools                            |
| Confused `which` and `whereis`           | One gives path, one gives full installation info          |
| Large 1K block numbers in `df`           | `-h` makes storage easier to read                         |
| WSL mount confusion                      | Linux and Windows storage appear as separate file systems |

These were very practical system-level lessons.

---

## Key Takeaways

The biggest lessons from today:

* `cal` improves terminal scheduling awareness
* `whereis` is best for installed tools
* `which` reveals exact executables
* `locate` is better for personal files
* `df` is essential for disk diagnostics
* WSL exposes Linux and Windows drives differently
* `df -h` is the most practical version for daily use
* storage awareness is critical in data workflows

The strongest takeaway:

> **system awareness is what transforms Linux from simple file navigation into real infrastructure management.**

---

## Resources

* DEC Linux learning guide
* WSL mounted storage environment
* built-in help pages
* practical local disk inspection

---

## Output

### Commands Practiced

```bash
cal
cal -y
cal -3
cal 06 2026
cal -jy 2025
whereis python3
which python3
locate stranger_things
whereis -b grep
whereis -m ls
whereis -s bash
df
df /home
df fruits.txt
df -h
df -i
df -T
df --total
```

### Key Practical Insight

```text
Windows mounted storage: 91% used
Linux root storage: 1% used
```

This was a major learning day because it introduced **Linux storage awareness, executable discovery, and system-level inspection**, which are all critical for building reliable data engineering environments.

```
```
