# Linux Mastery: Zero to Expert
### A Comprehensive Journey from Beginner to Linux Expert

---

## 📚 Course Overview

This course is designed to take you from a complete Linux beginner to an intermediate system administrator capable of managing production servers, troubleshooting complex issues, and automating infrastructure. You'll use both your Ubuntu Desktop and Ubuntu Server throughout this journey.

**Prerequisites:**
- Ubuntu Desktop installed on laptop ✓
- Ubuntu Server installed on Raspberry Pi 4 B ✓
- Basic computer literacy
- Enthusiasm to learn!

**Estimated Time:** 12-16 weeks (10-15 hours/week)

---

## 🗺️ Course Structure

1. **Module 1:** Linux Fundamentals (Weeks 1-2)
2. **Module 2:** File System & Permissions (Week 3)
3. **Module 3:** Text Processing & Shell Scripting (Weeks 4-5)
4. **Module 4:** User & Process Management (Week 6)
5. **Module 5:** Networking Essentials (Week 7)
6. **Module 6:** Package Management & Software (Week 8)
7. **Module 7:** System Administration (Weeks 9-10)
8. **Module 8:** Web Servers & Services (Weeks 11-12)
9. **Module 9:** Security & Hardening (Week 13)
10. **Module 10:** Advanced Topics & Automation (Weeks 14-16)

---

## Module 1: Linux Fundamentals

### Week 1: Getting Started

#### Day 1: Terminal Basics
**Concept:** The terminal is your primary interface to Linux power.

```bash
# Open terminal: Ctrl+Alt+T (Ubuntu Desktop)
# For Raspberry Pi: SSH in from your laptop
ssh username@raspberry_pi_ip

# Basic navigation commands
pwd                    # Print Working Directory - where am I?
ls                     # List files in current directory
ls -l                  # Long format (detailed)
ls -la                 # Include hidden files (starting with .)
ls -lh                 # Human-readable file sizes

# Change directories
cd /home               # Go to /home directory
cd ~                   # Go to your home directory
cd ..                  # Go up one level
cd -                   # Go to previous directory
cd /                   # Go to root directory

# Getting help
man ls                 # Manual page for ls command
ls --help              # Quick help for ls
whatis ls              # Brief description of ls
```

**Exercise 1.1:** Navigate to at least 5 different directories and use `pwd` to confirm your location each time. Try to reach `/var/log`, `/etc`, `/usr/bin`, your home directory, and root `/`.

**Challenge 1.1:** Without using `cd`, list the contents of `/etc` while staying in your home directory. (Hint: You can provide a path to `ls`)

---

#### Day 2: File Operations

```bash
# Creating files and directories
touch file.txt         # Create empty file
mkdir mydir            # Create directory
mkdir -p dir1/dir2/dir3  # Create nested directories

# Copying files
cp file.txt file_backup.txt      # Copy file
cp file.txt /tmp/                # Copy to another location
cp -r mydir mydir_backup         # Copy directory recursively
cp -i file.txt existing.txt      # Interactive (asks before overwrite)

# Moving/renaming
mv file.txt newname.txt          # Rename file
mv file.txt /tmp/                # Move file
mv -i file.txt /tmp/             # Interactive move

# Deleting
rm file.txt                      # Delete file
rm -i file.txt                   # Interactive delete (safer!)
rm -r mydir                      # Delete directory recursively
rm -rf mydir                     # Force delete (DANGEROUS - be careful!)
rmdir emptydir                   # Remove empty directory only

# Viewing file contents
cat file.txt                     # Display entire file
less file.txt                    # Page through file (q to quit)
head file.txt                    # First 10 lines
head -n 20 file.txt              # First 20 lines
tail file.txt                    # Last 10 lines
tail -n 20 file.txt              # Last 20 lines
tail -f /var/log/syslog          # Follow file in real-time (Ctrl+C to stop)
```

**Exercise 1.2:** 
1. Create a directory called `linux_practice`
2. Inside it, create 5 text files named `day1.txt` through `day5.txt`
3. Copy the entire directory to `linux_practice_backup`
4. Rename one file from the backup
5. Delete one file from the original directory

**Challenge 1.2:** Create a nested directory structure: `projects/web/frontend/css` in one command, then navigate to the css folder and create a file called `style.css`.

---

#### Day 3: Viewing and Editing Files

```bash
# Viewing files
cat filename                     # Display entire file
tac filename                     # Display file in reverse
more filename                    # Page through file (old style)
less filename                    # Better paging (search with /pattern)

# Editing files - nano (beginner-friendly)
nano filename                    # Open file in nano
# Ctrl+O to save, Ctrl+X to exit
# Ctrl+K to cut line, Ctrl+U to paste
# Ctrl+W to search

# Editing files - vim (powerful, steep learning curve)
vim filename                     # Open file in vim
# Press 'i' to enter insert mode
# Press 'Esc' to exit insert mode
# Type ':w' to save
# Type ':q' to quit
# Type ':wq' to save and quit
# Type ':q!' to quit without saving

# Quick file creation with content
echo "Hello Linux" > file.txt    # Create/overwrite file
echo "More text" >> file.txt     # Append to file

# Comparing files
diff file1.txt file2.txt         # Show differences
```

**Exercise 1.3:**
1. Create a file called `myinfo.txt` using nano
2. Add your name, favorite Linux distribution, and today's date
3. Save and exit
4. View the file using `cat`, `less`, and `head`
5. Append "I'm learning Linux!" to the file using echo

**Challenge 1.3:** Using vim, create a file with at least 20 lines of text (any content). Practice inserting, deleting lines, and searching for text.

---

#### Day 4: Wildcards and Patterns

```bash
# Wildcards (* and ?)
ls *.txt                         # All files ending in .txt
ls file*                         # Files starting with 'file'
ls file?.txt                     # file1.txt, fileA.txt (single character)
ls file[123].txt                 # file1.txt, file2.txt, file3.txt
ls file[!123].txt                # Anything except 1, 2, or 3

# Brace expansion
echo file{1..5}.txt              # Generates: file1.txt file2.txt ... file5.txt
touch file{1..10}.txt            # Create 10 files at once
mkdir -p project/{src,bin,lib,docs}  # Create multiple directories

# Combining commands
cp *.txt backup/                 # Copy all .txt files
rm file[0-9].txt                 # Delete file0.txt through file9.txt
```

**Exercise 1.4:**
1. Create 15 files named `test1.txt` through `test15.txt` in one command
2. List only files `test1.txt` through `test9.txt`
3. Delete all files from `test10.txt` to `test15.txt` in one command
4. Create a directory structure with subdirectories: docs, images, scripts, configs

**Challenge 1.4:** Create 100 files named `log001.txt` through `log100.txt` using brace expansion, then delete only the even-numbered files.

---

### Week 2: System Information & Command Line Mastery

#### Day 5: System Information Commands

```bash
# System information
uname -a                         # All system information
uname -r                         # Kernel version
hostname                         # Computer name
hostnamectl                      # Detailed hostname info

# Hardware information
lscpu                           # CPU information
lsmem                           # Memory information
lsblk                           # Block devices (disks)
lsusb                           # USB devices
lspci                           # PCI devices
free -h                         # Memory usage (human-readable)
df -h                           # Disk space usage
du -h /path                     # Directory size
du -sh *                        # Size of each item in current dir

# System monitoring
top                             # Process monitor (press q to quit)
htop                            # Better process monitor (install if needed)
uptime                          # How long system has been running
date                            # Current date and time
cal                             # Calendar
```

**Exercise 1.5:**
1. Find out your kernel version
2. Check how much free memory you have
3. List all your disk partitions and their sizes
4. Find the size of your `/home` directory
5. Check your system uptime

**Challenge 1.5:** Create a text file that contains: your hostname, kernel version, CPU model, total RAM, and disk usage of root partition. Do this using command output redirection.

---

#### Day 6: Command Line Efficiency

```bash
# Command history
history                          # Show command history
history | grep keyword           # Search history
!number                          # Run command number from history
!!                               # Run last command
!$                               # Last argument of previous command
Ctrl+R                           # Reverse search through history

# Tab completion
cd /us<TAB>                      # Auto-completes to /usr/
ls /etc/ap<TAB><TAB>            # Shows all matches

# Keyboard shortcuts
Ctrl+A                           # Go to beginning of line
Ctrl+E                           # Go to end of line
Ctrl+U                           # Delete from cursor to beginning
Ctrl+K                           # Delete from cursor to end
Ctrl+L                           # Clear screen (same as 'clear')
Ctrl+C                           # Cancel current command
Ctrl+D                           # Logout/exit
Ctrl+Z                           # Suspend current process

# Command chaining
command1 ; command2              # Run command2 after command1
command1 && command2             # Run command2 only if command1 succeeds
command1 || command2             # Run command2 only if command1 fails
command1 | command2              # Pipe output of command1 to command2

# Input/Output redirection
command > file                   # Redirect output to file (overwrite)
command >> file                  # Redirect output to file (append)
command < file                   # Use file as input
command 2> error.log             # Redirect errors to file
command &> all.log               # Redirect both output and errors
command > /dev/null 2>&1         # Discard all output
```

**Exercise 1.6:**
1. Search your history for all `ls` commands you've used
2. Use tab completion to navigate to `/usr/share/applications`
3. Create a chain that creates a directory, navigates into it, and creates a file
4. Redirect the output of `ls -la /etc` to a file called `etc_contents.txt`

**Challenge 1.6:** Create a single command that lists all files in your home directory, sorts them by size, saves the output to a file, and then displays the first 10 lines.

---

#### Day 7: Finding Files and Content

```bash
# Finding files
find /path -name "filename"      # Find by name
find ~ -name "*.txt"             # Find all .txt files in home
find / -name "file" 2>/dev/null  # Find, suppress errors
find . -type f                   # Find files only
find . -type d                   # Find directories only
find . -size +10M                # Find files larger than 10MB
find . -mtime -7                 # Modified in last 7 days
find . -empty                    # Find empty files/directories
find . -name "*.log" -delete     # Find and delete

# Locate (faster, uses database)
sudo updatedb                    # Update file database
locate filename                  # Quick search using database
locate -i filename               # Case-insensitive search

# Which/whereis
which python3                    # Location of command
whereis python3                  # Binary, source, and man page locations
type python3                     # Show command type

# Searching inside files
grep "pattern" file              # Search for pattern in file
grep -r "pattern" directory      # Recursive search
grep -i "pattern" file           # Case-insensitive
grep -v "pattern" file           # Invert match (show non-matching)
grep -n "pattern" file           # Show line numbers
grep -c "pattern" file           # Count matches
grep -l "pattern" *              # Show only filenames with matches
grep -A 3 "pattern" file         # Show 3 lines after match
grep -B 3 "pattern" file         # Show 3 lines before match
```

**Exercise 1.7:**
1. Find all `.conf` files in `/etc`
2. Search for the word "user" in `/etc/passwd`
3. Find all files in your home directory modified in the last 2 days
4. Find the location of the `bash` command

**Challenge 1.7:** Find all files in `/var/log` that contain the word "error" (case-insensitive), count how many files match, and save the list of matching files to `error_logs.txt`.

---

## Module 2: File System & Permissions

### Week 3: Understanding Linux File System

#### Day 8: File System Hierarchy

```bash
# Understanding the Linux directory structure
ls /                             # Root directory contents

# Key directories explained:
/bin                            # Essential command binaries
/boot                           # Boot loader files
/dev                            # Device files
/etc                            # System configuration files
/home                           # User home directories
/lib                            # Shared libraries
/media                          # Removable media mount points
/mnt                            # Temporary mount points
/opt                            # Optional software
/proc                           # Process information (virtual)
/root                           # Root user home directory
/sbin                           # System binaries
/srv                            # Service data
/tmp                            # Temporary files
/usr                            # User programs
/var                            # Variable data (logs, etc.)

# Exploring
ls -la /etc                     # Configuration files
ls -la /var/log                 # Log files
ls -la /usr/bin                 # User commands
cat /etc/os-release             # OS information
cat /proc/cpuinfo               # CPU information (virtual file)
cat /proc/meminfo               # Memory information
```

