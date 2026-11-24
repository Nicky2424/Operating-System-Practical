
# Practical 2: Execution of Linux Commands

## Aim
To execute various Linux commands for:
1. Information Maintenance
2. File Management
3. Directory Management

## Requirements
- Linux Operating System
- Linux Terminal

---

# Part A: Information Maintenance Commands

### 1. wc (Word Count)
**Purpose:** Counts lines, words and characters in a file.

**Syntax:**
```bash
wc filename
```

**Example:**
```bash
wc sample.txt
```

**Explanation:** Displays the number of lines, words and bytes in a file.

### 2. clear
**Purpose:** Clears the terminal screen.

**Example:**
```bash
clear
```

**Explanation:** Removes previous commands and output from the terminal display.

### 3. cal (Calendar)
**Purpose:** Displays the calendar.

**Example:**
```bash
cal
```

To display a particular month:
```bash
cal 11 2026
```

**Explanation:** Displays the current or specified month's calendar.

### 4. who
**Purpose:** Displays currently logged-in users.

**Example:**
```bash
who
```

**Explanation:** Shows information about users currently logged into the system.

### 5. date
**Purpose:** Displays the current date and time.

**Example:**
```bash
date
```

**Explanation:** Displays the system's current date and time.

### 6. pwd (Present Working Directory)
**Purpose:** Displays the current working directory.

**Example:**
```bash
pwd
```

**Explanation:** Shows the complete path of the directory in which the user is currently working.

---

# Part B: File Management Commands

### 1. cat (Concatenate)
**Purpose:** Displays the contents of a file.

**Example:**
```bash
cat sample.txt
```

**Explanation:** Reads and displays the contents of a text file.

### 2. cp (Copy)
**Purpose:** Copies files from one location to another.

**Example:**
```bash
cp sample.txt copy.txt
```

**Explanation:** Creates a copy of sample.txt named copy.txt.

### 3. rm (Remove)
**Purpose:** Deletes a file.

**Example:**
```bash
rm copy.txt
```

**Explanation:** Removes the specified file.

### 4. mv (Move)
**Purpose:** Moves or renames files.

**Example:**
```bash
mv sample.txt newfile.txt
```

**Explanation:** Renames sample.txt to newfile.txt.

### 5. cmp (Compare)
**Purpose:** Compares two files byte by byte.

**Example:**
```bash
cmp file1.txt file2.txt
```

**Explanation:** Reports the first difference between two files. If they are identical, it produces no output.

### 6. comm
**Purpose:** Compares two sorted files line by line.

**Example:**
```bash
comm file1.txt file2.txt
```

**Explanation:** Displays lines that are common and unique to the two files in separate columns.

### 7. diff (Difference)
**Purpose:** Displays differences between two files.

**Example:**
```bash
diff file1.txt file2.txt
```

**Explanation:** Shows the lines that differ between two files.

### 8. find
**Purpose:** Searches for files and directories.

**Example:**
```bash
find . -name "*.txt"
```

**Explanation:** Searches for all text files in the current directory and its subdirectories.

### 9. grep (Global Regular Expression Print)
**Purpose:** Searches for a particular word or pattern in a file.

**Example:**
```bash
grep "Linux" sample.txt
```

**Explanation:** Displays lines containing the word Linux.

### 10. awk
**Purpose:** Processes and extracts information from text files.

**Example:**
```bash
awk '{print $1}' sample.txt
```

**Explanation:** Displays the first field of every line in the file.

---

# Part C: Directory Management Commands

### 1. cd (Change Directory)
**Purpose:** Changes the current working directory.

**Example:**
```bash
cd Documents
```

**Explanation:** Moves into the Documents directory.

To return to the previous directory:
```bash
cd ..
```

### 2. mkdir (Make Directory)
**Purpose:** Creates a new directory.

**Example:**
```bash
mkdir myfolder
```

**Explanation:** Creates a directory named myfolder.

### 3. rmdir (Remove Directory)
**Purpose:** Removes an empty directory.

**Example:**
```bash
rmdir myfolder
```

**Explanation:** Deletes myfolder if it is empty.

### 4. ls (List)
**Purpose:** Lists files and directories.

**Example:**
```bash
ls
```

**Explanation:** Displays the contents of the current directory.

To display detailed information:
```bash
ls -l
```

---

# Practical Demonstration

First, create a sample file:

```bash
mkdir linux-practice
cd linux-practice
echo "Linux is an operating system" > sample.txt
```

Now execute the following commands:

```bash
pwd
ls
cat sample.txt
wc sample.txt
date
who
cp sample.txt copy.txt
cmp sample.txt copy.txt
grep "Linux" sample.txt
find . -name "*.txt"
```

For file comparison, create two sorted files:

```bash
printf "Apple\nBanana\nMango\n" > file1.txt
printf "Apple\nGrapes\nMango\n" > file2.txt
comm file1.txt file2.txt
diff file1.txt file2.txt
```

**Note:** Practise `rm` only on test files. It deletes files, so check the filename before executing it.

---

# Screenshots

Add screenshots of the commands and their outputs here.

### Information Maintenance
![Information Maintenance Output](../images/linux-information.png)

### File Management
![File Management Output](../images/linux-file-management.png)

### Directory Management
![Directory Management Output](../images/linux-directory-management.png)

---

# Result

Successfully executed and studied various Linux commands related to information maintenance, file management and directory management.

---

# Conclusion

Linux commands help users interact with the operating system through the terminal. They are useful for managing files, directories and system information.
