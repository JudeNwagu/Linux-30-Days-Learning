
# **Day 13 - Directory Operations in Linux for Data Engineering Workflows**

<img width="749" height="373" alt="Screenshot 2026-04-14 234220" src="https://github.com/user-attachments/assets/1918c471-4760-47c1-b456-7203404ded6f" />


Day 13 was not just about “folder commands.”
This was about understanding **how Linux directory operations map directly to the daily reality of a Data Engineer**:

* navigating ETL project folders
* tracing raw → processed → analytics paths
* locating lost datasets fast
* measuring storage pressure
* validating mounted storage
* cleaning stale staging folders safely
* understanding where jobs are running from

At this level, Linux stops being “commands to memorize” and becomes **operational thinking for data systems**.

The commands i covered:

* `cd`
* `pwd`
* `mkdir`
* `find`
* `du`
* `tree`
* `dirname`
* `rmdir`
* `lsblk`
* `mount`
* `dirs`
* `dir`

---

#  Objective

The objective of Day 13 was to build **directory intelligence for production-style data workflows**.

In real data environments, every pipeline depends on folder structure:

* ingestion folders receive batch files
* ETL jobs move data across zones
* logs are partitioned by date
* backups mount into safe locations
* archive jobs compress old partitions
* cleanup jobs remove empty temp folders

The aim was to learn how to:

1. **move confidently through Linux hierarchies**
2. **validate exact path location before destructive actions**
3. **design reusable directory structures**
4. **search large nested projects efficiently**
5. **analyze disk usage by project layer**
6. **inspect storage devices and mount relationships**
7. **clean directory trees safely without data loss**

This is the filesystem discipline behind **reliable data pipelines**.

---

#  What I Learned

## 1) `cd` — Navigating Like a Data Engineer

The `cd` command is the **foundation of workflow speed**.

Every engineering session starts with moving into the correct project layer.

### Moving into the ETL workspace

```bash id="xq6u8e"
judoski@DESKTOP-6FUB9PD:~$ cd project_zenith
judoski@DESKTOP-6FUB9PD:~/project_zenith$
```

This mirrors moving into:

* batch jobs
* dbt projects
* Spark scripts
* logs directories
* Airflow DAG folders

### Jumping to root for system-level work

```bash id="s4r8pw"
judoski@DESKTOP-6FUB9PD:~/project_zenith$ cd /
judoski@DESKTOP-6FUB9PD:/$ pwd
/
```

This matters when troubleshooting:

* `/var/log`
* `/mnt`
* mounted disks
* `/etc`
* Docker volumes

### Using absolute path correctly

One important lesson from your terminal:

```bash id="e9z0fr"
judoski@DESKTOP-6FUB9PD:/$ /home/judoski/project_zenith/analytics/gold
-bash: /home/judoski/project_zenith/analytics/gold: Is a directory
```

Linux treated the path like a command.

The correct version:

```bash id="p0j3dx"
cd /home/judoski/project_zenith/analytics/gold
```

### Why this matters

This is a **core terminal behavior lesson**:

> A path alone is not navigation.
> `cd` is what tells the shell you want movement.

That distinction becomes critical inside shell scripts and automation jobs.

---

## 2) `pwd` — Filesystem Verification Before Every Risky Move

`pwd` gives **positional certainty**.

```bash id="wyzwd6"
judoski@DESKTOP-6FUB9PD:~/project_zenith/analytics/gold$ pwd
/home/judoski/project_zenith/analytics/gold
```

In production workflows this protects you before:

* deleting partitions
* moving datasets
* archiving folders
* overwriting reports
* running cleanup scripts

### Important mistake you discovered

```bash id="w8ql4f"
judoski@DESKTOP-6FUB9PD:~/project_zenith/analytics/gold$ $PWD
-bash: /home/judoski/project_zenith/analytics/gold: Is a directory
```

This was excellent troubleshooting practice.

### Why it failed

`$PWD` expands to the directory string itself.

So Bash tried to **execute the path as a command**, which caused:

> `Is a directory`

### Better usage

Use:

```bash id="e0a4zq"
echo $PWD
```

or simply:

```bash id="yx0yxp"
pwd
```

### Why this matters

This teaches the difference between:

* **environment variables**
* **shell commands**
* **path strings**
* **executable commands**

That distinction is essential in scripting.

---

## 3) `mkdir` — Designing Data Pipeline Hierarchies

This command moves from usage into **filesystem architecture**.

