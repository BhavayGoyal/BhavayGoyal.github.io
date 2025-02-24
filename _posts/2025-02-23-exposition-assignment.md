---
layout: post
title: Mastering sed
subtitle: The Stream Editor for Efficient Text Processing
cover-img: /assets/img/bg.webp
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/bg.webp
tags: [assignment]
author: Bhavay Goyal, Heer Ahir, Ritika
---

# How to Install and Use `sed` (Linux Stream Editor) for Data Cleaning

## Introduction
`sed` (Stream Editor) is a powerful text-processing tool in Linux that allows you to perform search, replace, delete, insert, and filter operations on text files. It is widely used for data cleaning and manipulation tasks.

---

## Installing `sed`
### On Debian-based systems (Ubuntu, Debian)
```sh
sudo apt update
sudo apt install sed
```

### On Red Hat-based systems (CentOS, Fedora, RHEL)
```sh
sudo dnf install sed  # For Fedora 22+
sudo yum install sed  # For older versions
```

### On Arch Linux
```sh
sudo pacman -S sed
```

### On macOS (using Homebrew)
```sh
brew install gnu-sed
```

To verify the installation, run:
```sh
sed --version
```

### Windows Systems

Since `sed` is a Unix-based tool, Windows users can access it through one of the following methods:

- **Windows Subsystem for Linux (WSL)**  
  - Run a Linux distribution inside Windows and use `sed` just like on a native Linux system.  
  - Install WSL by following this guide: [Install WSL - Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install)  

