
# Day 08 - Linux Workflow Simulation for Data Engineering Environments

## Objective
The goal for today was to simulate how Linux supports the operational side of data engineering workflows.

Instead of focusing only on isolated commands, I built a structured Linux environment that mirrors how data teams manage:
- layered storage zones
- schema references
- system logs
- storage diagnostics
- process monitoring
- cleanup workflows

This practice was designed to strengthen the Linux foundations required for data engineering environments, where reliability, structure, and validation matter as much as the data itself.

---

## What I Learned

Today strengthened my understanding of Linux as a system operations tool.

### 1) Environment verification matters first

Before building anything, I confirmed:

```bash
whoami
uname -a
pwd
which grep
which sort
```

Output:

```bash
judoski
Linux DESKTOP-6FUB9PD 6.6.87.2-microsoft-standard-WSL2
/home/judoski
/usr/bin/grep
/usr/bin/sort
```

### Why it matters

This mirrors how engineers verify:

* active user context
* kernel compatibility
* working directory
* binary availability

before starting any pipeline job.

---

### 2) Structured directories make data workflows cleaner

I used one command to build the entire project structure.

```bash
mkdir -p project_zenith/{raw_data/bronze,processed_data/silver,analytics/gold,logs/system}
```

This introduced a practical **Bronze → Silver → Gold style workflow**:

* **Bronze** → raw ingestion
* **Silver** → cleaned data
* **Gold** → analytics-ready outputs

### Why it matters

This is how data platforms avoid mixing raw files with trusted business datasets.

---

### 3) Symbolic links simplify schema version control

I created a schema file:

```bash
touch schema_v1.json
```

Then linked it:

```bash
ln -s raw_data/bronze/schema_v1.json current_schema.json
```

Validation:

```bash
ls -l current_schema.json
```

Output:

```bash
current_schema.json -> raw_data/bronze/schema_v1.json
```

### Why it matters

Scripts can always read `current_schema.json` while the real versioned file changes behind the scenes.

This is very useful in ETL pipelines.

---

### 4) Linux can act like a mini incident pipeline

I created simulated logs:

```bash
cat > daily_log.txt
```

Then filtered only failures:

```bash
grep "ERROR" daily_log.txt > incident_report.txt
```

Output:

```bash
2026-04-01: ERROR: Timeout on Database_A
2026-04-02: ERROR: Authentication failed on Database_B
```

### Why it matters

This is exactly how log filtering works in monitoring systems.

Instead of scanning hundreds of lines manually, Linux can isolate critical failures instantly.

---

### 5) Sorting infrastructure nodes improves readability

I created database node metadata:

```bash
cat > db_nodes.txt
Node_C
Node_A
Node_Z
Node_B
```

Then sorted it:

```bash
sort db_nodes.txt
```

Output:

```bash
Node_A
Node_B
Node_C
Node_Z
```

### Why it matters

Sorted metadata helps with:

* node inventory checks
* infrastructure comparison
* audit consistency
* easier automation

---

### 6) Storage and process monitoring are essential

I inspected:

```bash
df -h
du -sh project_zenith
ps -e | grep bash
```

Key outputs:

```bash
/dev/sdd 1007G 3.8G 952G 1%
48K project_zenith
352 pts/0 00:00:00 bash
436 pts/1 00:00:00 bash
```

### Why it matters

This connects directly to:

* disk pressure monitoring
* project size validation
* stuck shell/job inspection

---

## What I Built / Practiced

Today’s practice focused on simulating the Linux operational workflow that supports a data engineering environment.

### Final Project Structure

```text
project_zenith/
├── analytics/
│   └── gold/
├── processed_data/
│   └── silver/
├── logs/
│   └── system/
│       ├── daily_log.txt
│       ├── incident_report.txt
│       └── schema_v1.json
├── db_nodes.txt
└── current_schema.json
```

### Workflow practiced

* system validation
* layered directory architecture
* schema linking
* log filtering
* node sorting
* storage diagnostics
* process filtering
* recursive cleanup
* command history review

---

## Challenges Faced

The most valuable part of today was the mistakes and fixes.

### 1) Broken symbolic link

Initial output:

```bash
cat: current_schema.json: No such file or directory
```

### Why it happened

The link originally pointed to:

```bash
docs/database/schema.sql
```

which did not exist.

### Fix

```bash
ln -sf raw_data/bronze/schema_v1.json current_schema.json
```

### Why it matters

Broken links can break data jobs, so validating with `ls -l` is critical.

---

### 2) Wrong path while reading incident report

Error:

```bash
cat: project_zenith/logs/system/incident_report.txt: No such file or directory
```

### Fix

Moved back to home:

```bash
cd ~
cat project_zenith/logs/system/incident_report.txt
```

### Why it matters

This reinforced **absolute path awareness**.

---

### 3) Wrong folder name during cleanup

Error:

```bash
rm: cannot remove 'project_zenith/raw-data'
```

### Fix

```bash
rm -r project_zenith/raw_data
```

### Why it matters

Tiny naming mistakes can be dangerous with recursive delete commands.

---

### 4) Incorrect tail syntax

Error:

```bash
tail: cannot open 'n-'
```

### Fix

```bash
history | tail -n 20
```

### Why it matters

Command syntax precision is everything in Linux.

---

## Key Takeaways

Linux is the operational backbone behind reliable data engineering environments.

My biggest lessons:

* always verify environment first
* structure folders like real data layers
* symbolic links simplify schema management
* `grep` can act like log filtering logic
* `sort` improves metadata organization
* `df`, `du`, and `ps` are system health tools
* safe cleanup requires exact paths
* mistakes improve command confidence faster than theory

The strongest takeaway:

> Linux is not just command memorization. It is how data workflows, system checks, logging, and cleanup are executed safely in production environments.

---

## Resources

* Days 01 to 08 Linux learning series
* WSL2 terminal practice
* DEC Linux learning materials
* personal Data Engineering workflow simulation
* Linux manual pages and command experimentation

---

## Output

### Core Commands Used

```bash
whoami
uname -a
pwd
which grep
which sort
mkdir -p project_zenith/{raw_data/bronze,processed_data/silver,analytics/gold,logs/system}
touch schema_v1.json
ln -sf raw_data/bronze/schema_v1.json current_schema.json
grep "ERROR" daily_log.txt > incident_report.txt
grep -c "Database" daily_log.txt
sort db_nodes.txt
df -h
du -sh project_zenith
ps -e | grep bash
rm -r project_zenith/raw_data
history | tail -n 20
```

### Final Validation Output

```bash
judoski@DESKTOP-6FUB9PD:~$ ls -R project_zenith
project_zenith:
analytics            db_nodes.txt  processed_data
current_schema.json  logs

project_zenith/logs/system:
daily_log.txt  incident_report.txt  schema_v1.json
```