```bash id="sjwh0n"
judoski@DESKTOP-6FUB9PD:~$ mkdir -v family_tree
mkdir: created directory 'family_tree'
```

This directly maps to real engineering structures like:

```text
raw/
processed/
analytics/
logs/
archive/
backup/
```

### Where this becomes powerful

You also covered multiple creation and parent creation.

This is how engineers rapidly scaffold:

* dated ingestion folders
* region partitions
* environment folders (`dev`, `prod`)
* backup snapshots
* temporary export zones

---

###  `mkdir` options worth remembering

| Option      | Use Case in Data Engineering                 |
| ----------- | -------------------------------------------- |
| `-v`        | Confirm directory creation during automation |
| `-p`        | Create nested partition folders safely       |
| `-m`        | Set permissions for shared ETL teams         |
| `--help`    | Quick syntax recall                          |
| `--version` | Verify GNU/coreutils behavior                |

A single sentence takeaway here: **`mkdir -p` is one of the most reused commands in ETL orchestration because pipelines often need date-based or environment-based nested folders created automatically.**

---

## 4) `find` — Dataset Discovery, Recovery, and Pipeline Debugging

This is one of the most practical commands for Data Engineers.

### Exact file search

```bash id="c1t7nn"
judoski@DESKTOP-6FUB9PD:~$ find . -name "movie1.csv"
./netflix/movies/comedy/movie1.csv
```

This is exactly how you locate:

* missing CSV drops
* late source files
* forgotten reports
* transformed parquet partitions
* old backups

---

### Case-insensitive search

```bash id="rdbwml"
find . -iname "movie1.csv"
```

Very useful when datasets come from mixed systems like:

* Windows exports
* S3 uploads
* manually named client files

---

## ⚠️ Critical wildcard lesson

This was the best troubleshooting point of the day.

### Failed command

```bash id="a0oqoc"
find ./fruits -name *.txt
```

### Error

```bash id="m8cbr2"
find: paths must precede expression
```

### Deep explanation

This failed because **Bash expanded the wildcard before `find` even started**.

So instead of receiving `"*.txt"`, `find` got:

```text
banana.txt countries.txt capitals.txt ...
```

which broke its syntax expectations.

### Correct command

```bash id="w6u2i6"
find ./fruits -name "*.txt"
```

### Why this matters deeply

This is a major shell scripting rule:

> **quote patterns when you want the command—not Bash—to interpret the wildcard.**

This matters in:

* cleanup scripts
* ingestion scans
* scheduled audits
* backup validation

---

###  Search Scope Comparison

| Scope                   | Best Scenario             |
| ----------------------- | ------------------------- |
| `find .`                | Current project only      |
| `find ~/project_zenith` | Specific external project |
| `find ~`                | Entire workspace          |
| `find /`                | Full system search        |

One sentence that matters here: **choosing the narrowest search scope improves performance dramatically when scanning large ETL workspaces or mounted data volumes.**

---

## 5) `du` — Storage Visibility for Data Projects

This command turns directories into **storage analytics**.

### Basic usage

```bash id="3r3xgo"
judoski@DESKTOP-6FUB9PD:~$ du project_zenith
```

This lets you measure:

* log growth
* raw dump size
* backup inflation
* partition imbalance
* warehouse storage hotspots

---

### Human-readable mode

```bash id="4pkc0s"
du -h dec
```

### Full file visibility

```bash id="rqk4h6"
du -a -h project_zenith
```

### Summary view

```bash id="woyb50"
du -s project_zenith
```

### Time-aware storage audit

```bash id="rw1jxf"
du -h --time project_zenith
```

This is extremely useful for **tracking recently modified data zones**.

---

###  Most useful `du` flags

| Option   | Why it matters                         |
| -------- | -------------------------------------- |
| `-h`     | Human-readable storage units           |
| `-a`     | Includes file-level detail             |
| `-s`     | Fast total size check                  |
| `--time` | Correlate storage with recent ETL jobs |
| `-d`     | Limit recursion depth                  |

One sentence takeaway: **`du` is one of the fastest ways to identify which stage of a data pipeline is consuming abnormal storage.**

---

## 6) `tree` — Visualizing Data Lake Hierarchy

This command gives **instant architecture clarity**.

Your `netflix` example perfectly simulates a **domain-partitioned data lake**.

```text
netflix/
├── movies/
├── tv_shows/
```

This mirrors real layouts like:

```text
sales/region/date/
logs/service/date/
warehouse/schema/table/
```