**Exercise 2.1:**
1. List the contents of `/bin`, `/sbin`, and `/usr/bin`
2. View your OS information from `/etc/os-release`
3. Check `/var/log` and identify 5 different log files
4. Explore `/proc` and view information about your CPU and memory

**Challenge 2.1:** Create a map/diagram of the top-level directories in Linux and write a one-line description of each in a text file.

---

#### Day 9: File Permissions - Part 1

```bash
# Understanding permissions
ls -l file.txt
# Output: -rw-r--r-- 1 user group 1234 Oct  1 12:00 file.txt
# Explained:
# - : file type (- = file, d = directory, l = link)
# rw- : owner permissions (read, write, no execute)
# r-- : group permissions (read only)
# r-- : others permissions (read only)
# user : owner name
# group : group name

# Permission values:
# r (read) = 4
# w (write) = 2
# x (execute) = 1
# - (no permission) = 0

# Changing permissions with chmod
chmod 755 file.sh                # rwxr-xr-x (owner: all, group: rx, others: rx)
chmod 644 file.txt               # rw-r--r-- (owner: rw, group: r, others: r)
chmod 600 private.txt            # rw------- (owner only)
chmod 777 file                   # rwxrwxrwx (all permissions - dangerous!)

# Symbolic mode
chmod u+x file.sh                # Add execute for owner (user)
chmod g+w file.txt               # Add write for group
chmod o-r file.txt               # Remove read for others
chmod a+x script.sh              # Add execute for all
chmod u=rw,g=r,o=r file.txt     # Set specific permissions

# Changing ownership
sudo chown newowner file.txt     # Change owner
sudo chown newowner:newgroup file.txt  # Change owner and group
sudo chgrp newgroup file.txt     # Change group only
sudo chown -R user:group dir/    # Recursive ownership change
```

**Exercise 2.2:**
1. Create a file and check its permissions
2. Make the file readable and writable only by you
3. Create a script file and make it executable
4. Create a directory and set permissions to 755

**Challenge 2.2:** Create three files: `public.txt` (everyone can read), `team.txt` (your group can read and write), and `private.txt` (only you can read and write). Verify with `ls -l`.

---

#### Day 10: File Permissions - Part 2

```bash
# Special permissions
chmod u+s file                   # SUID (Set User ID) - run as owner
chmod g+s directory              # SGID (Set Group ID) - new files inherit group
chmod +t directory               # Sticky bit - only owner can delete files

# Examples with numbers
chmod 4755 file                  # SUID + rwxr-xr-x
chmod 2755 directory             # SGID + rwxr-xr-x
chmod 1777 /tmp                  # Sticky bit + rwxrwxrwx

# Viewing special permissions
ls -l /usr/bin/passwd            # Notice the 's' in permissions
ls -ld /tmp                      # Notice the 't' in permissions

# Default permissions with umask
umask                            # View current umask
umask 022                        # Set umask (files: 644, dirs: 755)
umask 077                        # Restrictive (files: 600, dirs: 700)

# File attributes
lsattr file.txt                  # List attributes
sudo chattr +i file.txt          # Make immutable (can't be modified/deleted)
sudo chattr -i file.txt          # Remove immutable
sudo chattr +a file.log          # Append only
```

**Exercise 2.3:**
1. Check the umask on your system
2. Find three files with special permissions in `/usr/bin`
3. Create a directory with sticky bit set
4. Experiment with making a file immutable

**Challenge 2.3:** Create a shared directory where multiple users can create files, but only the file owner can delete them (use SGID and sticky bit).

---

#### Day 11: Links and File Types

```bash
# Hard links
ln source.txt hardlink.txt       # Create hard link
ls -li source.txt hardlink.txt   # Same inode number

# Symbolic (soft) links
ln -s /path/to/source link       # Create symbolic link
ln -s /usr/bin/python3 python    # Link to executable
ls -l link                       # Shows -> pointing to target
readlink link                    # Show target of link
readlink -f link                 # Show absolute path

# Understanding links
# Hard link: Another name for same file (same inode)
# Soft link: Pointer to filename (different inode)

# File types
file filename                    # Identify file type
file *                          # Check all files in directory
file -b filename                # Brief output

# Symbolic link management
find . -type l                  # Find all symbolic links
find . -type l -ls              # Detailed list of symlinks
find -L . -type l               # Find broken symlinks
unlink linkname                 # Remove symbolic link
```

**Exercise 2.4:**
1. Create a file and make a hard link to it
2. Create a symbolic link to a directory
3. Modify the original file and verify both links show the change
4. Use the `file` command on 10 different files

**Challenge 2.4:** Create a symbolic link to a file, then move the original file to a different location. What happens to the link? Fix it by creating a proper link.

---

## Module 3: Text Processing & Shell Scripting

### Week 4: Text Processing Tools

#### Day 12: Essential Text Tools

```bash
# Counting
wc file.txt                      # Lines, words, characters
wc -l file.txt                   # Count lines only
wc -w file.txt                   # Count words only
wc -c file.txt                   # Count bytes

# Sorting
sort file.txt                    # Sort alphabetically
sort -r file.txt                 # Reverse sort
sort -n numbers.txt              # Numerical sort
sort -u file.txt                 # Sort and remove duplicates
sort -k2 file.txt                # Sort by second column

# Unique lines
uniq file.txt                    # Remove adjacent duplicates (must sort first!)
sort file.txt | uniq             # Remove all duplicates
uniq -c file.txt                 # Count occurrences
uniq -d file.txt                 # Show only duplicates

# Cutting columns
cut -d: -f1 /etc/passwd          # Extract first field (delimiter: :)
cut -d: -f1,3 /etc/passwd        # Extract fields 1 and 3
cut -c1-10 file.txt              # Extract characters 1-10

# Pasting files
paste file1.txt file2.txt        # Merge files side by side
paste -d, file1.txt file2.txt    # Use comma as delimiter

# Translating characters
tr 'a-z' 'A-Z' < file.txt        # Convert to uppercase
tr -d ' ' < file.txt             # Delete spaces
tr -s ' ' < file.txt             # Squeeze repeated spaces
```

**Exercise 3.1:**
1. Count lines in `/etc/passwd`
2. Sort `/etc/passwd` by username
3. Extract only usernames from `/etc/passwd`
4. Count unique shells in `/etc/passwd`

**Challenge 3.1:** Find the 10 most common words in a text file (create one with repeated words). Hint: Combine multiple commands with pipes.

---

#### Day 13: Advanced Text Processing

```bash
# sed (Stream Editor)
sed 's/old/new/' file.txt        # Replace first occurrence per line
sed 's/old/new/g' file.txt       # Replace all occurrences
sed 's/old/new/gi' file.txt      # Case-insensitive replacement
sed -i 's/old/new/g' file.txt    # Edit file in-place
sed -n '5,10p' file.txt          # Print lines 5 to 10
sed '5d' file.txt                # Delete line 5
sed '/pattern/d' file.txt        # Delete lines matching pattern
sed 's/^/PREFIX: /' file.txt     # Add prefix to each line
sed 's/$/SUFFIX/' file.txt       # Add suffix to each line

# awk (Pattern Processing Language)
awk '{print $1}' file.txt        # Print first column
awk '{print $1, $3}' file.txt    # Print first and third columns
awk -F: '{print $1}' /etc/passwd # Use : as field separator
awk '$3 > 100' file.txt          # Print lines where 3rd field > 100
awk '{sum+=$1} END {print sum}' file.txt  # Sum first column
awk 'NR==5' file.txt             # Print 5th line
awk 'length > 80' file.txt       # Print lines longer than 80 chars
awk '{print NR, $0}' file.txt    # Add line numbers

# Advanced awk
awk 'BEGIN {print "START"} {print} END {print "END"}' file.txt
awk '{print $1, $(NF)}' file.txt # Print first and last column
awk -F: '$3 >= 1000 {print $1}' /etc/passwd  # Users with UID >= 1000

# Column formatting
column -t file.txt               # Format into columns
column -t -s: /etc/passwd        # Format : delimited file
```

**Exercise 3.2:**
1. Replace all occurrences of "error" with "ERROR" in a log file
2. Extract only the home directories from `/etc/passwd`
3. Calculate the sum of numbers in a file (one number per line)
4. Print lines 15-25 from a file

**Challenge 3.2:** Create a CSV file with names and scores. Use awk to calculate the average score and find the person with the highest score.

---

#### Day 14: Regular Expressions

```bash
# Basic regex patterns
grep 'pattern' file              # Literal match
grep '^pattern' file             # Line starts with pattern
grep 'pattern$' file             # Line ends with pattern
grep '^$' file                   # Empty lines
grep '.' file                    # Any single character
grep 'a*' file                   # Zero or more 'a'
grep 'a\+' file                  # One or more 'a'
grep 'a\?' file                  # Zero or one 'a'

# Character classes
grep '[abc]' file                # Match a, b, or c
grep '[^abc]' file               # Match anything except a, b, c
grep '[0-9]' file                # Match any digit
grep '[a-z]' file                # Match lowercase letter
grep '[A-Z]' file                # Match uppercase letter

# Extended regex (grep -E or egrep)
grep -E 'pattern1|pattern2' file # OR operation
grep -E 'ab+c' file              # One or more b
grep -E 'ab?c' file              # Zero or one b
grep -E 'ab{3}c' file            # Exactly 3 b's
grep -E 'ab{2,5}c' file          # 2 to 5 b's
grep -E '(abc)+' file            # One or more abc groups

# Practical examples
grep -E '^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' file  # IP addresses
grep -E '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b' file  # Email
grep -E '^[0-9]{3}-[0-9]{3}-[0-9]{4}$' file  # Phone: 123-456-7890

# Perl-compatible regex (grep -P)
grep -P '\d+' file               # Digits
grep -P '\w+' file               # Word characters
grep -P '\s+' file               # Whitespace
```

**Exercise 3.3:**
1. Find all lines in `/etc/passwd` that start with 'root'
2. Find all email addresses in a file
3. Find all IP addresses in a log file
4. Find lines that contain exactly 3 digits in a row

**Challenge 3.3:** Create a file with various phone number formats. Write a regex that matches all valid formats and another that identifies invalid formats.

---

### Week 5: Shell Scripting

#### Day 15: Bash Scripting Basics

```bash
# Create your first script
#!/bin/bash
# This is a comment

echo "Hello, World!"
echo "Current date: $(date)"
echo "Current user: $USER"
echo "Home directory: $HOME"
echo "Current directory: $PWD"

# Make script executable
chmod +x script.sh
./script.sh

# Variables
#!/bin/bash
NAME="Linux"
AGE=30
echo "Hello, $NAME"
echo "Age: $AGE"

# Read user input
#!/bin/bash
echo "What is your name?"
read NAME
echo "Hello, $NAME!"

# Command substitution
CURRENT_DATE=$(date +%Y-%m-%d)
FILE_COUNT=$(ls | wc -l)
echo "Today is $CURRENT_DATE"
echo "Files in directory: $FILE_COUNT"

# Script arguments
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
```

**Exercise 3.4:**
1. Create a script that prints your system information (hostname, kernel, date)
2. Create a script that takes a filename as argument and prints its line count
3. Create a script that asks for your name and age, then prints a greeting
4. Create a backup script that copies a file with a timestamp in the name

**Challenge 3.4:** Create a script that takes a directory path as argument and prints: number of files, number of directories, largest file, and total size.

---

#### Day 16: Conditionals and Loops

```bash
# If statements
#!/bin/bash
if [ "$1" == "hello" ]; then
    echo "Hi there!"
elif [ "$1" == "bye" ]; then
    echo "Goodbye!"
else
    echo "Unknown command"
fi

# Numeric comparisons
if [ $AGE -gt 18 ]; then
    echo "Adult"
fi
# -eq (equal), -ne (not equal), -gt (greater), -lt (less)
# -ge (greater or equal), -le (less or equal)

# File tests
if [ -f filename ]; then
    echo "File exists"
fi
# -f (file exists), -d (directory exists), -r (readable)
# -w (writable), -x (executable), -s (not empty)

# Logical operators
if [ $AGE -gt 18 ] && [ $AGE -lt 65 ]; then
    echo "Working age"
fi

# For loops
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

for file in *.txt; do
    echo "Processing $file"
done

for i in {1..10}; do
    echo "Count: $i"
done

# C-style for loop
for ((i=1; i<=10; i++)); do
    echo "Number: $i"
done

# While loop
COUNT=1
while [ $COUNT -le 5 ]; do
    echo "Count: $COUNT"
    COUNT=$((COUNT + 1))
done

# Until loop (opposite of while)
COUNT=1
until [ $COUNT -gt 5 ]; do
    echo "Count: $COUNT"
    COUNT=$((COUNT + 1))
done
```

