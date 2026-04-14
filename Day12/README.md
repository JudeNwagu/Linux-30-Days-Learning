
# Day 12 - Basic Data Transformation & Storage Workflows in Linux

## Objective

Today’s objective was to move beyond file inspection into **real data transformation workflows using Linux commands**.

The focus was to understand how Linux can help reshape raw text files into:

* selected fields
* sorted records
* merged datasets
* deduplicated rows
* horizontally combined files
* smaller split chunks
* compressed archive packages

This session felt like building a **command-line ETL toolkit**, where every Linux command acts like a transformation step inside a data pipeline.

---

## What I Learned

Today introduced the **core Linux commands for transforming structured and semi-structured text data**.

The major commands covered were:

| Category          | Commands |
| ----------------- | -------- |
| field extraction  | `cut`    |
| relational merge  | `join`   |
| horizontal merge  | `paste`  |
| file partitioning | `split`  |
| ordering          | `sort`   |
| deduplication     | `uniq`   |
| storage packaging | `tar`    |

The biggest shift in understanding today was:

> Linux can behave like a lightweight ETL engine before data even reaches Python, SQL, or Spark.

This is powerful because many preprocessing tasks can be handled directly in the terminal:

* clean
* merge
* sort
* split
* package
* transfer

---

# 1) `cut` - Column and Character-Level Extraction

The `cut` command became the first transformation layer today.

It helps isolate:

* fields
* character ranges
* specific byte positions

This is extremely useful when working with:

* CSV-like files
* fixed-width logs
* names
* IDs
* prefixes
* metadata columns

---

### Source File Used

```bash
judoski@DESKTOP-6FUB9PD:~$ cat names.txt
Ada August
adanna janu
adanne Febu
adaugo Marc
adachi jun
chi april
```

---

## Error-Driven Learning

One of the most important moments today was intentionally running:

```bash
judoski@DESKTOP-6FUB9PD:~$ cut names.txt
cut: you must specify a list of bytes, characters, or fields
Try 'cut --help' for more information.
```

### Why this matters

This error is actually a strong learning moment.

The terminal is teaching that:

> `cut` must always be given extraction logic.

Linux needs a clear instruction:

* delimiter + field
* character positions
* byte range

This reinforces precision in data transformation workflows.

---

## Extract First Field

```bash
judoski@DESKTOP-6FUB9PD:~$ cut -d " " -f1 names.txt
Ada
adanna
adanne
adaugo
adachi
chi
```

### Workflow Meaning

| Part     | Meaning            |
| -------- | ------------------ |
| `-d " "` | split by space     |
| `-f1`    | select first field |
| output   | first names only   |

### Real-world use

This mirrors:

* first-name extraction
* country column extraction
* user ID selection
* schema field isolation

---

## Character-Level Extraction

### First Letter

```bash
judoski@DESKTOP-6FUB9PD:~$ cut -c 1 names.txt
A
a
a
a
a
```

### First Three Characters

```bash
judoski@DESKTOP-6FUB9PD:~$ cut -c 1-3 names.txt
Ada
ada
ada
ada
ada
chi
```

### Specific Character Positions

```bash
judoski@DESKTOP-6FUB9PD:~$ cut -c 1,4 names.txt
A
an
an
au
ac
```

### Why this matters

This is very useful for:

* code prefixes
* state abbreviations
* log token extraction
* fixed-width data parsing
* short code generation

---

# 2) `join` - Relational Data Merging

Today’s most SQL-like command was `join`.

This introduced the Linux version of:

> **INNER JOIN logic**

It merges two files using a common key.

---

## The Failure That Taught the Biggest Lesson

```bash
judoski@DESKTOP-6FUB9PD:~$ join countries.txt capitals.txt
join: countries.txt:2: is not sorted: Egypt
join: capitals.txt:5: is not sorted: New Delhi
join: input is not in sorted order
```

This is one of the strongest engineering lessons so far.

### Core rule

The `join` command requires:

* both files sorted
* same key structure
* matching first field by default

Linux does **not scan randomly**.

It expects both files to already be aligned in sorted order.

---

## Best Engineering Fix

```bash
join <(sort countries.txt) <(sort capitals.txt)
```

This is powerful because it introduces:

> **process substitution**

Instead of sorting manually, Linux sorts both files in memory during execution.

### Why this matters

This is excellent for:

* lookup table enrichment
* country-capital joins
* dimension table merges
* ETL lookup workflows
* fast terminal joins

---

## Important `join` Options

| Option | Purpose                             |
| ------ | ----------------------------------- |
| `-1`   | key field for file1                 |
| `-2`   | key field for file2                 |
| `-t`   | custom delimiter                    |
| `-a1`  | left join style keep all file1 rows |

This directly maps to SQL joins.

---

# 3) `paste` - Horizontal Record Combination

The `paste` command merges files **side-by-side line by line**.

```bash
judoski@DESKTOP-6FUB9PD:~$ paste capitals.txt countries.txt
Abuja   Argentina
Beijing Australia
Berlin  Brazil
Brasilia        Canada
Buenos Aires    China
```

### Why this matters

This behaves like:

> column stitching

Useful for:

* rebuilding split exports
* quick feature engineering
* combining aligned text columns

---

## Serial Merge with `-s`

```bash
judoski@DESKTOP-6FUB9PD:~$ paste -s names.txt
Ada August adanna janu adanne Febu ...
```

This converts many rows into a single row.

Great for:

* payload creation
* text serialization
* API body generation
* compact exports

---

# 4) `split` - File Partitioning

This command is highly relevant for large datasets.

