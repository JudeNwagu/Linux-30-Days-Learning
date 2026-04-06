# Day 05 - Text Search, Output, User Identity, and Data Sorting

## Objective
The goal for today was to learn how Linux helps us **search through text, print output, confirm user identity, and organize data in a meaningful order**.

Today’s session focused on commands that are extremely useful when working with:
- log files
- configuration files
- datasets
- text documents
- terminal automation
- quick data checks

This made today feel very practical because the commands introduced the idea of **finding useful information fast instead of manually scanning files line by line**.

---

## What I Learned

### 1) Searching Text with `grep`
The `grep` command is one of the most useful Linux commands for searching text.

It helps locate:
- words
- phrases
- patterns
- matching lines in files

Basic syntax:

```bash
grep [options] pattern [file]
```

Example:

```bash
judoski@DESKTOP-6FUB9PD:~$ grep "may" country.txt
Thank you mayor for this opportunity
```

This shows how `grep` quickly scans a file and returns only lines containing the word.

This is especially useful for:
- searching logs
- finding SQL table names
- checking configuration files
- scanning documentation

---

### Common `grep` Options Practiced

#### Case-insensitive search
```bash
grep -i "Ada" names.txt
```

Output:

```text
Ada
adanna
adanne
adaugo
adachi
```

This taught me that `-i` ignores uppercase and lowercase differences.

---

#### Count matching lines
```bash
grep -c "ada" names.txt
```

Output:

```text
4
```

This is useful when you need a quick count instead of full matching lines.

---

#### Show matching filenames only
```bash
grep -l "ada" *
```

This returns only files containing the pattern.

A useful lesson from today:
when using `*`, Linux includes folders too, which is why I saw:

```text
grep: netflix: Is a directory
```

That helped reinforce the difference between **files and directories**.

---

#### Match whole words only
```bash
grep -w "Thank" country.txt
```

This avoids partial substring matches.

---

#### Show only matched text
```bash
grep -o "Thank" country.txt
```

Output:

```text
Thank
Thank
```

This is powerful for extracting repeated keywords.

---

#### Show line numbers
```bash
grep -n "ada" names.txt
```

Output:

```text
2:adanna
3:adanne
4:adaugo
5:adachi
```

This makes debugging easier because you know the exact line location.

---

#### Match lines starting with text
```bash
grep "^data" advice
```

The `^` symbol means:
> start of line

---

#### Match lines ending with text
```bash
grep "\.$" advice
```

The `$` symbol means:
> end of line

This introduced me to the idea of **simple pattern matching with regular expressions**.

---

### 2) Printing Output with `echo`
The `echo` command prints text directly to the terminal or writes text into files.

Example:

```bash
echo "nigeria and italy did not qualify..." >> country.txt
```

What I learned here:
- `echo` displays text
- `>>` appends content to an existing file
- this is useful for quick logging or notes

This command is simple but very useful for scripting later.

---

### 3) Confirming Current User with `whoami`
The `whoami` command tells you the currently logged-in user.

Example:

```bash
judoski@DESKTOP-6FUB9PD:~$ whoami
judoski
```

This is especially useful for:
- checking if you are root
- verifying active user session
- debugging permission issues
- confirming user context in scripts

A practical lesson:
> always confirm your user before running sensitive commands.

---

### 4) Organizing Data with `sort`
The `sort` command arranges file content in a logical order.

I first displayed the content:

```bash
cat dtype.txt
```

Then sorted it:

```bash
sort dtype.txt
```

Sorted output:

```text
Boolean: False
Boolean: True
DateTime: 2026-04-06
Float: 0.007
Float: 19.99
Integer: -102
Integer: 5500
JSON: {user: judoski}
Null: Empty value
String: This is a line of text.
UUID: f47ac10b-58cc-4372-a567-0e02b2c3d479
```

This showed how Linux automatically sorts alphabetically using ASCII order.

Important observations:
- numbers come before letters
- uppercase sorts before lowercase
- earlier letters appear first

---

### Useful `sort` Options
| Option | Purpose |
|---|---|
| `-o` | save output to a file |
| `-r` | reverse order |
| `-n` | numeric sorting |
| `-nr` | reverse numeric |
| `-k` | sort by column |
| `-u` | remove duplicates |
| `-M` | sort month names |

This command is highly useful when working with:
- CSV previews
- data validation
- log organization
- report preparation

---

## What I Built / Practiced
Today’s practice focused on **searching and organizing information quickly**.

I practiced:
- finding exact words inside files
- counting matches
- locating filenames
- using regex anchors
- appending text into files
- verifying current session user
- sorting mixed data types

This felt closer to **real data handling workflows**.

---

## Challenges Faced
Today’s biggest learning moments came from understanding command behavior.

| Challenge | Lesson Learned |
|---|---|
| `grep -l "ada" *` included folders | wildcard `*` includes files and directories |
| partial matches returned too much | `-w` helps target whole words |
| needed exact line locations | `-n` solves this |
| sorting mixed values | ASCII rules affect order |

These small discoveries made the commands much clearer.

---

## Key Takeaways
The biggest lessons from today:

- `grep` makes searching text fast and practical
- regex anchors `^` and `$` improve search precision
- `echo` is useful for fast file updates
- `whoami` confirms execution identity
- `sort` helps organize data without changing the original file
- wildcard behavior matters when searching many files

The strongest takeaway:
> Linux becomes far more powerful when you can search, filter, and organize text efficiently.

---

## Resources
- DEC Linux learning guide
- local text files (`country.txt`, `names.txt`, `dtype.txt`)
- terminal practice in WSL2

---

## Output
### Commands Practiced
```bash
grep "may" country.txt
grep -i "Ada" names.txt
grep -c "ada" names.txt
grep -l "ada" *
grep -w "Thank" country.txt
grep -o "Thank" country.txt
grep -n "ada" names.txt
grep "^data" advice
grep "\.$" advice
echo "..." >> country.txt
whoami
cat dtype.txt
sort dtype.txt
```

### Main Skills Reinforced
```text
Text search
Pattern matching
File appending
User identity check
Alphabetical sorting
Structured data organization
```

<img width="1357" height="686" alt="Linux grep 1" src="https://github.com/user-attachments/assets/75c16a00-052a-49b8-852d-371c29dcaa0d" />
<br><br>

<img width="1361" height="663" alt="linux grep" src="https://github.com/user-attachments/assets/b7bd03da-59ce-4043-8ae9-d43fd9197ce3" />
<br><br>

<img width="1361" height="663" alt="Linux grep (2)" src="https://github.com/user-attachments/assets/0771c11f-a5cb-43ea-b192-818d58fa881f" />
<br><br>

<img width="1363" height="680" alt="Linux whoami" src="https://github.com/user-attachments/assets/5f1a436a-581b-4425-9440-49db13d2f3e6" />
<br><br>

<img width="1326" height="515" alt="Linux whoami 2" src="https://github.com/user-attachments/assets/989b4076-d18e-45ff-a12a-87cd44117e00" />
