---
layout: post
title: Mastering sed
subtitle: The Stream Editor for Efficient Text Processing
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
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
### 2. Deleting Lines

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
### 3. Inserting and Appending Lines

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
### 4. Replacing Text in a Specific Line

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
### 5. Case-Insensitive Substitution

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
### 6. Printing Specific Lines

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
### 7. Replacing Multiple Patterns

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
### 8. Removing Extra Spaces

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

## Use Cases

- **Configuration Management** – Automate updates to configuration files.  
- **Data Cleaning** – Remove or replace unwanted data patterns in datasets.  
- **Log Processing** – Extract and format specific information from log files.  
- **Code Refactoring** – Modify source code files in bulk.  
- **Batch Text Processing** – Efficiently manipulate large text files.  

<!-- ## Key Features & Explanation
`sed` works by processing input line by line and applying transformations based on the provided commands.

### 1. Substituting Text
#### Syntax:
```sh
sed 's/old-text/new-text/' filename
```
#### Example:
```sh
sed 's/Linux/Ubuntu/' example.txt
```
This replaces the first occurrence of "Linux" with "Ubuntu" in each line.

To replace all occurrences in a line, use the `g` flag:
```sh
sed 's/Linux/Ubuntu/g' example.txt
```

### 2. Deleting Lines
#### Syntax to delete the Nth line:
```sh
sed 'Nd' filename  # Deletes the N-th line
```
#### Example:
```sh
sed '3d' example.txt  # Deletes the 3rd line
```
#### Syntax to delete all lines containing a specific pattern (Regular expression (RegEx)):
```sh
sed '/pattern/d' filename
```
#### Example:
```sh
sed '/[Ee][Rr][Rr][Oo][Rr]/d' logfile.txt # Deletes lines containing "ERROR" that is case insenstive
```

### 3. Inserting and Appending Lines
#### Insert before a line:
```sh
sed '3i\New line inserted' example.txt
```

#### Append after a line:
```sh
sed '3a\New line appended' example.txt
```

### 4. Extracting Specific Lines
To print only specific lines, use:
```sh
sed -n '2,4p' example.txt  # Prints lines 2 to 4
```
Syntax to print lines matching a pattern (Regular Expression (RegEx)):
```sh
sed -n '/pattern/p' example.txt
```

### 5. Removing Extra Spaces
```sh
sed 's/  */ /g' example.txt  # Converts multiple spaces into a single space
```

---

## Advanced Data Cleaning with `sed`

### 1. Remove Blank Lines
```sh
sed '/^$/d' example.txt
```

### 2. Convert Uppercase to Lowercase
```sh
sed 's/[A-Z]/\L&/g' example.txt
```

### 3. Add a Prefix or Suffix to Each Line
#### Add Prefix:
```sh
sed 's/^/PREFIX: /' example.txt
```
#### Add Suffix:
```sh
sed 's/$/ :SUFFIX/' example.txt
```

---

## Conclusion
`sed` is a powerful tool for text processing and data cleaning in Linux. With its substitution, deletion, insertion, and filtering capabilities, it becomes a crucial utility for anyone working with large text files or automation scripts.

For further learning, check out the official documentation:
[GNU Sed Manual](https://www.gnu.org/software/sed/manual/sed.html) -->