**Exercise 3.5:**
1. Create a script that checks if a file exists before reading it
2. Create a script that loops through numbers 1-20 and prints "even" or "odd"
3. Create a script that counts down from 10 to 1
4. Create a script that processes all `.log` files in a directory

**Challenge 3.5:** Create a number guessing game script where the computer picks a random number (1-100) and the user has to guess it, with "higher" or "lower" hints.

---

#### Day 17: Functions and Advanced Scripting

```bash
# Functions
#!/bin/bash
function greet() {
    echo "Hello, $1!"
}

greet "Alice"
greet "Bob"

# Function with return value
function add() {
    local RESULT=$(($1 + $2))
    echo $RESULT
}

SUM=$(add 5 3)
echo "Sum is: $SUM"

# Arrays
#!/bin/bash
FRUITS=("Apple" "Banana" "Cherry")
echo ${FRUITS[0]}               # First element
echo ${FRUITS[@]}               # All elements
echo ${#FRUITS[@]}              # Array length

for FRUIT in "${FRUITS[@]}"; do
    echo "Fruit: $FRUIT"
done

# Case statements
#!/bin/bash
case "$1" in
    start)
        echo "Starting service..."
        ;;
    stop)
        echo "Stopping service..."
        ;;
    restart)
        echo "Restarting service..."
        ;;
    *)
        echo "Usage: $0 {start|stop|restart}"
        exit 1
        ;;
esac

# Exit codes
#!/bin/bash
command
if [ $? -eq 0 ]; then
    echo "Success!"
else
    echo "Failed!"
    exit 1
fi

# Error handling
#!/bin/bash
set -e                          # Exit on error
set -u                          # Exit on undefined variable
set -o pipefail                 # Exit if any command in pipe fails

# Debugging
bash -x script.sh               # Run with debug output
set -x                          # Enable debugging in script
set +x                          # Disable debugging
```

**Exercise 3.6:**
1. Create a script with a function that checks if a directory exists, creates it if not
2. Create a menu-driven script using case statements (options: list files, show date, show disk usage, exit)
3. Create a script with an array of server names that pings each one
4. Create a script that validates user input (checks if file/directory exists)

**Challenge 3.6:** Create a log analyzer script that:
- Takes a log file as argument
- Counts ERROR, WARNING, and INFO messages
- Shows the 5 most common error messages
- Saves a summary report to a new file

---

## Module 4: User & Process Management

### Week 6: Users, Groups, and Processes

#### Day 18: User Management

```bash
# User information
whoami                          # Current username
id                              # User ID and groups
id username                     # Info about specific user
who                             # Who is logged in
w                               # Detailed who with activity
last                            # Login history
lastlog                         # Last login for all users

# Creating users (requires sudo)
sudo adduser newuser            # Interactive user creation (Debian/Ubuntu)
sudo useradd newuser            # Non-interactive (may need more options)
sudo useradd -m -s /bin/bash newuser  # Create with home dir and shell
sudo passwd newuser             # Set password

# Modifying users
sudo usermod -aG groupname user # Add user to group
sudo usermod -s /bin/zsh user   # Change shell
sudo usermod -l newname oldname # Rename user
sudo usermod -L username        # Lock account
sudo usermod -U username        # Unlock account

# Deleting users
sudo deluser username           # Delete user (Ubuntu/Debian)
sudo deluser --remove-home username  # Delete with home directory
sudo userdel username           # Delete user (generic)
sudo userdel -r username        # Delete user and home directory

# User files
cat /etc/passwd                 # User accounts
cat /etc/shadow                 # Encrypted passwords (requires sudo)
cat /etc/group                  # Groups
cat /etc/gshadow                # Secure group info

# Switching users
su username                     # Switch user
su -                            # Switch to root with root environment
su - username                   # Switch with user environment
sudo -i                         # Interactive root shell
sudo -u username command        # Run command as user
exit                            # Exit user session
```

**Exercise 4.1:**
1. Create a new user called "testuser"
2. Set a password for testuser
3. Check the entry in `/etc/passwd` for testuser
4. Switch to testuser and verify with `whoami`
5. Delete testuser when done

**Challenge 4.1:** Create three users (dev1, dev2, dev3), create a group called "developers", add all three users to this group, and verify the group membership.

---

#### Day 19: Group Management and Sudo

```bash
# Group commands
groups                          # Show your groups
groups username                 # Show user's groups
sudo groupadd newgroup          # Create group
sudo groupdel groupname         # Delete group
sudo gpasswd -a user group      # Add user to group
sudo gpasswd -d user group      # Remove user from group
newgrp groupname                # Switch to group temporarily

# Sudo configuration
sudo visudo                     # Edit sudoers file safely
# File: /etc/sudoers

# Sudoers examples:
# username ALL=(ALL:ALL) ALL  # User has full sudo access
# %groupname ALL=(ALL:ALL) ALL # Group has full sudo access
# username ALL=(ALL) NOPASSWD: ALL # No password required

# Sudo usage
sudo command                    # Run command as root
sudo -u username command        # Run command as different user
sudo -l                         # List sudo privileges
sudo -k                         # Invalidate sudo timestamp
sudo !!                         # Run last command with sudo

# Checking sudo logs
sudo cat /var/log/auth.log | grep sudo  # Ubuntu/Debian
sudo cat /var/log/secure | grep sudo    # RHEL/CentOS
```

**Exercise 4.2:**
1. Create a group called "admins"
2. Add your user to the admins group
3. Check your group membership
4. View your sudo privileges
5. Run a command that requires root without sudo, then with sudo

**Challenge 4.2:** Create a user that can only run specific commands with sudo (e.g., can restart apache but nothing else). Test that it works.

---

#### Day 20: Process Management

```bash
# Viewing processes
ps                              # Current shell processes
ps aux                          # All processes (BSD style)
ps -ef                          # All processes (Unix style)
ps -u username                  # Processes for specific user
pstree                          # Process tree
top                             # Interactive process viewer
htop                            # Better interactive viewer (install first)

# Process information
ps aux | grep processname       # Find specific process
pgrep processname               # Get PID by name
pidof processname               # Get PID by name
ps -p PID                       # Info about specific PID

# Background and foreground
command &                       # Run in background
jobs                            # List background jobs
fg %1                           # Bring job 1 to foreground
bg %1                           # Continue job 1 in background
Ctrl+Z                          # Suspend current process
Ctrl+C                          # Terminate current process

# Process priority (nice values: -20 to 19, lower = higher priority)
nice -n 10 command              # Start with nice value 10
renice 10 -p PID                # Change nice value of running process
renice -n 10 -u username        # Renice all user's processes

# Killing processes
kill PID                        # Terminate process (SIGTERM)
kill -9 PID                     # Force kill (SIGKILL)
kill -15 PID                    # Graceful termination (SIGTERM)
kill -HUP PID                   # Hangup (often reloads config)
killall processname             # Kill all with name
pkill processname               # Kill by name pattern
pkill -u username               # Kill all user processes

# Process monitoring
watch -n 2 'ps aux'             # Run ps every 2 seconds
top -u username                 # Monitor specific user
lsof -p PID                     # Files opened by process
lsof /path/to/file              # Which process is using file
```

**Exercise 4.3:**
1. List all running processes on your system
2. Find the PID of your current bash shell
3. Run a process in the background (try: `sleep 60 &`)
4. List your background jobs and bring one to foreground
5. Kill the sleep process

**Challenge 4.3:** Create a script that runs in the background, writes to a log file every 5 seconds, then find its PID and kill it gracefully.

---

#### Day 21: System Monitoring

```bash
# CPU and memory
top                             # Real-time system monitor
htop                            # Enhanced system monitor
uptime                          # Load averages
mpstat                          # CPU usage (may need to install sysstat)
vmstat 2                        # Virtual memory stats every 2 seconds
free -h                         # Memory usage
watch -n 1 free -h              # Monitor memory continuously

# Disk I/O
iostat                          # I/O statistics (install sysstat)
iotop                           # I/O monitor by process (needs sudo)
df -h                           # Disk space usage
df -i                           # Inode usage
du -sh /path                    # Directory size
du -sh * | sort -h              # Sort directories by size

# Network monitoring
netstat -tuln                   # Active network connections
ss -tuln                        # Socket statistics (modern netstat)
iftop                           # Network bandwidth monitor (install first)
nload                           # Network load monitor
nethogs                         # Network usage by process

# System logs
dmesg                           # Kernel messages
dmesg -T                        # With human-readable timestamps
journalctl                      # Systemd journal
journalctl -f                   # Follow journal
journalctl -u servicename       # Logs for specific service
journalctl --since "1 hour ago" # Recent logs
tail -f /var/log/syslog         # Follow system log

# Performance analysis
sar                             # System activity report (install sysstat)
sar -u 2 5                      # CPU usage, 2 sec intervals, 5 times
sar -r                          # Memory usage
sar -n DEV                      # Network statistics
```

**Exercise 4.4:**
1. Check your system's load average
2. Monitor CPU usage in real-time
3. Find the process using the most memory
4. Check disk I/O statistics
5. View the last 50 lines of system log

**Challenge 4.4:** Create a monitoring script that runs every 10 seconds and logs: timestamp, CPU load, memory usage, and disk usage to a file. Let it run for 5 minutes, then analyze the log.

---

## Module 5: Networking Essentials

### Week 7: Linux Networking

#### Day 22: Network Configuration

```bash
# Network interfaces
ip addr show                    # Show all IP addresses
ip a                            # Short form
ifconfig                        # Legacy command (may need net-tools)
ip link show                    # Show all network interfaces
ip link set eth0 up             # Bring interface up
ip link set eth0 down           # Bring interface down

# IP address management
sudo ip addr add 192.168.1.100/24 dev eth0  # Add IP address
sudo ip addr del 192.168.1.100/24 dev eth0  # Remove IP address

# Routing
ip route show                   # Show routing table
route -n                        # Legacy routing table
sudo ip route add default via 192.168.1.1  # Add default gateway
sudo ip route del default       # Remove default route

# DNS configuration
cat /etc/resolv.conf            # DNS servers
cat /etc/hosts                  # Local hostname resolution
cat /etc/hostname               # System hostname
hostname                        # Current hostname
sudo hostnamectl set-hostname newhostname  # Change hostname

# Network configuration files (Ubuntu)
cat /etc/netplan/*.yaml         # Netplan config (Ubuntu 18.04+)
sudo netplan apply              # Apply netplan changes
cat /etc/network/interfaces     # Legacy network config

# Testing connectivity
ping google.com                 # Test connection (Ctrl+C to stop)
ping -c 4 google.com            # Send 4 packets
ping6 google.com                # IPv6 ping
traceroute google.com           # Trace route to destination
tracepath google.com            # Alternative trace
mtr google.com                  # Combined ping and traceroute
```

**Exercise 5.1:**
1. Display your IP address and network interface
2. Show your routing table
3. Ping your router/gateway
4. Trace the route to google.com
5. Check your DNS configuration

**Challenge 5.1:** Document your complete network configuration: IP address, subnet mask, gateway, DNS servers, and hostname. Save this to a file for reference.

---

#### Day 23: Network Tools and Diagnostics

