# Day 03 - Linux Basic Commands and Terminal Practice

## Objective
The goal for today was to build confidence with **essential Linux terminal commands** used for navigation, file management, system inspection, and everyday command-line operations.

Today moved beyond just understanding the Linux file system into **actively interacting with it using commands**. The focus was on learning how commands work, what common options do, and how small mistakes in syntax can lead to useful lessons.

This is a critical stage in the journey because command-line fluency is the foundation for Linux administration, automation, DevOps workflows, and data engineering tasks.

---

## What I Learned
Before jumping into commands, I first understood **why the command line matters in Linux**.

Linux professionals spend a significant amount of time in the terminal because:
- there is no GUI overhead
- almost every task can be completed faster
- repetitive tasks can be automated with scripts
- remote machines can be managed easily
- graphical apps can even be launched from the terminal
- command-line workflows stay consistent across Linux distributions

That consistency is one of the biggest strengths of Linux.

---

### Core Commands Learned Today
Below is a structured breakdown of the major commands I practiced.

| Command | Purpose | Example |
|---|---|---|
| `ls` | List files and directories | `ls -l` |
| `pwd` | Show current directory | `pwd` |
| `mkdir` | Create directories | `mkdir -p netflix/...` |
| `cd` | Change directory | `cd netflix` |
| `rmdir` | Remove empty directories | `rmdir dir1` |
| `cp` | Copy files/directories | `cp banana.txt ~/futbolclubs/` |
| `mv` | Move or rename files | `mv oranges.csv apples.csv` |
| `rm` | Delete files/directories | `rm apples.csv` |
| `uname` | Show system info | `uname -a` |
| `locate` | Find files quickly | `locate banana.txt` |
| `head` | Show first lines/items | `head -1` |

---

### 1) `ls` — Listing Files
The `ls` command helps display files and folders in the current directory.

My real practice:
```bash
judoski@DESKTOP-6FUB9PD:~$ ls -t fruits
oragnes.csv  watermelon.csv  banana.txt  pineapple.py
```

This sorts files by **most recently modified first**.

A very useful pattern I learned:

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -t fruits | head -1
oragnes.csv
```

This combines:
- `ls -t` → newest files first
- `head -1` → show only the first result

This became today’s first major lesson in **command piping**.

Other useful `ls` options:

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -1
judoski@DESKTOP-6FUB9PD:~$ ls -l
```

---

### 2) `pwd` — Present Working Directory
This shows the absolute path of where I currently am.

```bash
judoski@DESKTOP-6FUB9PD:~$ pwd
/home/Judoski
```

This is one of the easiest ways to avoid getting lost.

---

### 3) `mkdir` — Creating Directories
I practiced nested directory creation with one command.

```bash
judoski@DESKTOP-6FUB9PD:~$ mkdir -p netflix/{movies,tv_shows}/{action,comedy,drama,sci_fi}
```

This was powerful because it created an entire folder structure instantly.

---

### 4) `cd` — Changing Directories
I practiced moving through the tree structure.

```bash
judoski@DESKTOP-6FUB9PD:~$ cd netflix
judoski@DESKTOP-6FUB9PD:~/netflix$
```

Moving deeper:

```bash
judoski@DESKTOP-6FUB9PD:~$ cd netflix/tv_shows
judoski@DESKTOP-6FUB9PD:~/netflix/tv_shows$ ls
action  comedy  drama  sci_fi
```

Returning home:

```bash
judoski@DESKTOP-6FUB9PD:~/netflix/tv_shows$ cd ~
judoski@DESKTOP-6FUB9PD:~$
```

This reinforced Linux tree navigation.

---

### 5) `rmdir` — Removing Empty Directories
I learned that `rmdir` only works on **empty folders**.

```bash
rmdir dir1 dir2 dir3
```

Useful options:
- `-p` → remove parent directories
- `-v` → verbose confirmation

This taught me Linux’s **“empty box” safety rule**.

---

### 6) `cp` — Copying Files
I practiced copying files between folders.

```bash
judoski@DESKTOP-6FUB9PD:~/fruits$ cp banana.txt ~/futbolclubs/
```

This duplicated the file into another directory.

A major lesson here:
the destination must truly be a directory, not a file with a similar name.

---

### 7) `mv` — Moving and Renaming
I used `mv` both for renaming and moving.

Rename:
```bash
judoski@DESKTOP-6FUB9PD:~/fruits$ mv oragnes.csv apples.csv
```

Move:
```bash
judoski@DESKTOP-6FUB9PD:~/fruits$ mv apples.csv ~/futbolclubs/proArsenal/
```

This command is excellent for fast file organization.

