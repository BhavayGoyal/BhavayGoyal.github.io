---
layout: post
title: Exposition Assignment
subtitle: Topic name here
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

---

## Basic Usage of `sed`
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
#### Syntax:
```sh
sed 'Nd' filename  # Deletes the N-th line
```
#### Example:
```sh
sed '3d' example.txt  # Deletes the 3rd line
```
To delete all lines containing a specific pattern:
```sh
sed '/error/d' example.txt
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
To print lines matching a pattern:
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
[GNU Sed Manual](https://www.gnu.org/software/sed/manual/sed.html)