```bash
# Port scanning and connection testing
nc -zv hostname 80              # Test if port 80 is open (netcat)
telnet hostname 80              # Test connection to port
nmap localhost                  # Scan localhost ports (install nmap)
nmap -p 1-1000 192.168.1.1      # Scan ports 1-1000
nmap -sV 192.168.1.1            # Service/version detection

# DNS queries
nslookup google.com             # DNS lookup
dig google.com                  # Detailed DNS query
dig +short google.com           # Short answer
dig @8.8.8.8 google.com         # Query specific DNS server
host google.com                 # Simple DNS lookup

# Netstat and socket statistics
netstat -tuln                   # TCP/UDP listening ports
netstat -tunp                   # With process names (needs sudo for all)
ss -tuln                        # Modern replacement for netstat
ss -tunp                        # Socket statistics with processes
lsof -i :80                     # What's using port 80
lsof -i tcp                     # All TCP connections
sudo netstat -anp | grep LISTEN # All listening ports

# Downloading files
wget https://example.com/file   # Download file
wget -O newname.txt url         # Save with different name
curl https://example.com        # Display content
curl -O https://example.com/file # Download file
curl -I https://example.com     # Get headers only
curl -L url                     # Follow redirects

# Bandwidth and speed
speedtest-cli                   # Internet speed test (install first)
iperf3 -s                       # Start iperf server
iperf3 -c serverip              # Test bandwidth to server

# Network statistics
netstat -s                      # Network statistics
netstat -i                      # Interface statistics
ip -s link                      # Interface statistics (modern)
```

**Exercise 5.2:**
1. Look up the IP address of github.com using multiple tools
2. Check what ports are listening on your system
3. Download a file using wget
4. Test if port 22 (SSH) is open on your Raspberry Pi from your laptop
5. Check network statistics on your primary interface

**Challenge 5.2:** Create a network diagnostic script that checks: internet connectivity (ping), DNS resolution (dig), and lists all listening ports. Output should be color-coded (green=ok, red=problem).

---

#### Day 24: SSH and Remote Access

```bash
# SSH basics
ssh username@hostname           # Connect to remote system
ssh username@192.168.1.100      # Connect using IP
ssh -p 2222 user@host           # Connect to non-standard port
exit                            # Disconnect

# SSH key authentication
ssh-keygen                      # Generate SSH key pair
ssh-keygen -t rsa -b 4096       # RSA 4096-bit key
ssh-keygen -t ed25519           # Ed25519 key (modern, recommended)
ssh-copy-id user@host           # Copy public key to server
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host  # Specify key

# SSH configuration
cat ~/.ssh/config               # Client configuration
# Example config:
# Host myserver
#   HostName 192.168.1.100
#   User myusername
#   Port 22
#   IdentityFile ~/.ssh/id_rsa

# Then connect with: ssh myserver

# File transfer with SCP
scp file.txt user@host:/path/   # Copy file to remote
scp user@host:/path/file.txt .  # Copy file from remote
scp -r directory user@host:/path/  # Copy directory
scp -P 2222 file user@host:/path/  # Use specific port

# SFTP (Secure FTP)
sftp user@host                  # Start SFTP session
# Commands in SFTP:
# put file.txt                  # Upload file
# get file.txt                  # Download file
# ls                            # List remote directory
# lls                           # List local directory
# cd                            # Change remote directory
# lcd                           # Change local directory
# exit                          # Quit SFTP

# Rsync (efficient file synchronization)
rsync -avz source/ dest/        # Sync directories
rsync -avz file user@host:/path/ # Sync to remote
rsync -avz user@host:/path/ .   # Sync from remote
rsync -avz --delete source/ dest/ # Delete files not in source
rsync -avz -e "ssh -p 2222" source/ user@host:/path/ # Custom SSH port

# SSH tunneling
ssh -L 8080:localhost:80 user@host  # Local port forwarding
ssh -R 8080:localhost:80 user@host  # Remote port forwarding
ssh -D 1080 user@host           # Dynamic port forwarding (SOCKS proxy)

# SSH in scripts (non-interactive)
ssh -o StrictHostKeyChecking=no user@host "command"  # Skip host key check
ssh user@host "df -h"           # Run single command
ssh user@host << 'EOF'
command1
command2
EOF
```

**Exercise 5.3:**
1. SSH into your Raspberry Pi from your Ubuntu Desktop
2. Generate an SSH key pair
3. Copy your SSH key to your Raspberry Pi
4. SSH to your Raspberry Pi without password
5. Transfer a file to your Raspberry Pi using scp

**Challenge 5.3:** Create an SSH config file with an alias for your Raspberry Pi. Set up key-based authentication so you can SSH without password. Then create a script that backs up a directory from your Pi to your laptop daily using rsync over SSH.

---

#### Day 25: Firewall Basics

```bash
# UFW (Uncomplicated Firewall) - Ubuntu's firewall
sudo ufw status                 # Check firewall status
sudo ufw enable                 # Enable firewall
sudo ufw disable                # Disable firewall

# UFW rules
sudo ufw allow 22               # Allow SSH
sudo ufw allow 80/tcp           # Allow HTTP
sudo ufw allow 443/tcp          # Allow HTTPS
sudo ufw allow from 192.168.1.0/24  # Allow from subnet
sudo ufw deny 23                # Deny telnet
sudo ufw delete allow 80        # Delete rule

# UFW application profiles
sudo ufw app list               # List available profiles
sudo ufw allow 'Apache Full'    # Allow Apache (80 and 443)
sudo ufw allow 'OpenSSH'        # Allow SSH

# Advanced UFW
sudo ufw allow from 192.168.1.100 to any port 22  # Specific IP to port
sudo ufw allow proto tcp from any to any port 80  # Specify protocol
sudo ufw logging on             # Enable logging
sudo ufw status numbered        # Show rules with numbers
sudo ufw delete 2               # Delete rule by number

# iptables (lower-level firewall)
sudo iptables -L                # List rules
sudo iptables -L -v -n          # Verbose listing
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # Allow SSH
sudo iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT  # Allow subnet
sudo iptables -A INPUT -j DROP  # Drop all other input

# Save iptables rules
sudo iptables-save > /etc/iptables/rules.v4  # Save rules
sudo iptables-restore < /etc/iptables/rules.v4  # Restore rules

# Network connection monitoring
sudo tcpdump -i eth0            # Capture packets on eth0
sudo tcpdump -i eth0 port 80    # Capture HTTP traffic
sudo tcpdump -i any -c 100      # Capture 100 packets on any interface
sudo tcpdump -w capture.pcap    # Save to file (analyze with wireshark)
```

**Exercise 5.4:**
1. Check if UFW is enabled on your systems
2. Allow SSH on your Raspberry Pi
3. Check the firewall status and rules
4. Set up UFW to allow HTTP and HTTPS
5. Test that SSH still works after enabling firewall

**Challenge 5.4:** Configure UFW on your Raspberry Pi to:
- Allow SSH only from your laptop's IP
- Allow HTTP from anywhere
- Block all other incoming traffic
- Test and verify the configuration works

---

## Module 6: Package Management & Software

### Week 8: Software Management

#### Day 26: APT Package Manager

```bash
# APT basics (Ubuntu/Debian)
sudo apt update                 # Update package list
sudo apt upgrade                # Upgrade all packages
sudo apt full-upgrade           # Upgrade with dependency handling
sudo apt dist-upgrade           # Distribution upgrade (legacy command)

# Installing software
sudo apt install package        # Install package
sudo apt install package1 package2  # Install multiple
sudo apt install -y package     # Auto-yes to prompts
sudo apt reinstall package      # Reinstall package
sudo apt install ./package.deb  # Install local .deb file

# Removing software
sudo apt remove package         # Remove package
sudo apt purge package          # Remove package and configs
sudo apt autoremove             # Remove unused dependencies
sudo apt autoremove --purge     # Remove dependencies and configs

# Searching and information
apt search keyword              # Search for packages
apt show package                # Show package details
apt list --installed            # List installed packages
apt list --upgradable           # List upgradable packages
dpkg -l                         # List all installed packages
dpkg -L package                 # List files installed by package
dpkg -S /path/to/file           # Find package that owns file

# Repository management
cat /etc/apt/sources.list       # Main repository list
ls /etc/apt/sources.list.d/     # Additional repositories
sudo add-apt-repository ppa:user/repo  # Add PPA
sudo add-apt-repository --remove ppa:user/repo  # Remove PPA

# Package cache
sudo apt clean                  # Remove downloaded packages
sudo apt autoclean              # Remove outdated packages
du -sh /var/cache/apt/archives  # Check cache size

# Holding packages (prevent upgrade)
sudo apt-mark hold package      # Hold package at current version
sudo apt-mark unhold package    # Unhold package
apt-mark showhold               # Show held packages

# dpkg (low-level package manager)
sudo dpkg -i package.deb        # Install .deb package
sudo dpkg -r package            # Remove package
sudo dpkg --configure -a        # Configure unpacked packages
sudo dpkg-reconfigure package   # Reconfigure installed package
```

**Exercise 6.1:**
1. Update your package list
2. Search for a package (try "nginx")
3. Install htop if not already installed
4. Show details about the htop package
5. List all installed packages and count them

**Challenge 6.1:** Create a script that:
- Updates package lists
- Shows available upgrades
- Logs the output to a file with timestamp
- Emails or displays a summary (number of upgradable packages)

---

#### Day 27: Snap and Alternative Package Managers

```bash
# Snap packages
snap find keyword               # Search for snaps
sudo snap install package       # Install snap
sudo snap install --classic package  # Install with classic confinement
snap list                       # List installed snaps
sudo snap refresh               # Update all snaps
sudo snap refresh package       # Update specific snap
sudo snap remove package        # Remove snap
snap info package               # Package information

# Snap services
snap services                   # List snap services
sudo snap start package.service # Start service
sudo snap stop package.service  # Stop service
sudo snap restart package.service  # Restart service

# Flatpak (if installed)
flatpak search keyword          # Search flatpaks
sudo flatpak install package    # Install flatpak
flatpak list                    # List installed
flatpak update                  # Update all
flatpak uninstall package       # Remove flatpak

# AppImage
chmod +x application.AppImage   # Make executable
./application.AppImage          # Run AppImage

# Building from source
sudo apt install build-essential  # Install compiler tools
sudo apt build-dep package      # Install build dependencies
./configure                     # Configure source
make                            # Compile
sudo make install               # Install
sudo make uninstall             # Uninstall (if supported)

# Alternative: using checkinstall
sudo apt install checkinstall
sudo checkinstall               # Creates .deb during make install
```

**Exercise 6.2:**
1. Check if snap is installed
2. Search for and install a snap package
3. List your installed snaps
4. Check for snap updates
5. Remove the snap package you installed

**Challenge 6.2:** Compare the same application available as apt package, snap, and (if available) flatpak. Document: installation size, startup time, and any differences in functionality.

---

#### Day 28: System Updates and Maintenance

```bash
# System updates
sudo apt update && sudo apt upgrade -y  # Update and upgrade
sudo apt full-upgrade           # Complete upgrade
sudo do-release-upgrade         # Upgrade to new Ubuntu release

# Checking system version
lsb_release -a                  # Distribution information
cat /etc/os-release             # OS information
uname -r                        # Kernel version

# Kernel management
dpkg --list | grep linux-image  # List installed kernels
sudo apt autoremove             # Remove old kernels
uname -r                        # Current kernel
```

**Exercise 6.3:**
1. Check your current Ubuntu version
2. Update package lists and upgrade all packages
3. Remove unnecessary packages
4. Check your kernel version
5. List all installed kernels

**Challenge 6.3:** Create an automated update script that:
- Checks for updates daily
- Logs all operations
- Sends notification if reboot is required
- Auto-removes old packages
- Keeps last 7 days of logs

---

## Module 7: System Administration

### Week 9-10: Core System Administration

#### Day 29: System Services (systemd)

```bash
# Systemd basics
systemctl                       # List all units
systemctl list-units            # List active units
systemctl list-units --type=service  # List services only
systemctl list-unit-files       # List all unit files

# Service management
sudo systemctl start service    # Start service
sudo systemctl stop service     # Stop service
sudo systemctl restart service  # Restart service
sudo systemctl reload service   # Reload configuration
sudo systemctl status service   # Service status
systemctl is-active service     # Check if active
systemctl is-enabled service    # Check if enabled at boot

# Enable/disable services
sudo systemctl enable service   # Enable at boot
sudo systemctl disable service  # Disable at boot
sudo systemctl enable --now service  # Enable and start

# Common services
sudo systemctl status ssh       # SSH service
sudo systemctl status networking # Networking
sudo systemctl status cron      # Cron daemon

# System states
sudo systemctl reboot           # Reboot system
sudo systemctl poweroff         # Power off
sudo systemctl suspend          # Suspend
sudo systemctl hibernate        # Hibernate

# Creating custom service
sudo nano /etc/systemd/system/myservice.service
```

