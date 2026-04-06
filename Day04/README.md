# Day 04 - Linux Command Revision, File Creation, and Process Inspection

## Objective
The goal for today was to **reinforce previously learned Linux commands through active recall** and then continue learning more essential commands for file creation, content viewing, process inspection, and command documentation.

Today’s focus was not just learning new commands, but **strengthening memory through repetition**, which is one of the best ways to make terminal work feel natural over time.

---

## What I Learned
I started today with **revision practice using my Netflix directory project**, which helped reinforce navigation, directory listing, and movement through the Linux tree structure.

### Revision Practice: Revisiting Navigation
First, I listed my home directory contents and sorted them by modification time.

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -lt
total 112
drwxr-xr-x 2 judoski judoski 4096 Apr  3 16:52 fruits
drwxr-xr-x 4 judoski judoski 4096 Apr  3 16:24 futbolclubs
drwxr-xr-x 4 judoski judoski 4096 Apr  3 14:52 netflix
```

This helped me quickly identify my most recently active folders.

I then moved into the Netflix project structure:

```bash
cd netflix
cd movies
cd ..
cd tv_shows
```

This reinforced:
- `cd` for navigation
- `cd ..` for moving one level up
- `ls` for checking contents
- understanding the directory hierarchy visually

A major lesson came when moving to root:

```bash
judoski@DESKTOP-6FUB9PD:~/netflix/tv_shows/drama$ cd /..
judoski@DESKTOP-6FUB9PD:/$
```

This demonstrated an important Linux truth:

> **The root directory `/` is the highest point in the file system tree.**
> You cannot move above it.

That made the Linux hierarchy much clearer.

---

### System Identity with `uname`
I continued with `uname` revision to inspect my system.

```bash
uname -s
uname -r
uname -m
uname -o
uname -a
```

| Flag | Meaning | My Result |
|---|---|---|
| `-s` | Kernel name | Linux |
| `-r` | Kernel release | 6.6.87.2-microsoft-standard-WSL2 |
| `-m` | Architecture | x86_64 |
| `-o` | Operating system | GNU/Linux |
| `-a` | Full system info | Complete environment details |

This was especially useful because it confirms I’m working inside **WSL2**, which is important for future data engineering workflows.

---

### New Command: `touch`
The `touch` command creates new empty files or updates timestamps.

```bash
judoski@DESKTOP-6FUB9PD:~/netflix$ touch new_release_dump.csv
```

I immediately practiced organizing the file:

```bash
mv new_release_dump.csv movies/sci_fi
```

Then created another:

```bash
touch stranger_things.txt
mv stranger_things.txt tv_shows/sci_fi
```

This made the Netflix project feel like a **real mini data pipeline structure**.

#### Useful `touch` options
| Option | Purpose |
|---|---|
| `-a` | Update access time only |
| `-m` | Update modification time only |
| `-c` | Update existing file only, don’t create |

---

### New Command: `ln`
The `ln` command creates links between files.

```bash
ln -s file1.txt link1.txt
```

This is useful for:
- creating shortcuts
- reducing duplicates
- referencing files from multiple locations

Today’s key takeaway:
> links help manage files efficiently without copying the actual content.

---

### New Command: `cat`
The `cat` command became today’s main file content tool.

#### Reading a file
```bash
cat project_note.txt
```

Output:
```text
This is my Netflix Data Project
```

#### Reading with full path
```bash
cat /home/judoski/project_note.txt
cat ~/project_note.txt
```

This strengthened my understanding of:
- relative paths
- absolute paths
- home shorthand `~`

#### Creating a file with content
```bash
cat > advice
practice make perfect in data profession foundation is the bedrock of all things
```

This taught me how terminal input can directly create content.

---

### New Command: `clear`
The `clear` command simply refreshes the terminal workspace.

```bash
clear
```

This is small, but very useful for staying organized during long sessions.

---

### New Command: `ps`
Today was my first deeper look into Linux processes.

```bash
ps
```

Output:
```text
PID TTY          TIME CMD
395 pts/2    00:00:01 bash
1646 pts/2   00:00:00 ps
```

This introduced:
- `PID` → process ID
- `TTY` → terminal session
- `TIME` → CPU time used
- `CMD` → process name

#### `ps -e`
I also learned how to display all running processes.

```bash
ps -e
```

This shifted my learning from **user-level commands into system-level awareness**.

---

### New Command: `man`
The `man` command is Linux’s built-in documentation system.

```bash
man ls
```

This command is powerful because it teaches you how to **learn commands directly from the terminal itself**.

#### Useful `man` options
| Option | Meaning |
|---|---|
| `man [cmd]` | Open manual |
| `-f` | Short description |
| `-k` | Search by keyword |
| `-a` | Show all matches |
| `Q` | Quit manual |
| `Space` | Next page |

This command is one of the most important long-term Linux learning tools.

---

## What I Built / Practiced
Today’s practice centered around:
- revising navigation inside the Netflix directory
- moving between project and system root
- creating realistic project files
- organizing files into category folders
- reading files using multiple path styles
- creating text directly in terminal
- inspecting active processes
- learning how to self-document commands using `man`

The Netflix structure is gradually becoming a **real simulated data project workspace**.

---

## Challenges Faced
Today’s learning had several important hurdles.

| Challenge | Lesson Learned |
|---|---|
| Tried `cd /..` | Root `/` is the ceiling of the tree |
| File vs folder confusion with `cat` | `cat` reads files, not directories |
| Relative vs absolute path mistakes | Use `/` or `~` for full paths |
| Process tree confusion | `ps` helped reveal parent-child relationships |

These mistakes made the command line logic much clearer.

---

## Key Takeaways
The biggest lessons from today:

- revision makes commands stick faster
- Linux hierarchy always begins and ends at `/`
- `touch` is excellent for fast file creation
- `cat` is useful for both reading and creating content
- `ps` introduces system process awareness
- `man` is the best built-in Linux teacher
- active recall makes terminal work feel natural

The strongest takeaway:
> **learning Linux is less about memorizing commands and more about repeatedly using them in realistic workflows.**

---

## Resources
- DEC Linux learning guide
- personal Netflix directory practice
- WSL2 terminal exercises
- built-in manual pages using `man`

---

## Output
### Commands Practiced
```bash
ls -lt
cd netflix
cd movies
cd ..
cd tv_shows
cd /..
uname -a
touch new_release_dump.csv
mv new_release_dump.csv movies/sci_fi
touch stranger_things.txt
mv stranger_things.txt tv_shows/sci_fi
cat ~/project_note.txt
cat > advice
clear
ps
ps -e
man ls
```

### Updated Netflix Structure
```text
netflix/
├── movies/
│   └── sci_fi/
│       └── new_release_dump.csv
└── tv_shows/
    └── sci_fi/
        └── stranger_things.txt
```

<img width="1287" height="394" alt="linux cd" src="https://github.com/user-attachments/assets/c67f88df-addd-4ad1-9ee5-8fada10bffd7" />
<br><br>

<img width="1351" height="671" alt="linux manual" src="https://github.com/user-attachments/assets/a1a3f82d-d9d4-4aaf-b23e-7c114b0384b1" />
<br><br>

<img width="1347" height="681" alt="linux pratice" src="https://github.com/user-attachments/assets/fa7cc0f3-0e22-429b-8189-4350e5961166" />
<br><br>

<img width="1132" height="657" alt="linux ps" src="https://github.com/user-attachments/assets/ddef1b02-d70b-4a11-b29e-522aaa7c3534" />
<br><br>

<img width="1085" height="172" alt="linux pwd" src="https://github.com/user-attachments/assets/8e5b433e-3f5e-4fb2-ab52-ab40e453a19f" />
<br><br>

<img width="1286" height="678" alt="linux rm" src="https://github.com/user-attachments/assets/ad02d1ab-e999-437a-a12c-cd8ac60e14b1" />