```bash
judoski@DESKTOP-6FUB9PD:~$ split fruits.txt
```

Generated:

* `xaa`
* `xab`

### Why this matters

This mirrors:

* partitioning large logs
* splitting datasets before upload
* chunking files for distributed systems
* easier transfer over unstable networks

---

## Best Split Options

| Need             | Command                     |
| ---------------- | --------------------------- |
| split by lines   | `split -l 5000 file chunk_` |
| split by bytes   | `split -b 50M file chunk_`  |
| numeric suffix   | `split -d file part_`       |
| verbose progress | `split --verbose`           |

This is directly useful for:

* S3 uploads
* partition movement
* distributed ingestion

---

# 5) `sort` - Organizing Records for Downstream Processing

The `sort` command became the **foundation command** for multiple workflows today.

It powers:

* `join`
* `uniq`
* ordering datasets
* numeric ranking
* date preparation

---

## Important Sort Options

| Option | Use Case                 |
| ------ | ------------------------ |
| `-n`   | numeric sort             |
| `-r`   | descending               |
| `-k`   | sort by column           |
| `-u`   | sort + remove duplicates |
| `-M`   | month sort               |
| `-c`   | validate sorted file     |

This is critical in ETL because sorted data improves:

* joins
* deduplication
* partition scans
* grouped processing

---

# 6) `uniq` - Duplicate Profiling & Cleanup

This was today’s **data quality command**.

### Input Data

```bash
judoski@DESKTOP-6FUB9PD:~$ cat dirtydata.txt
This is a test.
This is a test.
This is a test.

This is another line.
This is another line.
This is another line.
```

---

## Remove Duplicates

```bash
judoski@DESKTOP-6FUB9PD:~$ uniq dirtydata.txt
This is a test.

This is another line.
```

---

## Frequency Count

```bash
judoski@DESKTOP-6FUB9PD:~$ uniq -c dirtydata.txt
      3 This is a test.
      1
      3 This is another line.
```

This acts like quick profiling.

Useful for:

* duplicate events
* repeated categories
* frequency analysis
* quick anomaly checks

---

## Most Important Production Workflow

```bash
sort dirtydata.txt | uniq
```

This ensures every duplicate is adjacent before deduplication.

This is the industry-standard Linux cleanup pipeline.

---

# 7) `tar` - Data Packaging for Movement & Backup

This became today’s **storage engineering layer**.

---

## Create Archive

```bash
judoski@DESKTOP-6FUB9PD:~$ tar -cvf day11_data.tar *.txt
```

### Tar Flag Breakdown

| Flag | Meaning           |
| ---- | ----------------- |
| `-c` | create            |
| `-v` | verbose           |
| `-f` | filename          |
| `-x` | extract           |
| `-z` | gzip              |
| `-C` | extract to folder |

---

## Extract to Controlled Directory

```bash
judoski@DESKTOP-6FUB9PD:~$ tar -xvf day11_data.tar -C extracted_data
```

This is cleaner for:

* backup restores
* ETL staging
* folder isolation

---

## Compression Comparison

| Format     | Flag | Best Use      |
| ---------- | ---- | ------------- |
| `.tar.gz`  | `-z` | fast + common |
| `.tar.bz2` | `-j` | smaller       |
| `.tar.xz`  | `-J` | best ratio    |

---

## Archive Size Validation

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -c day11_data.tar.gz
1413 day11_data.tar.gz
```

This helps compare:

* raw vs compressed size
* transfer efficiency
* storage optimization

---

## Challenges Encountered

Today’s challenges were highly practical.

### 1) Sorting Constraint

`join` failed because files were not sorted.

This mirrors real ETL join issues.

---

### 2) Key Mismatch

Names like:

* New Zealand
* New Delhi

introduced spacing issues.

This shows why key normalization matters.

---

### 3) Delimiter Confusion

Wrong delimiters break extraction logic.

Lesson:

> command structure must match data structure

---

### 4) `uniq` Limitation

Duplicates must be adjacent.

That’s why:

```bash
sort file | uniq
```

is safer.

---

## Key Takeaways

Today Linux truly felt like a **text-based transformation engine**.

The strongest workflow today:

```bash
sort dirtydata.txt | uniq
```

Simple but production-ready.

This entire Day12 maps directly to:

* SQL joins
* dataframe merges
* ETL staging
* duplicate cleanup
* archive transfer
* cloud upload preparation

---

## Output

```bash
cut -d " " -f1 names.txt
cut -c 1-3 names.txt
join <(sort countries.txt) <(sort capitals.txt)
paste capitals.txt countries.txt
split fruits.txt
sort dirtydata.txt | uniq
tar -cvf day11_data.tar *.txt
```

---

<img width="1366" height="730" alt="cut 2" src="https://github.com/user-attachments/assets/2b053313-3959-4e0d-bd20-7d29cb341623" />
<br><br>

<img width="1352" height="711" alt="cut-c" src="https://github.com/user-attachments/assets/0e404abc-3e1a-4715-a565-196325657d9e" />
<br><br>

<img width="1366" height="591" alt="tar" src="https://github.com/user-attachments/assets/f73c13c1-1c3c-4bf4-8176-f726534a34c0" />
<br><br>

<img width="1360" height="712" alt="cut" src="https://github.com/user-attachments/assets/1c633005-b04f-4ee8-9a4d-3ef9f5e5c404" />
<br><br>

<img width="1350" height="716" alt="uniq" src="https://github.com/user-attachments/assets/73a77a41-3d40-4bb0-870a-c1c5e4d4a019" />