**Example service file:**
```ini
[Unit]
Description=My Custom Service
After=network.target

[Service]
Type=simple
User=username
WorkingDirectory=/home/username
ExecStart=/path/to/script.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
# After creating service:
sudo systemctl daemon-reload    # Reload systemd
sudo systemctl start myservice  # Start service
sudo systemctl enable myservice # Enable at boot

# Logs and debugging
journalctl                      # All journal logs
journalctl -u service           # Logs for specific service
journalctl -f                   # Follow logs (like tail -f)
journalctl -u service -f        # Follow service logs
journalctl --since "1 hour ago" # Recent logs
journalctl --since "2024-01-01" # Logs since date
journalctl -p err               # Only error priority
journalctl --disk-usage         # Journal disk usage
```

**Exercise 7.1:**
1. List all active services
2. Check the status of SSH service
3. Restart a service (like cron)
4. View logs for a specific service
5. Check if a service is enabled at boot

**Challenge 7.1:** Create a custom systemd service that:
- Runs a bash script every time the system boots
- Logs output to a file
- Restarts automatically if it fails
- Test it by rebooting

---

#### Day 30: Scheduled Tasks (Cron & At)

```bash
# Crontab (recurring tasks)
crontab -e                      # Edit your crontab
crontab -l                      # List your crontab
crontab -r                      # Remove your crontab
sudo crontab -e -u username     # Edit another user's crontab

# Crontab format:
# * * * * * command
# │ │ │ │ │
# │ │ │ │ └─── Day of week (0-7, both 0 and 7 are Sunday)
# │ │ │ └───── Month (1-12)
# │ │ └─────── Day of month (1-31)
# │ └───────── Hour (0-23)
# └─────────── Minute (0-59)

# Examples:
# */5 * * * * /path/to/script.sh        # Every 5 minutes
# 0 2 * * * /path/to/backup.sh          # Daily at 2 AM
# 0 0 * * 0 /path/to/weekly.sh          # Weekly on Sunday
# 0 0 1 * * /path/to/monthly.sh         # Monthly on 1st
# @reboot /path/to/startup.sh           # At boot
# @daily /path/to/daily.sh              # Daily
# @weekly /path/to/weekly.sh            # Weekly

# System cron directories
ls /etc/cron.daily/             # Daily jobs
ls /etc/cron.weekly/            # Weekly jobs
ls /etc/cron.monthly/           # Monthly jobs
ls /etc/cron.hourly/            # Hourly jobs
cat /etc/crontab                # System crontab

# At command (one-time tasks)
at now + 1 hour                 # Schedule task in 1 hour
at 10:00 PM                     # Schedule for 10 PM
at noon tomorrow                # Schedule for tomorrow noon
# Type commands, then Ctrl+D to save

atq                             # List scheduled at jobs
atrm job_number                 # Remove at job
batch                           # Run when system load is low
```

**Exercise 7.2:**
1. Create a cron job that runs every minute and writes timestamp to a file
2. Create a cron job that cleans /tmp every day at 3 AM
3. List all your cron jobs
4. Schedule a one-time task using 'at' command
5. View scheduled at jobs

**Challenge 7.2:** Create a backup system using cron:
- Full backup weekly (Sunday 2 AM)
- Incremental backup daily (2 AM)
- Log all operations
- Rotate old backups (keep last 4 weeks)
- Email/notify if backup fails

---

#### Day 31: Log Management

```bash
# System logs location
ls /var/log/                    # All logs
tail -f /var/log/syslog         # System log (Ubuntu/Debian)
tail -f /var/log/messages       # System log (RHEL/CentOS)
tail -f /var/log/auth.log       # Authentication log
tail -f /var/log/kern.log       # Kernel log
tail -f /var/log/boot.log       # Boot log

# Application logs
ls /var/log/apache2/            # Apache logs
ls /var/log/nginx/              # Nginx logs
tail -f /var/log/mysql/error.log # MySQL errors

# Journalctl (systemd logging)
journalctl                      # All logs
journalctl -n 50                # Last 50 entries
journalctl -f                   # Follow (real-time)
journalctl -u servicename       # Specific service
journalctl -p err               # Only errors
journalctl -p warning           # Warnings and above
journalctl --since "2024-01-01" # Since date
journalctl --since "1 hour ago" # Last hour
journalctl --until "2024-01-31" # Until date
journalctl -k                   # Kernel messages only
journalctl _PID=1234            # Specific process
journalctl --disk-usage         # Journal size
sudo journalctl --vacuum-size=100M  # Limit journal to 100MB
sudo journalctl --vacuum-time=2weeks  # Keep 2 weeks only

# Log rotation
cat /etc/logrotate.conf         # Main config
ls /etc/logrotate.d/            # Service-specific configs
sudo logrotate -f /etc/logrotate.conf  # Force rotation

# Example logrotate config:
# /var/log/myapp/*.log {
#     daily
#     rotate 7
#     compress
#     delaycompress
#     missingok
#     notifempty
# }

# Searching logs
grep -r "error" /var/log/       # Search for errors
grep -i "failed" /var/log/syslog # Case-insensitive search
zgrep "error" /var/log/syslog.*.gz  # Search compressed logs

# Real-time log monitoring
tail -f /var/log/syslog | grep --color error  # Highlight errors
multitail /var/log/syslog /var/log/auth.log   # Multiple logs (install first)
lnav /var/log/syslog            # Log navigator (install first)
```

**Exercise 7.3:**
1. View the last 100 lines of system log
2. Find all error messages from the last hour
3. Monitor authentication log in real-time
4. Check journal disk usage
5. Find all SSH login attempts

**Challenge 7.3:** Create a log analysis script that:
- Scans system logs for errors/warnings
- Counts occurrences by type
- Identifies failed login attempts
- Creates a daily report
- Sends alert if critical errors found

---

#### Day 32: Disk Management

```bash
# Viewing disks and partitions
lsblk                           # List block devices
lsblk -f                        # Show filesystem types
sudo fdisk -l                   # List all disks and partitions
df -h                           # Disk space usage
df -i                           # Inode usage
du -sh /path                    # Directory size
du -sh /* | sort -h             # Size of top-level directories
ncdu /                          # Interactive disk usage (install first)

# Disk usage analysis
sudo du -h /var | sort -h | tail -20  # 20 largest in /var
find / -type f -size +100M 2>/dev/null  # Files over 100MB
find / -type f -size +1G 2>/dev/null    # Files over 1GB

# Partitioning (CAREFUL - can destroy data!)
sudo fdisk /dev/sdb             # Partition disk (interactive)
# Commands in fdisk:
# m - help
# p - print partition table
# n - new partition
# d - delete partition
# w - write changes
# q - quit without saving

sudo parted /dev/sdb            # Alternative partitioning tool
sudo parted -l                  # List all partitions

# Formatting filesystems
sudo mkfs.ext4 /dev/sdb1        # Format as ext4
sudo mkfs.xfs /dev/sdb1         # Format as XFS
sudo mkfs.vfat /dev/sdb1        # Format as FAT32

# Mounting
sudo mount /dev/sdb1 /mnt       # Mount partition
mount | grep sdb1               # Check if mounted
sudo umount /mnt                # Unmount
sudo umount /dev/sdb1           # Unmount by device

# Permanent mounts (fstab)
cat /etc/fstab                  # View mount configuration
sudo blkid                      # Get UUID of partitions
# Add to /etc/fstab:
# UUID=xxx /mnt/data ext4 defaults 0 2

sudo mount -a                   # Mount all in fstab
findmnt                         # Show all mounts in tree format

# Checking filesystems
sudo fsck /dev/sdb1             # Check filesystem (unmount first!)
sudo fsck -y /dev/sdb1          # Auto-fix errors
sudo e2fsck -f /dev/sdb1        # Force check on ext4

# LVM (Logical Volume Management)
sudo pvdisplay                  # Physical volumes
sudo vgdisplay                  # Volume groups
sudo lvdisplay                  # Logical volumes
sudo pvcreate /dev/sdb          # Create physical volume
sudo vgcreate myvg /dev/sdb     # Create volume group
sudo lvcreate -L 10G -n mylv myvg  # Create logical volume
sudo mkfs.ext4 /dev/myvg/mylv   # Format LV

# RAID information
cat /proc/mdstat                # RAID status
sudo mdadm --detail /dev/md0    # RAID array details

# SMART monitoring (disk health)
sudo smartctl -a /dev/sda       # Disk health (install smartmontools)
sudo smartctl -H /dev/sda       # Health summary
```

**Exercise 7.4:**
1. List all block devices on your system
2. Check disk space usage
3. Find the largest files in /var
4. Check inode usage
5. View your /etc/fstab file

**Challenge 7.4:** Set up a USB drive:
- Create a partition
- Format it as ext4
- Mount it
- Add to fstab for automatic mounting
- Test by rebooting
- Safely unmount and remove

---

#### Day 33: Backup and Recovery

```bash
# tar archives
tar -czf backup.tar.gz /path    # Create compressed archive
tar -czf backup-$(date +%Y%m%d).tar.gz /path  # With date
tar -xzf backup.tar.gz          # Extract archive
tar -xzf backup.tar.gz -C /destination  # Extract to directory
tar -tzf backup.tar.gz          # List contents
tar -xzf backup.tar.gz file.txt # Extract specific file

# tar options:
# -c create
# -x extract
# -t list
# -z gzip compression
# -j bzip2 compression
# -J xz compression
# -v verbose
# -f file

# rsync backups
rsync -av source/ destination/  # Archive mode, verbose
rsync -avz source/ destination/ # With compression
rsync -av --delete source/ dest/  # Delete files not in source
rsync -avz --exclude='*.log' source/ dest/  # Exclude pattern
rsync -av --progress source/ dest/  # Show progress
rsync -av --dry-run source/ dest/   # Test run

# rsync over SSH
rsync -avz -e ssh source/ user@host:/path/
rsync -avz --delete -e ssh source/ user@host:/backup/

# Incremental backups with rsync
rsync -av --link-dest=/backup/last /source/ /backup/new/

# dd (disk cloning)
sudo dd if=/dev/sda of=/dev/sdb bs=64K status=progress  # Clone disk
sudo dd if=/dev/sda of=disk.img bs=4M status=progress   # Disk image
sudo dd if=disk.img of=/dev/sdb bs=4M status=progress   # Restore image

# Compression tools
gzip file.txt                   # Compress (removes original)
gzip -k file.txt                # Keep original
gunzip file.txt.gz              # Decompress
bzip2 file.txt                  # Better compression
bunzip2 file.txt.bz2            # Decompress bzip2
xz file.txt                     # Best compression
unxz file.txt.xz                # Decompress xz
zip archive.zip files           # Create zip
unzip archive.zip               # Extract zip

# 7zip (install p7zip-full)
7z a archive.7z files           # Create archive
7z x archive.7z                 # Extract archive

# Backup strategies
# Full backup
tar -czf full-backup-$(date +%Y%m%d).tar.gz /home

# Incremental backup using find
find /home -mtime -1 -type f -print0 | tar -czf incremental-$(date +%Y%m%d).tar.gz --null -T -

# Backup script example
#!/bin/bash
BACKUP_DIR="/backup"
SOURCE="/home /etc /var/www"
DATE=$(date +%Y%m%d)
tar -czf $BACKUP_DIR/backup-$DATE.tar.gz $SOURCE
find $BACKUP_DIR -name "backup-*.tar.gz" -mtime +30 -delete  # Delete old
```

**Exercise 7.5:**
1. Create a compressed tar archive of your home directory
2. List contents of the archive without extracting
3. Extract a single file from the archive
4. Use rsync to backup a directory
5. Test a dry-run rsync operation

**Challenge 7.5:** Create a comprehensive backup script that:
- Performs full backup weekly
- Performs incremental backup daily
- Compresses backups
- Rotates old backups (keep 4 weeks)
- Logs all operations
- Can restore from backup
- Sends email notification of backup status

---

## Module 8: Web Servers & Services

### Week 11-12: Web Server Administration

#### Day 34: Apache Web Server

