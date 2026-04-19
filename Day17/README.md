

# Day 17 – Process Management in Linux

## Objective

Today’s focus was on understanding how Linux manages running processes and how to monitor, inspect, and control them effectively.

In a real-world environment (data pipelines, servers, ETL jobs), processes are constantly running in the background. Knowing how to track and manage them is critical for system stability, performance tuning, and troubleshooting.

---

## What I Learned

### 1. Understanding `ps` (Process Snapshot)

The `ps` command provides a **static snapshot** of running processes at a specific point in time.

```bash
judoski@DESKTOP-6FUB9PD:~$ ps
    PID TTY          TIME CMD
    395 pts/2    00:00:01 bash
   1646 pts/2    00:00:00 ps
```

**Breakdown of Columns**

| Column | Meaning                          |
| ------ | -------------------------------- |
| PID    | Unique Process ID                |
| TTY    | Terminal session                 |
| TIME   | CPU time used                    |
| CMD    | Command that started the process |

---

### 2. Viewing All Processes (`ps -e`)

```bash
ps -e
```

* Shows **all running processes**
* Includes system-level background services

---

### 3. Full Process Details (`ps -ef`)

```bash
judoski@DESKTOP-6FUB9PD:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  7 21:10 ?        00:00:05 /sbin/init
root           2       1  0 21:10 ?        00:00:00 /init
root           6       2  0 21:10 ?        00:00:00 plan9 --control-socket ...
```

**Key Insight**

* `PID 1` → first process (`init/systemd`)
* `PPID` → shows **parent-child relationship**

---

### 4. Processes Without Terminal (`ps -x`)

```bash
judoski@DESKTOP-6FUB9PD:~$ ps -x
    PID TTY      STAT   TIME COMMAND
    372 pts/0    Ss+    0:00 -bash
    495 ?        Ss     0:00 /usr/lib/systemd/systemd --user
```

* `?` → background service (daemon)
* Useful for inspecting system services

---

### 5. Filtering & Advanced Options

```bash
ps -p <PID>              # Specific process
ps -ef --forest          # Tree structure
ps -G root               # By group
```

---

## 6. Real-Time Monitoring with `top`

Unlike `ps`, `top` provides **live system monitoring**.

```bash
top
```

### Key Sections in `top`

#### Tasks

* Total processes
* Running, sleeping, stopped, zombie

#### CPU Usage (%Cpu)

* `us` → user processes
* `sy` → system processes
* `id` → idle CPU
* `wa` → waiting for I/O

#### Memory (RAM)

* Total, used, free
* Buff/cache

#### Swap

* Overflow memory when RAM is full

---

### Interactive Commands in `top`

| Key | Function                 |
| --- | ------------------------ |
| k   | Kill a process           |
| r   | Change priority (renice) |
| q   | Quit                     |

Example:

```bash
top
PID to Kill = 1869
```

---

## What I Built / Practiced

Today was highly hands-on. I practiced:

* Running `ps` to inspect processes
* Using `ps -ef` to understand process hierarchy
* Identifying system services vs user processes
* Using `ps -x` to inspect background processes
* Filtering processes by PID and group
* Running `top` for real-time monitoring
* Killing processes using interactive commands
* Adjusting process priority using `renice`

This felt like **real system monitoring**, not just commands.

---

## Challenges Faced

### 1. Static vs Real-Time Confusion

At first, it was unclear why `ps` doesn’t update automatically.

**Resolution:**

* `ps` = snapshot
* `top` = real-time

---

### 2. Understanding Process Hierarchy

Interpreting `PID` vs `PPID` was confusing initially.

**Resolution:**

* Every process is created by another process
* This forms a **tree structure**

---

### 3. Background Services (`?` in TTY)

Seeing `?` instead of terminal names was confusing.

**Resolution:**

* `?` = daemon (no terminal attached)

---

## Key Takeaways

* `ps` gives a **snapshot**, `top` gives **live monitoring**
* Every process has a **PID and parent (PPID)**
* Background services run without terminals
* System performance depends on **CPU + memory usage**
* Process management is critical for:

  * debugging systems
  * optimizing performance
  * managing servers

---

## Resources

* Linux terminal practice
* Manual pages (`man ps`, `man top`)
* geeksforgeeks

---

## Output

By the end of today, I can:

* Identify running processes and their details
* Understand process hierarchy and relationships
* Monitor system performance in real time
* Kill or reprioritize processes
* Distinguish between user processes and system services

This is a major step forward because **process management is the backbone of system control in Linux environments**, especially in **data engineering, DevOps, and production systems**.