- **Git for Windows (Git Bash)**  
  - Git Bash provides a Unix-like terminal on Windows that includes `sed`.  
  - Download Git for Windows here: [Git for Windows](https://gitforwindows.org/)  

---

## Understanding the `sed` Command Format

The basic syntax of sed is:
```sh
sed [OPTIONS] 'COMMAND' filename
```
Where:
- `Options` - Modify `sed` behavior (e.g., `-i` for inline editing).
- `COMMAND` – The actual operation (`s`, `d`, `i`, `a`, etc.).
- `filename` – The file to be processed (or input via stdin).

### Commonly Used `sed` Options

- `-i` – Edit files in-place (modifies the file directly).  
- `-n` – Suppress automatic printing of lines (useful with `p` to print only selected lines).  
- `-e` – Allows multiple `sed` commands in a single execution.  
- `-f` – Read commands from a separate script file instead of writing them inline.  

For example, replacing all insatnces of the word `"error"` with `"warning"` in a file (named `logfile.log`) and modifying it directly (we'll see more on this ahead):

```bash
sed -i 's/error/warning/g' logfile.log
```

### What is Redirection in sed (`>` and `>>`)

- `>` – Redirects output to a new file (overwriting it).
- `>>` – Redirects output to an existing file (appending to it).

For example, replacing text and saving the output to `output.txt`:

```bash
sed 's/old/new/g' filename > output.txt
```

---

## Key Features & Explanation
### 1. Text Substitution

#### Syntax:
```bash
sed 's/old_text/new_text/' filename # Replace first occuraence in each line
sed 's/old_text/new_text/g' filename # Replace all occurrences in each line
```

#### Example:
Replace "cat" with "dog" in each line.

```bash
sed 's/cat/dog/' animals.txt
```
#### Input:
```bash
I have a cat and a black cat.
```
#### Output:
```bash
I have a dog and a black dog.
```
### 2. Conditional Substitution

#### Syntax:
```bash
sed '/pattern/ s/old/new/' filename # Here pattern refers to Regular expression (RegEx)
```

#### Example:
Example: Replace "cat" with "dog" only in lines containing "pet" in animals.txt.

```bash
sed '/pet/ s/cat/dog/' animals.txt
```
#### Input (animals.txt):
```bash
I have a cat.
My pet is a cat.
Cats are independent.
```
#### Output:
```bash
I have a cat.
My pet is a dog.
Cats are independent.
```
Explanation: The substitution `s/cat/dog/` is applied only to lines matching the pattern "pet".
### 3. Deleting Lines

#### Syntax:
```bash
sed '/pattern/d' filename     # Delete lines containing a pattern (RegEx pattern)
sed 'Nd' filename             # Delete line number N
sed 'M,Nd' filename           # Delete lines from M to N
```

#### Example:
Delete line 3 from a file.

```bash
sed '3d' logs.txt
```
#### Input (logs.txt):
```bash
Line 1: Success
Line 2: Warning
Line 3: Error detected
Line 4: Success
```
#### Output:
```bash
Line 1: Success
Line 2: Warning
Line 4: Success
```
### 4. Inserting and Appending Lines

#### Syntax:
```bash
sed 'Ni\New Line' filename    # Insert a line before line N
sed 'Na\New Line' filename    # Append a line after line N
```

#### Example:
Insert "This is a new inserted line" before line 3.

```bash
sed '3i\This is a new inserted line' file.txt
```
#### Input (file.txt):
```bash
Line 1
Line 2
Line 3
Line 4
```
#### Output:
```bash
Line 1
Line 2
This is a new inserted line
Line 3
Line 4
```
### 5. Replacing Text in a Specific Line

#### Syntax:
```bash
sed 'Ns/old_text/new_text/' filename
```

#### Example:
Replace "apple" with "orange" only in line 2.

```bash
sed '2s/apple/orange/' fruits.txt
```
#### Input (fruits.txt):
```bash
Apple is red.
I love apple juice.
Apples are tasty.
```
#### Output:
```bash
Apple is red.
I love orange juice.
Apples are tasty.
```
### 6. Case-Insensitive Substitution

#### Syntax:
```bash
sed 's/old_text/new_text/I' filename   # 'I' flag for case-insensitive
```
#### Example:
Replace "hello" with "Hi" in a case-insensitive manner.
```bash
sed 's/hello/Hi/I' greetings.txt
```
#### Input (greetings.txt):
```bash
Hello world!
hello there!
```
#### Output:
```bash
Hi world!
Hi there!
```
### 7. Printing Specific Lines

#### Syntax:
```bash
sed -n 'N,Mp' filename   # Print lines from N to M
sed -n '/pattern/p' filename  # Print lines matching a pattern
```
#### Example:
Print only lines 2 to 4.
```bash
sed -n '2,4p' file.txt
```
#### Input (file.txt):
```bash
Line 1
Line 2
Line 3
Line 4
Line 5
```
#### Output:
```bash
Line 2
Line 3
Line 4
```
### 8. Replacing Multiple Patterns

#### Syntax:
```bash
sed -e 's/old1/new1/g' -e 's/old2/new2/g' filename
```
#### Example:
Replace "red" with "blue" and "green" with "yellow" in one command.
```bash
sed -e 's/red/blue/g' -e 's/green/yellow/g' colors.txt
```
#### Input (colors.txt):
```bash
I like red and green colors.
```
#### Output:
```bash
I like blue and yellow colors.
```
### 9. Removing Extra Spaces

#### Syntax:
```bash
sed 's/  */ /g' filename   # Replace multiple spaces with a single space
```
#### Example:
Convert multiple spaces into a single space.
```bash
sed 's/  */ /g' testfile.txt
```
#### Input (testfile.txt):
```bash
This    is   a   test   file.
```
#### Output:
```bash
This is a test file.
```
### 10. Performing In-Place Edits with Backup

#### Syntax:
```bash
sed -i.bak 's/pattern/replacement/' filename
```
#### Example:
Replace the first occurrence of "error" with "warning" in each line of log.txt, creating a backup named log.txt.bak.
```bash
sed -i.bak 's/error/warning/' log.txt
```
#### Input (log.txt):
```bash
error: file not found
error: access denied
```
#### Output (log.txt):
```bash
warning: file not found
warning: access denied
```
#### Backup (log.txt.bak):
```bash
error: file not found
error: access denied
```
Explanation: The `-i.bak` option edits the file in place and creates a backup with the `.bak` extension before making changes.

---
## Use Cases

- **Configuration Management** – Automate updates to configuration files.  
- **Data Cleaning** – Remove or replace unwanted data patterns in datasets.  
- **Log Processing** – Extract and format specific information from log files.  
- **Code Refactoring** – Modify source code files in bulk.  
- **Batch Text Processing** – Efficiently manipulate large text files.  

---

## Conclusion
`sed` is a powerful tool for text processing and data cleaning in Linux. With its substitution, deletion, insertion, and filtering capabilities, it becomes a crucial utility for anyone working with large text files or automation scripts.

## Further Readings
- For further learning, check out the official documentation:
[GNU Sed Manual](https://www.gnu.org/software/sed/manual/sed.html)
- If you want to learn more about RegEx, do check this out [Regex Tutorial](https://www.geeksforgeeks.org/write-regular-expressions/)