```bash
# Installing Apache
sudo apt update
sudo apt install apache2

# Apache service management
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
sudo systemctl reload apache2    # Reload config without stopping
sudo systemctl status apache2
sudo systemctl enable apache2    # Enable at boot

# Testing Apache
curl localhost                   # Test from command line
# Or open browser: http://your_ip

# Apache configuration files
/etc/apache2/apache2.conf        # Main configuration
/etc/apache2/ports.conf          # Port configuration
/etc/apache2/sites-available/    # Available sites
/etc/apache2/sites-enabled/      # Enabled sites
/etc/apache2/mods-available/     # Available modules
/etc/apache2/mods-enabled/       # Enabled modules
/var/www/html/                   # Default document root
/var/log/apache2/                # Log files

# Virtual hosts
sudo nano /etc/apache2/sites-available/example.com.conf

# Example virtual host:
<VirtualHost *:80>
    ServerName example.com
    ServerAlias www.example.com
    ServerAdmin admin@example.com
    DocumentRoot /var/www/example.com
    
    ErrorLog ${APACHE_LOG_DIR}/example.com-error.log
    CustomLog ${APACHE_LOG_DIR}/example.com-access.log combined
    
    <Directory /var/www/example.com>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

# Enable/disable sites
sudo a2ensite example.com.conf   # Enable site
sudo a2dissite example.com.conf  # Disable site
sudo systemctl reload apache2    # Apply changes

# Modules management
sudo a2enmod rewrite             # Enable rewrite module
sudo a2enmod ssl                 # Enable SSL
sudo a2dismod autoindex          # Disable directory listing
sudo systemctl restart apache2

# Common modules
a2enmod rewrite                  # URL rewriting
a2enmod ssl                      # SSL/TLS
a2enmod headers                  # HTTP headers
a2enmod proxy                    # Proxy
a2enmod proxy_http               # HTTP proxy

# Testing configuration
sudo apache2ctl configtest       # Test config syntax
sudo apache2ctl -S               # Show virtual hosts

# Logs
sudo tail -f /var/log/apache2/access.log
sudo tail -f /var/log/apache2/error.log
sudo cat /var/log/apache2/error.log | grep error

# .htaccess (if AllowOverride All is set)
# Create .htaccess in website directory
# Example .htaccess:
# RewriteEngine On
# RewriteCond %{HTTPS} off
# RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Performance tuning
sudo nano /etc/apache2/mods-available/mpm_prefork.conf
```

**Exercise 8.1:**
1. Install Apache on your Raspberry Pi
2. Verify it's running by accessing http://raspberry_pi_ip
3. Create a custom index.html in /var/www/html
4. View Apache access logs
5. Check Apache configuration for syntax errors

**Challenge 8.1:** Set up two virtual hosts:
- site1.local serving content from /var/www/site1
- site2.local serving content from /var/www/site2
- Configure /etc/hosts to resolve these names
- Create different index.html for each
- Test both sites work correctly

---

#### Day 35: Nginx Web Server

```bash
# Installing Nginx
sudo apt update
sudo apt install nginx

# Nginx service management
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx      # Reload config (preferred)
sudo systemctl status nginx
sudo systemctl enable nginx

# Testing Nginx
curl localhost
curl -I localhost                # Headers only

# Nginx configuration
/etc/nginx/nginx.conf            # Main configuration
/etc/nginx/sites-available/      # Available sites
/etc/nginx/sites-enabled/        # Enabled sites (symlinks)
/etc/nginx/conf.d/               # Additional configs
/var/www/html/                   # Default document root
/var/log/nginx/                  # Log files

# Server blocks (virtual hosts)
sudo nano /etc/nginx/sites-available/example.com

# Example server block:
server {
    listen 80;
    listen [::]:80;
    
    server_name example.com www.example.com;
    root /var/www/example.com;
    index index.html index.htm;
    
    access_log /var/log/nginx/example.com-access.log;
    error_log /var/log/nginx/example.com-error.log;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    # PHP support
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    }
    
    # Deny .htaccess files
    location ~ /\.ht {
        deny all;
    }
}

# Enable/disable sites
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/example.com
sudo systemctl reload nginx

# Testing configuration
sudo nginx -t                    # Test configuration
sudo nginx -T                    # Test and display config

# Common configurations
# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name example.com;
    return 301 https://$server_name$request_uri;
}

# Reverse proxy
location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}

# Load balancing
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}

server {
    location / {
        proxy_pass http://backend;
    }
}

# Logs
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
sudo cat /var/log/nginx/access.log | awk '{print $1}' | sort | uniq -c | sort -rn  # Top IPs
```

**Exercise 8.2:**
1. Install Nginx (you can have both Apache and Nginx, use different ports)
2. Configure Nginx to listen on port 8080 (if Apache is on 80)
3. Create a custom index.html
4. Test the configuration
5. View Nginx access logs

**Challenge 8.2:** Configure Nginx as a reverse proxy:
- Run Apache on port 8080
- Configure Nginx on port 80 to proxy to Apache
- Test that accessing port 80 shows Apache content
- Add custom headers to identify the proxy

---

#### Day 36: SSL/TLS and HTTPS

```bash
# Installing Certbot (Let's Encrypt)
sudo apt install certbot
sudo apt install python3-certbot-apache   # For Apache
sudo apt install python3-certbot-nginx    # For Nginx

# Obtaining SSL certificate (Apache)
sudo certbot --apache -d example.com -d www.example.com

# Obtaining SSL certificate (Nginx)
sudo certbot --nginx -d example.com -d www.example.com

# Manual certificate (for testing)
sudo certbot certonly --standalone -d example.com

# Certificate renewal
sudo certbot renew                # Renew all certificates
sudo certbot renew --dry-run     # Test renewal
sudo systemctl status certbot.timer  # Auto-renewal timer

# Certificate locations
/etc/letsencrypt/live/example.com/fullchain.pem   # Certificate
/etc/letsencrypt/live/example.com/privkey.pem     # Private key
/etc/letsencrypt/live/example.com/chain.pem       # Chain
/etc/letsencrypt/live/example.com/cert.pem        # Cert only

# Self-signed certificate (for testing)
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/selfsigned.key \
    -out /etc/ssl/certs/selfsigned.crt

# Apache SSL configuration
sudo nano /etc/apache2/sites-available/example.com-ssl.conf

<VirtualHost *:443>
    ServerName example.com
    DocumentRoot /var/www/example.com
    
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/selfsigned.key
    
    # Modern SSL configuration
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite HIGH:!aNULL:!MD5
</VirtualHost>

# Nginx SSL configuration
sudo nano /etc/nginx/sites-available/example.com

server {
    listen 443 ssl http2;
    server_name example.com;
    
    ssl_certificate /etc/ssl/certs/selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/selfsigned.key;
    
    # Modern SSL settings
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    
    # Additional security headers
    add_header Strict-Transport-Security "max-age=31536000" always;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    
    root /var/www/example.com;
    index index.html;
}

# Testing SSL
openssl s_client -connect example.com:443
curl -k https://example.com      # -k to ignore self-signed warning

# SSL testing tools
# Check SSL Labs: https://www.ssllabs.com/ssltest/
```

**Exercise 8.3:**
1. Generate a self-signed SSL certificate
2. Configure your web server to use HTTPS
3. Set up HTTP to HTTPS redirect
4. Test HTTPS connection
5. View certificate details

**Challenge 8.3:** Implement complete SSL configuration:
- Generate self-signed certificate
- Configure both HTTP (redirect) and HTTPS
- Add security headers
- Force HTTPS for all traffic
- Test with curl and browser
- Document the process

---

#### Day 37: PHP and Database Integration

```bash
# Installing PHP
sudo apt install php libapache2-mod-php php-mysql
sudo systemctl restart apache2

# For Nginx (uses PHP-FPM)
sudo apt install php-fpm php-mysql
sudo systemctl start php7.4-fpm
sudo systemctl enable php7.4-fpm

# Testing PHP (Apache)
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
# Visit: http://your_ip/info.php
sudo rm /var/www/html/info.php   # Remove after testing (security)

# PHP configuration
/etc/php/7.4/apache2/php.ini     # Apache PHP config
/etc/php/7.4/fpm/php.ini         # PHP-FPM config
/etc/php/7.4/cli/php.ini         # CLI PHP config

# Common PHP settings to modify
sudo nano /etc/php/7.4/apache2/php.ini
# upload_max_filesize = 20M
# post_max_size = 20M
# max_execution_time = 300
# memory_limit = 256M

# Installing MySQL/MariaDB
sudo apt install mariadb-server mariadb-client
sudo systemctl start mariadb
sudo systemctl enable mariadb

# Secure MySQL installation
sudo mysql_secure_installation
# - Set root password
# - Remove anonymous users
# - Disallow root login remotely
# - Remove test database
# - Reload privilege tables

# MySQL/MariaDB basics
sudo mysql -u root -p

# In MySQL:
CREATE DATABASE myapp;
CREATE USER 'myapp_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON myapp.* TO 'myapp_user'@'localhost';
FLUSH PRIVILEGES;
SHOW DATABASES;
USE myapp;
EXIT;

# Testing PHP-MySQL connection
sudo nano /var/www/html/dbtest.php

<?php
$servername = "localhost";
$username = "myapp_user";
$password = "password";
$dbname = "myapp";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully to database: " . $dbname;
$conn->close();
?>

# MySQL management
sudo systemctl status mariadb
sudo systemctl restart mariadb
mysql -u username -p database_name < backup.sql  # Import
mysqldump -u username -p database_name > backup.sql  # Export

# Installing phpMyAdmin (optional)
sudo apt install phpmyadmin
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
# Visit: http://your_ip/phpmyadmin

# PostgreSQL alternative
sudo apt install postgresql postgresql-contrib
sudo -u postgres psql
# CREATE DATABASE myapp;
# CREATE USER myapp_user WITH PASSWORD 'password';
# GRANT ALL PRIVILEGES ON DATABASE myapp TO myapp_user;
# \q
```

**Exercise 8.4:**
1. Install PHP and verify it works with web server
2. Install MySQL/MariaDB
3. Secure the MySQL installation
4. Create a database and user
5. Test PHP-MySQL connection

**Challenge 8.4:** Deploy a complete LAMP/LEMP stack application:
- Set up virtual host
- Install WordPress or similar CMS
- Configure database
- Ensure proper file permissions
- Test full functionality
- Create backup script for database and files

---

#### Day 38: Web Server Troubleshooting

```bash
# Common issues and solutions

# 1. Check if service is running
sudo systemctl status apache2
sudo systemctl status nginx
sudo systemctl status php7.4-fpm

# 2. Check ports
sudo netstat -tlnp | grep :80
sudo ss -tlnp | grep :80
sudo lsof -i :80

# 3. Test configuration
sudo apache2ctl configtest
sudo nginx -t

# 4. Check logs
sudo tail -100 /var/log/apache2/error.log
sudo tail -100 /var/log/nginx/error.log
sudo journalctl -u apache2 -n 50
sudo journalctl -u nginx -n 50

# 5. File permissions
ls -la /var/www/html/
# Should be owned by www-data:www-data (Ubuntu)
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/

# 6. SELinux (if enabled)
getenforce                       # Check if SELinux is active
sudo setenforce 0                # Temporarily disable (testing only)

# 7. Firewall
sudo ufw status
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 8. DNS issues
nslookup example.com
dig example.com
host example.com

# 9. Test connectivity
curl -v http://localhost
curl -v http://your_domain.com
wget http://localhost

# 10. Check disk space
df -h
du -sh /var/www/*
du -sh /var/log/*

# 11. Process limits
ps aux | grep apache2 | wc -l
ps aux | grep nginx | wc -l
# Check MaxRequestWorkers (Apache) or worker_processes (Nginx)

# 12. Database connection
mysql -u username -p -h localhost database_name
mysqladmin -u root -p status

# 13. PHP errors
cat /var/log/php7.4-fpm.log
sudo nano /etc/php/7.4/apache2/php.ini
# display_errors = On (development only!)
# log_errors = On
# error_log = /var/log/php_errors.log

# 14. Network troubleshooting
ping your_server_ip
traceroute your_server_ip
tcpdump -i any port 80

# 15. Performance monitoring
top
htop
apache2ctl status
sudo apache2ctl fullstatus (enable mod_status first)

# Enable mod_status (Apache)
sudo a2enmod status
# Add to apache2.conf or site config:
<Location "/server-status">
    SetHandler server-status
    Require ip 127.0.0.1
</Location>

# Nginx status
# Add to server block:
location /nginx_status {
    stub_status on;
    allow 127.0.0.1;
    deny all;
}

# Stress testing
ab -n 1000 -c 10 http://localhost/  # Apache Bench
# -n: number of requests
# -c: concurrent requests
```