### Why it matters

This is useful for:

* README documentation
* onboarding engineers
* debugging misplaced files
* validating partition logic

One sentence insight: **`tree` converts hidden filesystem complexity into instantly understandable architecture diagrams.**

---

## 7) `dirname` — Parent Path Extraction for Automation

This is heavily used in shell scripting.

```bash id="26s1yq"
dirname /home/judoski/netflix/movies/comedy/movie1.csv
```

Output:

```text
/home/judoski/netflix/movies/comedy
```

This helps dynamic scripts derive:

* backup folders
* archive destinations
* log parents
* staging parents

One sentence takeaway: **`dirname` is essential when building reusable ETL scripts that must derive output folders dynamically from input file paths.**

---

## 8) `rmdir` — Safe Empty Directory Cleanup

Unlike `rm -r`, `rmdir` protects you by refusing non-empty folders.

That makes it excellent for:

* stale temp partitions
* unused daily folders
* empty staging zones
* old checkpoint paths

### Important challenge you hit

Your issue with nested hierarchy assumptions was excellent operational learning.

The problem was not the command itself—it was **directory shape mismatch**.

### Real lesson

Always verify structure first:

```bash id="5zpqvt"
tree
```

Then delete.

One sentence takeaway: **filesystem cleanup should always follow hierarchy validation, never memory alone.**

---

## 9) `lsblk` — Understanding Storage Infrastructure

This command moves beyond directories into **storage topology awareness**.

It helps you inspect:

* physical disks
* SSDs
* partitions
* mounted WSL drives
* external devices

This becomes critical when working with:

* large backup drives
* cloud block volumes
* Linux partitions
* Docker persistent storage

One sentence takeaway: **`lsblk` gives the infrastructure context behind where your data physically lives.**

---

## 10) `mount` — Connecting Storage to Data Workflows

This is where directory operations touch **real storage engineering**.

```bash id="5h3yds"
sudo mount <device> <mount_point>
```

This is how production systems expose:

* NAS storage
* NFS shares
* external SSDs
* cloud block volumes
* backup drives

Unmounting safely:

```bash id="g3brv8"
umount /mnt
```

### Why it matters

If data is not mounted correctly:

* ETL jobs fail
* backups miss files
* ingestion reads empty folders
* logs disappear

One sentence takeaway: **mount points are often the bridge between Linux pipelines and external data storage systems.**

---

#  Challenges Faced

The strongest learning moments today came from **shell interpretation mistakes and hierarchy assumptions**.

### 1) Wildcard expansion in `find`

* failed because Bash expanded first
* solved with quotes
* major scripting lesson

### 2) Path treated as executable

* absolute path alone caused “Is a directory”
* solved by prefixing with `cd`

### 3) `$PWD` misuse

* variable expanded into raw path
* shell tried to execute it
* solved with `echo $PWD`

### 4) Incorrect hierarchy deletion assumptions

* solved by validating structure with `tree`

These are the kinds of mistakes that actually make engineers stronger.

---

#  Key Takeaways

* directory commands are **workflow accelerators**
* `find` is **dataset discovery**
* `du` is **storage analytics**
* `tree` is **architecture visualization**
* `dirname` supports **dynamic automation**
* `lsblk` reveals **device topology**
* `mount` connects **storage to pipelines**
* `rmdir` enforces **safe cleanup discipline**

Day 13 strongly reflects **real operational filesystem skills used in data engineering environments**.

---

#  Resources

Built on previous continuity from:

* **Days 01–12:** Linux fundamentals + Project Zenith
* **Day 12:** file transformation workflows
* Data Engineering Community

---

#  Output

<img width="1362" height="718" alt="Screenshot 2026-04-15 160505" src="https://github.com/user-attachments/assets/6a64a386-368d-48bc-b2da-3250e3982066" />
<br><br>


<img width="1361" height="716" alt="Screenshot 2026-04-15 171511" src="https://github.com/user-attachments/assets/ab8f0588-2922-477a-9cc9-ce4462f55ee8" />
<br><br>

<img width="1359" height="709" alt="Screenshot 2026-04-15 171529" src="https://github.com/user-attachments/assets/25a680b9-66c0-4b68-b759-a344fe035971" />
<br><br>


<img width="1326" height="714" alt="Screenshot 2026-04-15 171554" src="https://github.com/user-attachments/assets/38159529-8c36-4da2-bade-c4aea4ab9180" />



