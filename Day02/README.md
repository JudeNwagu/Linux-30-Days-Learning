# Day 02 - Linux File System

## Objective
The goal for today was to understand how Linux stores, organizes, and manages files through its file system structure.

Rather than only memorizing folder names, I focused on understanding **why Linux uses a hierarchical tree structure**, how the major top-level directories support different system operations, and how to move through them confidently using navigation commands.

This is a foundational concept because every future Linux task—file handling, scripting, permissions, package management, and system administration—depends on understanding the file system first.

---

## What I Learned
Today I learned that the Linux file system is built on a **single hierarchical tree structure**, where everything starts from one central point:

```text
/
```

This symbol represents the **root directory**, which sits at the top of the Linux operating system.

Every file, folder, application, configuration, device file, and process-related location branches out from this single root. Once I understood this, the Linux environment started to feel much more logical.

I also learned that Linux supports multiple file system types such as:
- ext4
- XFS
- Btrfs

Each offers different advantages in performance, reliability, and storage management.

The most interesting part of today’s learning was understanding the story behind the major directories and how each one plays a specific role in the operating system.

### Understanding the Linux Directory Tree
The Linux directory tree is like a map of the operating system.

#### `/` — Root Directory
This is the starting point of the entire system.

A key distinction I learned:
- `/` = root of the whole Linux file system
- `/root` = home directory of the root user

#### `/bin`
Stores essential executable commands used by all users.

Examples:
- `ls`
- `cp`
- `ssh`
- `kill`

#### `/boot`
Contains files needed to start Linux:
- kernel files
- GRUB bootloader
- startup images

#### `/dev`
Stores hardware-related device files.

Example:
```text
/dev/sda1
```

This represents storage devices and partitions.

#### `/etc`
Stores system-wide configuration files.

This includes:
- application settings
- service configuration
- startup scripts
- host-specific settings

#### `/home`
Contains personal folders for regular users.

Example:
```text
/home/jude
```

#### `/lib`
Stores shared libraries required by applications.

#### `/media`
Used for automatically mounted removable devices like USB drives.

#### `/mnt`
Used for temporary manual mounts.

#### `/opt`
Stores optional third-party software.

#### `/sbin`
Contains system administration commands.

Examples:
- `fdisk`
- `reboot`
- `iptables`

#### `/tmp`
Stores temporary files created by running programs.

#### `/usr`
Stores user applications, libraries, documentation, and locally installed programs.

Important subfolders:
- `/usr/bin`
- `/usr/sbin`
- `/usr/lib`
- `/usr/local`

#### `/proc`
A virtual file system that exposes real-time system information.

Examples:
```text
/proc/meminfo
/proc/uptime
```

### Linux File System Layers
I also learned the **three major layers of the Linux file system**.

#### 1) Logical File System
The layer applications interact with for:
- open
- read
- write
- close
- permissions

#### 2) Virtual File System (VFS)
This provides a common interface for multiple file systems such as:
- ext4
- XFS
- NTFS
- FAT32

#### 3) Physical File System
This layer works directly with storage hardware and manages:
- disk blocks
- inodes
- data writing
- data retrieval

### File System Characteristics
I also studied the major characteristics that define a file system:
- space management
- filename rules
- directory organization
- metadata
- file utilities
- design limits

These determine speed, scalability, and storage efficiency.

---

## What I Built / Practiced
Today’s practical work focused on **directory navigation and understanding the Linux tree structure**.

I practiced:
- moving to the root directory
- entering configuration folders
- stepping backward in the tree
- jumping directly to the home directory
- listing directory contents
- tracing the Linux file system from `/`

Commands practiced:
```bash
pwd
ls
ls -l
ls -a
cd /
cd /etc
cd ..
cd ~
```

This practical movement made the file system easier to visualize and remember.

---

## Challenges Faced
The main challenge today was remembering the directories that seem similar at first.

The most confusing comparisons were:
- `/` vs `/root`
- `/bin` vs `/sbin`
- `/media` vs `/mnt`

Another challenge was understanding how Linux supports multiple file system formats while keeping the same command experience.

Learning about the **Virtual File System (VFS)** made this clearer.

---

## Key Takeaways
My biggest lessons from today are:

- everything in Linux starts from `/`
- every major folder has a defined responsibility
- Linux navigation becomes easier when the file system is seen as a tree
- `pwd`, `ls`, and `cd` are foundational navigation commands
- VFS allows Linux to work with many storage formats
- understanding the file system structure makes all future Linux tasks easier

The strongest takeaway from today is that the Linux file system is a **logical map of how the operating system works internally**.

---

## Resources
- DEC Linux learning resource
- terminal navigation practice
- personal file system tree notes

---

## Output
### Commands Practiced
```bash
pwd
ls
ls -l
ls -a
cd /
cd /etc
cd ..
cd ~
```

### Linux Directory Tree Explored
```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── sbin
├── srv
├── tmp
├── usr
└── proc
```

### Key Result
Today I can now confidently:
- identify the purpose of major Linux directories
- navigate the Linux tree using core commands
- explain the role of VFS and physical storage layers
- move between root, system, and home directories