**Exercise 8.5:**
1. Deliberately break your web server config and fix it
2. Check web server logs for errors
3. Verify file permissions on web directory
4. Test configuration syntax
5. Monitor web server processes

**Challenge 8.5:** Create a web server monitoring script:
- Checks if web server is running
- Verifies HTTP response (200 OK)
- Checks disk space
- Monitors error log for issues
- Sends alert if problems detected
- Runs every 5 minutes via cron
- Logs all checks

---

## Module 9: Security & Hardening

### Week 13: System Security

#### Day 39: Basic Security Hardening

```bash
# 1. Update system regularly
sudo apt update && sudo apt upgrade -y
sudo apt autoremove
sudo unattended-upgrades         # Auto security updates

# Enable automatic updates
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades

# 2. Configure firewall
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp            # SSH
sudo ufw allow 80/tcp            # HTTP
sudo ufw allow 443/tcp           # HTTPS
sudo ufw enable
sudo ufw status verbose

# 3. Secure SSH
sudo nano /etc/ssh/sshd_config
# Change these settings:
# Port 2222                      # Change default port (optional)
# PermitRootLogin no             # Disable root login
# PasswordAuthentication no      # Use keys only
# PubkeyAuthentication yes
# AllowUsers yourusername        # Limit users
# MaxAuthTries 3
# ClientAliveInterval 300
# ClientAliveCountMax 2

sudo systemctl restart sshd

# 4. Fail2ban (protect against brute force)
sudo apt install fail2ban
sudo systemctl start fail2ban
sudo systemctl enable fail2ban

sudo nano /etc/fail2ban/jail.local
# [sshd]
# enabled = true
# port = 22
# filter = sshd
# logpath = /var/log/auth.log
# maxretry = 3
# bantime = 3600

sudo systemctl restart fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd

# 5. Disable unnecessary services
systemctl list-unit-files --state=enabled
sudo systemctl disable service_name
sudo systemctl stop service_name

# 6. Remove unused packages
dpkg --list | grep unused
sudo apt autoremove
sudo apt autopurge

# 7. File integrity monitoring (AIDE)
sudo apt install aide
sudo aideinit
sudo mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
sudo aide --check               # Check for changes

# 8. Secure shared memory
sudo nano /etc/fstab
# Add: tmpfs /run/shm tmpfs defaults,noexec,nosuid 0 0
sudo mount -o remount /run/shm

# 9. Kernel hardening (sysctl)
sudo nano /etc/sysctl.conf
# Add these:
```
---

#### Day 40: User and Permission Auditing

```bash
# Finding files with specific permissions
find / -perm -4000 2>/dev/null  # SUID files
find / -perm -2000 2>/dev/null  # SGID files
find / -perm -1000 2>/dev/null  # Sticky bit files
find / -perm -777 2>/dev/null   # World-writable files (dangerous!)
find / -nouser 2>/dev/null      # Files with no owner
find / -nogroup 2>/dev/null     # Files with no group

# World-writable directories (except /tmp, /var/tmp)
find / -type d -perm -002 2>/dev/null | grep -v '/tmp\|/var/tmp\|/proc\|/sys'

# Files modified in last 7 days
find /etc -mtime -7 -type f

# Large files that might be suspicious
find / -size +100M -type f 2>/dev/null

# User auditing
awk -F: '($3 >= 1000) {print $1}' /etc/passwd  # Regular users
awk -F: '($3 == 0) {print $1}' /etc/passwd     # Root equivalent users (should only be root)
awk -F: '($2 == "") {print $1}' /etc/shadow    # Users with no password

# Group auditing
cat /etc/group                   # All groups
getent group sudo                # Members of sudo group
groups username                  # User's groups

# Check for unauthorized changes
rpm -Va                          # RHEL/CentOS
debsums -c                       # Debian/Ubuntu (install debsums)

# AppArmor (Ubuntu/Debian)
sudo aa-status                   # AppArmor status
sudo aa-enforce /path/to/profile # Enforce mode
sudo aa-complain /path/to/profile # Complain mode
sudo aa-disable /path/to/profile # Disable profile

# SELinux (RHEL/CentOS)
getenforce                       # Check mode
sestatus                         # Detailed status
sudo setenforce 1                # Enforcing mode
ls -Z                            # List SELinux contexts
ps -eZ                           # Process contexts

# Sudo usage audit
sudo grep sudo /var/log/auth.log # Who used sudo
sudo last                        # Login history
sudo lastb                       # Failed login attempts

# Check for rootkits
sudo apt install chkrootkit rkhunter
sudo chkrootkit
sudo rkhunter --check
```

**Exercise 9.2:**
1. Find all SUID files on your system
2. Identify world-writable files
3. List all users with UID >= 1000
4. Check which users are in the sudo group
5. Review recent file modifications in /etc

**Challenge 9.2:** Create a security audit script that:
- Checks for suspicious file permissions
- Lists unauthorized SUID/SGID files
- Identifies files without owners
- Checks for empty passwords
- Audits sudo group membership
- Generates a report with findings
- Emails/alerts on critical issues

---

#### Day 41: Encryption and Secrets Management

```bash
# GPG (GNU Privacy Guard)
gpg --gen-key                    # Generate key pair
gpg --list-keys                  # List public keys
gpg --list-secret-keys           # List private keys

# Encrypting files
gpg -c file.txt                  # Symmetric encryption (password)
gpg -e -r recipient@email file.txt  # Asymmetric encryption
gpg -d file.txt.gpg              # Decrypt

# Signing and verifying
gpg --sign file.txt              # Sign file
gpg --verify file.txt.gpg        # Verify signature
gpg --clearsign file.txt         # Sign (readable text)

# Exporting keys
gpg --export -a "User Name" > public.key
gpg --export-secret-key -a "User Name" > private.key
gpg --import public.key          # Import key

# Encrypting partitions (LUKS)
sudo apt install cryptsetup

# Create encrypted partition
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 encrypted_volume
sudo mkfs.ext4 /dev/mapper/encrypted_volume
sudo mount /dev/mapper/encrypted_volume /mnt

# Close encrypted volume
sudo umount /mnt
sudo cryptsetup luksClose encrypted_volume

# Encrypted home directory
sudo apt install ecryptfs-utils
ecryptfs-migrate-home -u username

# SSL/TLS certificates
# Generate private key
openssl genrsa -out private.key 2048

# Generate certificate signing request
openssl req -new -key private.key -out request.csr

# Generate self-signed certificate
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes

# View certificate
openssl x509 -in cert.pem -text -noout

# Test SSL connection
openssl s_client -connect example.com:443

# Password management
# Generate random passwords
openssl rand -base64 32
pwgen -s 20 1                    # Install pwgen first

# Password hashing
echo -n "password" | sha256sum
echo -n "password" | openssl passwd -6 -stdin  # SHA-512

# Secure file deletion
sudo apt install secure-delete
shred -vfz -n 10 file.txt       # Overwrite and delete
srm file.txt                     # Secure remove
sfill /path                      # Fill free space

# Secrets in environment variables
export DB_PASSWORD="secret"      # Don't do this in production!
# Better: Use .env files not in version control

# Vault (HashiCorp Vault) - advanced
# Install from hashicorp.com
vault server -dev                # Development server
export VAULT_ADDR='http://127.0.0.1:8200'
vault kv put secret/db password=secret
vault kv get secret/db
```

**Exercise 9.3:**
1. Generate a GPG key pair
2. Encrypt a file using GPG
3. Decrypt the file
4. Generate a self-signed SSL certificate
5. Create secure random passwords

**Challenge 9.3:** Implement encryption strategy:
- Create encrypted partition for sensitive data
- Set up GPG for file encryption
- Generate and manage SSL certificates
- Create secure password generation script
- Document encryption/decryption procedures
- Test backup and recovery of encrypted data

---

#### Day 42: Security Monitoring and Logging

```bash
# Centralized logging
# Install rsyslog (usually installed by default)
sudo apt install rsyslog
sudo systemctl status rsyslog

# Configure remote logging
sudo nano /etc/rsyslog.conf
# On log server:
# module(load="imudp")
# input(type="imudp" port="514")

# On clients:
# *.* @logserver_ip:514         # UDP
# *.* @@logserver_ip:514        # TCP

sudo systemctl restart rsyslog

# Auditd (detailed system auditing)
sudo apt install auditd audispd-plugins
sudo systemctl start auditd
sudo systemctl enable auditd

# Audit rules
sudo auditctl -l                 # List rules
sudo auditctl -w /etc/passwd -p wa -k passwd_changes
sudo auditctl -w /etc/shadow -p wa -k shadow_changes
sudo auditctl -w /var/log/auth.log -p wa -k auth_log_changes

# Make rules persistent
sudo nano /etc/audit/rules.d/audit.rules
# Add rules, then:
sudo augenrules --load

# Search audit logs
sudo ausearch -k passwd_changes
sudo ausearch -ua username       # By user
sudo ausearch -f /etc/passwd     # By file
sudo aureport                    # Summary report
sudo aureport -au                # Authentication report

# Logwatch (log analyzer)
sudo apt install logwatch
sudo logwatch --detail High --mailto your@email.com --service all --range today

# Configure logwatch
sudo nano /etc/logwatch/conf/logwatch.conf
# MailTo = your@email.com
# Range = yesterday
# Detail = High

# Manual cron for daily reports
sudo crontab -e
# 0 6 * * * /usr/sbin/logwatch --output mail --mailto your@email.com --detail high

# Log analysis tools
# 1. GoAccess (web server log analyzer)
sudo apt install goaccess
goaccess /var/log/apache2/access.log -o report.html --log-format=COMBINED
goaccess /var/log/nginx/access.log -o report.html --log-format=COMBINED

# 2. Logrotate monitoring
cat /etc/logrotate.conf
ls /etc/logrotate.d/
sudo logrotate -d /etc/logrotate.conf  # Debug mode

# 3. Monitoring failed login attempts
sudo grep "Failed password" /var/log/auth.log
sudo grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn

# 4. SSH login monitoring
sudo grep "Accepted" /var/log/auth.log
sudo last -n 20                  # Last 20 logins
sudo lastb -n 20                 # Last 20 failed logins

# 5. Intrusion detection (OSSEC/Wazuh)
# Basic installation (simplified)
wget -q -O - https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
# Follow official documentation for full installation

# Real-time log monitoring script
#!/bin/bash
tail -f /var/log/auth.log | while read line; do
    echo $line | grep -q "Failed password"
    if [ $? -eq 0 ]; then
        echo "Alert: Failed login attempt detected!"
        echo $line
        # Send notification here
    fi
done

# Security alerts
# Install alerting tool
sudo apt install mailutils        # For email alerts

# Create alert script
sudo nano /usr/local/bin/security-alert.sh
#!/bin/bash
ALERT_EMAIL="admin@example.com"

# Check for failed logins
FAILED=$(grep "Failed password" /var/log/auth.log | tail -20)
if [ ! -z "$FAILED" ]; then
    echo "$FAILED" | mail -s "Security Alert: Failed Logins" $ALERT_EMAIL
fi

# Check for new SUID files
# (Store baseline in /root/suid_baseline.txt)
find / -perm -4000 2>/dev/null > /tmp/suid_current.txt
diff /root/suid_baseline.txt /tmp/suid_current.txt > /tmp/suid_diff.txt
if [ -s /tmp/suid_diff.txt ]; then
    cat /tmp/suid_diff.txt | mail -s "Security Alert: New SUID Files" $ALERT_EMAIL
fi

# Schedule in cron
sudo crontab -e
# 0 * * * * /usr/local/bin/security-alert.sh
```

**Exercise 9.4:**
1. Configure auditd to monitor /etc/passwd changes
2. Set up logwatch for daily reports
3. Analyze web server logs with goaccess
4. Monitor failed SSH login attempts
5. Create a simple log monitoring script