---

### 8) `rm` — Permanent Delete
The `rm` command permanently deletes files.

```bash
judoski@DESKTOP-6FUB9PD:~/futbolclubs/proArsenal$ rm apples.csv
```

Useful options learned:

| Option | Purpose |
|---|---|
| `-i` | Ask before deleting |
| `-f` | Force delete |
| `-r` | Recursive folder delete |
| `--` | Delete hyphen-starting files |

A very important comparison today:

| Feature | `rm` | `rmdir` |
|---|---|---|
| Purpose | Deletes files and folders | Deletes empty folders only |
| Recursive | Yes (`-r`) | No |
| Force | Yes (`-f`) | No |

---

### 9) `uname` — System Information
This command displays system-level information.

Useful options:

| Option | Meaning |
|---|---|
| `-a` | All system info |
| `-s` | Kernel name |
| `-r` | Kernel release |
| `-m` | Machine architecture |
| `-o` | Operating system |

This helps understand the Linux environment deeply.

---

### 10) `locate` — Fast File Search
I used `locate` to quickly find files.

```bash
judoski@DESKTOP-6FUB9PD:~$ locate banana.txt
/home/judoski/fruits/banana.txt
```

Check existing only:
```bash
judoski@DESKTOP-6FUB9PD:~$ locate -e banana.txt
```

Count matches:
```bash
judoski@DESKTOP-6FUB9PD:~$ locate -c "*.txt"
```

A key lesson:
`locate` uses a **database snapshot**, not real-time search.

---

## What I Built / Practiced
Today’s practice was heavily hands-on.

I practiced:
- file listing
- sorting by time
- command piping
- nested directory creation
- moving through directory trees
- copying files
- renaming files
- permanent deletion
- recursive deletion logic
- fast file searching
- system inspection

The Netflix directory tree exercise was especially useful.

---

## Challenges Faced
Today came with several practical lessons.

| Challenge | Lesson |
|---|---|
| Forgot `|` pipe | Learned how command output flows |
| Tried sideways `cd` | Must go up with `..` or use full path |
| `rmdir` on non-empty folder | Use `rm -r` instead |
| File vs directory confusion | Verify destination with `ls -F` |
| Typos like `oragnes.csv` | Use tab completion |
| `locate` stale results | Refresh with `updatedb` |

These mistakes actually made today’s learning stronger.

---

## Key Takeaways
The biggest lessons from today:

- Linux commands become powerful when chained together
- syntax precision matters
- typos can break workflows
- `rm` and `rmdir` serve different purposes
- `mv` can both move and rename
- `locate` is fast because it uses a database
- terminal confidence comes from repetition

The strongest takeaway is that **Linux commands are simple individually, but extremely powerful when combined correctly**.

---

## Resources
- DEC Linux learning resource
- personal terminal practice
- live root prompt exercises using:
```bash
judoski@DESKTOP-6FUB9PD:~$
```

---

## Output
### Commands Practiced
```bash
ls -t fruits | head -1
ls -1
ls -l
pwd
mkdir -p netflix/{movies,tv_shows}/{action,comedy,drama,sci_fi}
cd netflix
cd netflix/tv_shows
cd ~
cp banana.txt ~/futbolclubs/
mv oragnes.csv apples.csv
rm apples.csv
locate banana.txt
uname -a
```
<img width="1089" height="135" alt="list all file" src="https://github.com/user-attachments/assets/1f08d2b7-4086-4681-93f4-e912d9ecdd2a" />
<br><br>

<img width="867" height="581" alt="cd" src="https://github.com/user-attachments/assets/49d1c343-579f-4b5a-9ab2-d6e1f6e27046" />
<br><br>

<img width="1221" height="232" alt="linux ls" src="https://github.com/user-attachments/assets/702fe648-6449-459a-8e12-36483386cb9c" />
<br><br>

<img width="1085" height="172" alt="linux pwd" src="https://github.com/user-attachments/assets/f2923b0e-fcd7-41ea-9ed1-d392f43cdd54" />
<br><br>

<img width="1152" height="420" alt="ls -l" src="https://github.com/user-attachments/assets/16572c2a-c7ce-4657-9f3c-a2f5109b80b5" />
<br><br>

<img width="1286" height="678" alt="linux rm" src="https://github.com/user-attachments/assets/7e86432e-e390-4b4a-b6d2-084eaa1c712d" />



### Mini Directory Structure Built
```text
netflix/
├── movies/
│   ├── action
│   ├── comedy
│   ├── drama
│   └── sci_fi
└── tv_shows/
    ├── action
    ├── comedy
    ├── drama
    └── sci_fi
```
