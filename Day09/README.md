# Day 09 - Practical Linux Commands for Everyday File Work

## Objective

Today’s goal was to strengthen my Linux command-line foundation by learning practical commands used in real file workflows.

I focused on three highly useful commands:

* `basename` → extract clean filenames from paths
* `cat` → read, create, combine, and update file content
* `cksum` → verify file integrity after edits, copies, or transfers

The aim was not just to know the syntax, but to understand **where each command fits into real work**, especially documentation, data projects, scripting, and file validation.

---

## What I Learned

Linux commands make file operations faster, cleaner, and easier to automate.

Today’s practice showed me that even simple commands can improve how I work with:

* project notes
* exported datasets
* logs
* backups
* script outputs

Instead of navigating folders manually, these commands let me interact with files directly from the terminal in seconds.

---

### 1) `basename` — Extracting Clean File Names from Paths

The `basename` command removes the directory path and returns only the filename.

This is especially useful in:

* shell scripting
* automation workflows
* log processing
* dynamic file naming
* ETL and data pipeline outputs

### Syntax

```bash
basename [path] [suffix]
```

### Example 1: Extract the filename

**Command**

```bash
basename practice_files/all.txt
```

**Result**

```bash
all.txt
```

**Why this matters**
This is useful when a script receives a full file path, but I only need the final file name for display, logging, or renaming.

### Example 2: Remove file extension

**Command**

```bash
basename practice_files/all.txt .txt
```

**Result**

```bash
all
```

**Why this matters**
A clean filename without extension is useful when generating report names, folder labels, or dynamic output files.

### Option: Process multiple paths with `-a`

**Command**

```bash
basename -a practice_files/DE.txt netflix/tv_shows/comedy/movie4.csv
```

**Result**

```bash
DE.txt
movie4.csv
```

**Why this matters**
This helps when working with several file paths at once, especially in batch scripts.

### Option: Remove suffix with `-s`

**Command**

```bash
basename -s .csv netflix/tv_shows/comedy/movie4.csv movie5.csv movie6.csv
```

**Result**

```bash
movie4
movie5
movie6
```

**Why this matters**
A practical way to clean multiple exported CSV filenames before processing them.

### Option: NULL-separated output with `-z`

**Command**

```bash
basename -z netflix/tv_shows/comedy/movie4.csv
```

**Result**

```bash
movie4.csv
```

**Why this matters**
Useful in scripting scenarios where filenames may contain spaces.

---

### 2) `cat` — Working with File Content Quickly

The `cat` command is one of the most useful Linux commands for quick file interaction.

Today I used it to:

* read files
* create files
* combine multiple files
* append new content

### View a file

**Command**

```bash
cat project_note.txt
```

**Result**

```text
This is my Netflix Data Project
```

**Why this matters**
This is the fastest way to inspect a note, config file, or text output without opening an editor.

### View using full path

**Command**

```bash
cat /home/judoski/project_note.txt
cat ~/project_note.txt
```

**Result**

```text
This is my Netflix Data Project
This is my Netflix Data Project
```

**Why this matters**
I reinforced how `~` simplifies navigation to files in the home directory.

### Create a new file directly from terminal

**Command**

```bash
cat > advice
```

**Content entered**

```text
practice make perfect in data profession foundation is the bedrock of all things
```

**Why this matters**
A fast way to capture ideas, learning notes, or reminders without opening Nano or Vim.

### Merge multiple files into one

**Command**

```bash
cat DA DS DE > data_title
cat data_title
```

**Result**

```text
A data analyst i make sense of data

A data scientist, train and machine model
A data engineer, building pipeline for the end user
```

**Why this matters**
This is practical when consolidating documentation, combining logs, or merging outputs from multiple steps.

### Append new content to existing file

**Command**

```bash
cat >> data_title
```

**Content entered**

```text
A Data Architect is like a structural engineer for information
```

**Verification**

```bash
cat data_title
```

**Result**

```text
A data analyst i make sense of data

A data scientist, train and machine model
A data engineer, building pipeline for the end user
A Data Architect is like a structural engineer for information
```

**Why this matters**
This helps preserve existing content while continuously growing a knowledge file.

### Display all text files in a folder

**Command**

```bash
cat *.txt
```

**Why this matters**
Useful when quickly reviewing multiple exported notes or text-based outputs together.

---

### 3) `cksum` — Verifying File Integrity

The `cksum` command generates:

* CRC checksum value
* file size
* filename

It helps confirm whether a file changed unexpectedly.

This is useful after:

* copying datasets
* moving backup files
* downloading archives
* transferring logs

### Check a single file

**Command**

```bash
cksum data_title
```

**Result**

```text
1182594115 194 data_title
```

Repeated check:

```bash
cksum data_title
```

**Result**

```text
1182594115 194 data_title
```

**Why this matters**
Matching checksum values confirm the file remained unchanged.

### Check multiple files

**Command**

```bash
cksum countries.txt country.txt names.txt
```

**Result**

```text
795382239 112 countries.txt
1745570892 303 country.txt
1299627055 111 names.txt
```

**Why this matters**
This is useful when validating several files after a copy or cleanup task.

### Save checksum for later validation

**Command**

```bash
cksum file.txt > file_checksum.txt
```

**Why this matters**
This creates a reference record that can be reused later to confirm consistency.

### Compare current file against saved checksum

**Command**

```bash
cksum file.txt | diff - file_checksum.txt
```

**Why this matters**
No output means the file is still identical.

This is valuable for:

* backup validation
* config monitoring
* dataset verification
* export consistency checks

---

## What I Built / Practiced

Today’s practice was very hands-on.

I worked on:

* extracting filenames from nested paths
* cleaning file extensions from CSV exports
* creating terminal notes
* merging role-based learning files
* appending new knowledge to an existing file
* validating file consistency using checksums

One practical output from today was building and extending:

```text
data_title
```

This file became a growing note about data roles across the modern data ecosystem.

---

## Challenges Faced

The main challenge today was being intentional with file redirection.

I had to carefully distinguish between:

* `>` → create new file or overwrite
* `>>` → append without losing previous content

Mixing them up can accidentally remove existing work.

Another key lesson was understanding that `cksum` is excellent for **error detection**, but it is **not a security tool**.

It helps verify accidental corruption, not malicious tampering.

---

## Key Takeaways

Today reinforced that Linux efficiency comes from mastering simple commands deeply.

My biggest lessons:

* `basename` simplifies path-heavy workflows
* `cat` makes content interaction fast
* `cksum` adds confidence when handling important files

The real value is not memorizing syntax.

It is knowing **when to use the right command in the right workflow**.

For example:

* use `basename` in scripts
* use `cat` in quick documentation work
* use `cksum` before trusting copied or transferred files

That practical confidence is what makes Linux powerful.

---

## Resources

* GeeksforGeeks Linux command-line learning resource
* WSL terminal practice environment
* Personal practice files:

  * `project_note.txt`
  * `data_title`
  * `countries.txt`

---

## Output

### Commands practiced

```bash
basename practice_files/all.txt
basename practice_files/all.txt .txt
basename -a practice_files/DE.txt netflix/tv_shows/comedy/movie4.csv
basename -s .csv netflix/tv_shows/comedy/movie4.csv movie5.csv movie6.csv
cat project_note.txt
cat > advice
cat DA DS DE > data_title
cat >> data_title
cksum data_title
cksum countries.txt country.txt names.txt
```

### Practical file built

```text
data_title
```

### Key validation outcome

Verified that repeated checksum results remained identical, confirming the file had not changed after review.