**Challenge 9.4:** Build comprehensive security monitoring system:
- Configure auditd for critical files
- Set up automated log analysis
- Create real-time alert system
- Monitor for suspicious activities:
  - Failed logins
  - New SUID files
  - Unauthorized sudo usage
  - Large file transfers
- Generate daily security reports
- Set up log retention and rotation

---

## Module 10: Advanced Topics & Automation

### Week 14-16: Advanced System Administration

#### Day 43: Advanced Bash Scripting

```bash
# Advanced variable manipulation
STRING="Hello World"
echo ${STRING,,}                 # Lowercase
echo ${STRING^^}                 # Uppercase
echo ${STRING:0:5}               # Substring
echo ${STRING/World/Linux}       # Replace
echo ${STRING#Hello }            # Remove from start
echo ${STRING%World}             # Remove from end

# Arrays (advanced)
ARRAY=(one two three four five)
echo ${ARRAY[@]}                 # All elements
echo ${ARRAY[2]}                 # Third element
echo ${#ARRAY[@]}                # Array length
ARRAY+=(six)                     # Append
unset ARRAY[2]                   # Remove element

# Associative arrays
declare -A USER_AGES
USER_AGES[alice]=25
USER_AGES[bob]=30
echo ${USER_AGES[alice]}
echo ${!USER_AGES[@]}            # All keys
echo ${USER_AGES[@]}             # All values

# Advanced conditionals
[[ $VAR =~ ^[0-9]+$ ]]          # Regex match (numbers only)
[[ -z $VAR ]]                    # Empty string
[[ -n $VAR ]]                    # Not empty
[[ $FILE1 -nt $FILE2 ]]         # FILE1 newer than FILE2
[[ $FILE1 -ot $FILE2 ]]         # FILE1 older than FILE2

# Process substitution
diff <(ls dir1) <(ls dir2)      # Compare directory contents
while read line; do echo $line; done < <(command)

# Here documents
cat << EOF > file.txt
Line 1
Line 2
Variable: $VAR
EOF

# Command grouping
{ command1; command2; } > output.txt
( cd /tmp && command )           # Run in subshell

# Traps (error handling)
#!/bin/bash
cleanup() {
    echo "Cleaning up..."
    rm -f /tmp/tempfile
}
trap cleanup EXIT                # Run on exit
trap 'echo "Error on line $LINENO"' ERR

# Parallel execution
#!/bin/bash
for i in {1..5}; do
    (
        echo "Task $i starting"
        sleep 2
        echo "Task $i done"
    ) &
done
wait                             # Wait for all background jobs

# Logging function
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a /var/log/myscript.log
}

log "Script started"

# Argument parsing
while getopts "hv:f:" opt; do
    case $opt in
        h) echo "Help message"; exit 0 ;;
        v) VERBOSE=$OPTARG ;;
        f) FILE=$OPTARG ;;
        \?) echo "Invalid option"; exit 1 ;;
    esac
done

# Configuration file parsing
#!/bin/bash
CONFIG_FILE="config.ini"
while IFS='=' read -r key value; do
    case $key in
        username) USERNAME=$value ;;
        password) PASSWORD=$value ;;
    esac
done < "$CONFIG_FILE"

# Advanced script template
#!/bin/bash
set -euo pipefail               # Exit on error, undefined var, pipe fail

# Script metadata
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
SCRIPT_NAME="$(basename "${BASH_SOURCE[0]}")"
LOG_FILE="/var/log/${SCRIPT_NAME%.sh}.log"

# Functions
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

error() {
    log "ERROR: $*" >&2
    exit 1
}

usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS]

Options:
    -h, --help      Show this help message
    -v, --verbose   Verbose output
    -f FILE         Input file

EOF
    exit 0
}

cleanup() {
    log "Cleaning up..."
    # Cleanup code here
}

# Main logic
main() {
    log "Script started"
    
    # Your code here
    
    log "Script completed successfully"
}

# Setup
trap cleanup EXIT
trap 'error "Script failed on line $LINENO"' ERR

# Run
main "$@"
```

**Exercise 10.1:**
1. Create a script using associative arrays to store user info
2. Implement proper error handling with traps
3. Add command-line argument parsing
4. Create a logging function
5. Use process substitution to compare outputs

**Challenge 10.1:** Create a professional deployment script:
- Parse configuration from file
- Validate all prerequisites
- Implement rollback on failure
- Comprehensive logging
- Email notifications
- Parallel task execution
- Progress indicators
- Detailed error messages

---

#### Day 44: System Automation with Ansible (Introduction)

```bash
# Installing Ansible
sudo apt update
sudo apt install ansible

# Ansible configuration
/etc/ansible/ansible.cfg         # Global config
~/.ansible.cfg                   # User config
./ansible.cfg                    # Project config

# Inventory file
sudo nano /etc/ansible/hosts
# or create local inventory
nano inventory.ini

# Example inventory:
[webservers]
web1.example.com
web2.example.com

[databases]
db1.example.com

[pi]
192.168.1.100 ansible_user=pi

[all:vars]
ansible_python_interpreter=/usr/bin/python3

# Testing connectivity
ansible all -m ping -i inventory.ini
ansible webservers -m ping
ansible -i inventory.ini pi -m ping

# Ad-hoc commands
ansible all -a "uptime"          # Run command
ansible all -m shell -a "df -h"  # Shell module
ansible all -m copy -a "src=/path/file dest=/tmp/"
ansible all -m apt -a "name=nginx state=present" --become

# Playbooks
# Create playbook.yml
nano playbook.yml

---
- name: Configure web servers
  hosts: webservers
  become: yes
  
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600
    
    - name: Install nginx
      apt:
        name: nginx
        state: present
    
    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: yes
    
    - name: Copy website files
      copy:
        src: ./html/
        dest: /var/www/html/
        owner: www-data
        group: www-data
        mode: '0644'
    
    - name: Template configuration
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Restart nginx
  
  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted

# Running playbooks
ansible-playbook playbook.yml
ansible-playbook -i inventory.ini playbook.yml
ansible-playbook playbook.yml --check  # Dry run
ansible-playbook playbook.yml --tags "install"
ansible-playbook playbook.yml -v      # Verbose
ansible-playbook playbook.yml --limit webservers

# Variables
# In playbook:
vars:
  http_port: 80
  domain_name: example.com

# Variable files
# vars.yml
http_port: 80
max_clients: 200

# Use in playbook:
vars_files:
  - vars.yml

# Ansible Vault (encrypted variables)
ansible-vault create secrets.yml
ansible-vault edit secrets.yml
ansible-vault encrypt existing.yml
ansible-vault decrypt existing.yml
ansible-playbook playbook.yml --ask-vault-pass

# Roles (organized playbooks)
ansible-galaxy init myrole       # Create role structure
# Directory structure:
# myrole/
#   tasks/
#   handlers/
#   templates/
#   files/
#   vars/
#   defaults/
#   meta/

# Using roles in playbook:
roles:
  - myrole
  - { role: anotherrole, when: ansible_os_family == "Debian" }

# Ansible Galaxy (community roles)
ansible-galaxy search nginx
ansible-galaxy install geerlingguy.nginx
ansible-galaxy list

# Example: Complete web server setup
---
- name: Setup LAMP Stack
  hosts: webservers
  become: yes
  
  vars:
    mysql_root_password: "{{ vault_mysql_root_password }}"
    app_user: webapp
  
  tasks:
    - name: Install required packages
      apt:
        name:
          - apache2
          - mysql-server
          - php
          - libapache2-mod-php
          - php-mysql
        state: present
    
    - name: Create application user
      user:
        name: "{{ app_user }}"
        state: present
        shell: /bin/bash
    
    - name: Configure MySQL
      mysql_user:
        name: root
        password: "{{ mysql_root_password }}"
        host: localhost
        state: present
    
    - name: Enable Apache modules
      apache2_module:
        name: "{{ item }}"
        state: present
      loop:
        - rewrite
        - ssl
      notify: Restart Apache
    
    - name: Copy virtual host config
      template:
        src: vhost.conf.j2
        dest: /etc/apache2/sites-available/app.conf
      notify: Restart Apache
    
    - name: Enable site
      command: a2ensite app.conf
      notify: Restart Apache
  
  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
```

**Exercise 10.2:**
1. Install Ansible on your Ubuntu Desktop
2. Create inventory with your Raspberry Pi
3. Test connectivity with ping module
4. Run ad-hoc command to check disk space
5. Create simple playbook to install a package

**Challenge 10.2:** Create complete infrastructure automation:
- Multi-server inventory
- Playbook to configure web servers
- Playbook to configure database servers
- Use variables and templates
- Implement roles for reusability
- Use Vault for sensitive data
- Create deployment playbook
- Document the entire setup

---
#### Day 45: Containers - Docker Basics

```bash
# Installing Docker
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io

# Add user to docker group (no sudo needed)
sudo usermod -aG docker $USER
newgrp docker                    # Or logout/login

# Docker basics
docker --version
docker info
docker run hello-world           # Test installation

# Running containers
docker run ubuntu                # Run Ubuntu container
docker run -it ubuntu bash       # Interactive terminal
docker run -d nginx              # Detached mode
docker run -d -p 8080:80 nginx   # Port mapping
docker run -d --name mynginx nginx  # Named container
docker run -d -v /host/path:/container/path nginx  # Volume mount
docker run -e "ENV_VAR=value" nginx  # Environment variable

# Container management
docker ps                        # Running containers
docker ps -a                     # All containers
docker stop container_id         # Stop container
docker start container_id        # Start container
docker restart container_id      # Restart container
docker rm container_id           # Remove container
docker rm -f container_id        # Force remove running container
docker exec -it container_id bash  # Execute command in container
docker logs container_id         # View logs
docker logs -f container_id      # Follow logs
docker inspect container_id      # Detailed info

# Images
docker images                    # List images
docker pull ubuntu:20.04         # Pull image
docker rmi image_id              # Remove image
docker search nginx              # Search Docker Hub
docker history image_id          # Image history
docker tag image_id myimage:tag  # Tag image

# Building images (Dockerfile)
nano Dockerfile

# Example Dockerfile:
FROM ubuntu:20.04
LABEL maintainer="you@example.com"
RUN apt-get update && apt-get install -y \
    nginx \
    && rm -rf /var/lib/apt/lists/*
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Build image
docker build -t mywebserver:1.0 .
docker build -t mywebserver:1.0 -f CustomDockerfile .

# Multi-stage builds
FROM node:14 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Docker Compose
sudo apt install docker-compose

# docker-compose.yml
version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db
  
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: myapp
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:

# Docker Compose commands
docker-compose up                # Start services
docker-compose up -d             # Detached
docker-compose down              # Stop and remove
docker-compose ps                # List services
docker-compose logs              # View logs
docker-compose logs -f web       # Follow specific service
docker-compose exec web bash     # Execute in service
docker-compose build             # Build images
docker-compose restart           # Restart services

# Networks
docker network ls                # List networks
docker network create mynetwork  # Create network
docker network inspect mynetwork # Inspect network
docker run --network=mynetwork nginx  # Run in network
docker network connect mynetwork container_id  # Connect container

# Volumes
docker volume ls                 # List volumes
docker volume create myvolume    # Create volume
docker volume inspect myvolume   # Inspect volume
docker volume rm myvolume        # Remove volume
docker run -v myvolume:/data nginx  # Use volume

# Docker system
docker system df                 # Disk usage
docker system prune              # Clean up
docker system prune -a           # Remove all unused
docker image prune               # Remove unused images
docker container prune           # Remove stopped containers

# Docker registry
docker login                     # Login to Docker Hub
docker push username/image:tag   # Push image
docker pull username/image:tag   # Pull image

# Private registry
docker run -d -p 5000:5000 --name registry registry:2
docker tag myimage localhost:5000/myimage
docker push localhost:5000/myimage
```

**Exercise 10.3:**
1. Install Docker
2. Run a container and explore it
3. Create a simple Dockerfile
4. Build and run your custom image
5. Set up a multi-container application with docker-compose

**Challenge 10.3:** Dockerize a web application:
- Create Dockerfile for application
- Use multi-stage build
- Set up docker-compose with:
  - Web server
  - Application server
  - Database
  - Redis cache
- Configure volumes for persistence
- Set up networks properly
- Add health checks
- Configure for production

---
