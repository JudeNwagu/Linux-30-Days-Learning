# Day 07 - File Metrics and Downloading Data with wc and wget

## Objective

The goal for today was to understand how to **measure file content using `wc`** and learn how to **download files from the internet using `wget`**, which is essential for handling datasets in real-world workflows.

---


## What I Learned

* `wc` helps count lines, words, characters, and bytes in files
* `wc` can work with single or multiple files
* Different flags allow targeted analysis like lines, words, or longest line
* `wget` is used to download files directly from the internet
* `wget` supports background downloads and resume for interrupted files
* Both commands are practical for data validation and data ingestion

---

## What I Built / Practiced

* Measured dataset size and structure using `wc`
* Compared multiple files to validate consistency
* Practiced downloading files using `wget`
* Understood how Linux handles file size vs content structure

---

## Challenges Faced

* Interpreting multiple outputs from `wc` correctly
* Understanding difference between bytes and characters
* Realizing `wget` works without opening a browser

---

## Key Takeaways

* `wc` is a fast way to validate dataset completeness
* File size does not always mean number of records
* `wget` is powerful for automating data downloads
* These commands are useful in real data workflows

---

## Resources

* DEC Linux learning guide
* Manual pages using `man wc` and `man wget`
* Personal practice files

---

## Output

### 1. Using `wc` on a Single File

```bash
judoski@DESKTOP-6FUB9PD:~$ wc countries.txt
 15  16 112 countries.txt
```

**Interpretation**

* Lines: 15
* Words: 16
* Bytes: 112

**Why It Matters**
I used this to confirm that my dataset has the expected number of records before using it for analysis.

---

### 2. Using `wc` on Another File

```bash
judoski@DESKTOP-6FUB9PD:~$ wc capitals.txt
 15  18 123 capitals.txt
```

**Interpretation**

* Lines: 15
* Words: 18
* Bytes: 123

**Why It Matters**
This helped me compare both datasets and ensure they align in structure.

---

### 3. Using `wc` on Multiple Files

```bash
judoski@DESKTOP-6FUB9PD:~$ wc countries.txt capitals.txt
 15  16 112 countries.txt
 15  18 123 capitals.txt
 30  34 235 total
```

**Why It Matters**
This gives a combined summary, which is useful when working with multiple datasets.

---

### 4. Count Lines Only

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -l countries.txt
15 countries.txt
```

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -l countries.txt capitals.txt
 15 countries.txt
 15 capitals.txt
 30 total
```

**Why It Matters**
Used to quickly check if rows are missing after editing a dataset.

---

### 5. Count Words Only

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -w countries.txt
16 countries.txt
```

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -w countries.txt capitals.txt
 16 countries.txt
 18 capitals.txt
 34 total
```

**Why It Matters**
Helpful when validating text-heavy data or logs.

---

### 6. Count Bytes

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -c countries.txt
112 countries.txt
```

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -c capitals.txt
123 capitals.txt
```

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -c countries.txt capitals.txt
112 countries.txt
123 capitals.txt
235 total
```

**Why It Matters**
Useful when monitoring file size for storage or transfer.

---

### 7. Count Characters

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -m countries.txt
112 countries.txt
```

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -m countries.txt capitals.txt
112 countries.txt
123 capitals.txt
235 total
```

**Why It Matters**
Helps detect encoding differences in files.

---

### 8. Longest Line in File

```bash
judoski@DESKTOP-6FUB9PD:~$ wc -L countries.txt capitals.txt
 11 countries.txt
 12 capitals.txt
 12 total
```

**Why It Matters**
Useful when checking column width or formatting issues.

---

### 9. Check Version

```bash
judoski@DESKTOP-6FUB9PD:~$ wc --version
wc (GNU coreutils) 9.4
```

**Why It Matters**
Helps confirm compatibility when working across systems.

---

## Working with `wget`

### 10. Download a File

```bash
wget http://example.com/sample.php
```

**Why It Matters**
Used to download datasets directly without opening a browser.

---

### 11. Download in Background

```bash
wget -b http://www.example.com/samplepage.php
```

**Why It Matters**
Allows downloads to run while working on other tasks.

---

### 12. Save Logs to File

```bash
wget http://www.example.com/filename.txt -o /path/filename.txt
```

**Why It Matters**
Helps track download activity for debugging.

---

### 13. Resume Download

```bash
wget -c http://example.com/samplefile.tar.gz
```

**Why It Matters**
Prevents restarting large downloads when interrupted.

---

### 14. Set Retry Attempts

```bash
wget --tries=10 http://example.com/samplefile.tar.gz
```

**Why It Matters**
Improves reliability on unstable networks.

---

### 15. Set Wait Time

```bash
wget -w 10 http://example.com/large_file.zip
```

**Why It Matters**
Prevents overwhelming servers when downloading multiple files.

---

### 16. Recursive Download

```bash
wget -r http://example.com/
```

**Why It Matters**
Useful for downloading full datasets or documentation sites.

---

### 17. Download from File List

```bash
wget -i urls.txt
```

**Why It Matters**
Allows batch downloading of multiple datasets.

---

<img width="1347" height="602" alt="Linux wc 1" src="https://github.com/user-attachments/assets/f56595f7-1673-42df-89bb-4d60097d35be" />
<br><br>

<img width="1335" height="614" alt="Linux wc 2" src="https://github.com/user-attachments/assets/efb21859-cd2a-4fdf-867b-1fb80c7772f2" />
<br><br>

<img width="1265" height="621" alt="Linux wc" src="https://github.com/user-attachments/assets/d84cb9f6-e4ec-4e5d-a3c0-badc40447cea" />
<br><br>


## Final Reflection

Today shifted my learning from **just working with files locally to interacting with external data sources**.

The biggest takeaway:

**Linux is not just for managing files, it is also a powerful tool for collecting and validating data before analysis.**
