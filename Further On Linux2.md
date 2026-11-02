---

title: "Further on Linux — Day 4"  
tags:

- linux
    
- cybersecurity
    
- ethical-hacking
    
- linux-fundamentals
    
- vim
    
- nano
    
- user-management  
    date: 2026-11-02
    

---

# Further on Linux — Day 4

> [!abstract] Lesson Overview  
> This lesson covers the Linux File Hierarchy, text editors (VIM and Nano), and Linux User Management. These are foundational skills for Linux administration and ethical hacking.

## Learning Objectives

By the end of this lesson, I should be able to:

- Understand the Linux directory structure.
    
- Identify important Linux system directories.
    
- Create and edit files using VIM and Nano.
    
- Save, exit, undo, and redo changes in text editors.
    
- Understand Linux users, groups, privileges, and root.
    
- Create users and identify where Linux stores account information.
    
- Use `sudo` safely.
    

---

# 1. Linux File Hierarchy

## 1.1 What is a File System?

A **file system** is the structure and method an operating system uses to organize and manage files and directories.

Linux and Windows organize their files differently.

|Windows|Linux|
|---|---|
|Uses drive letters such as `C:`|Uses one root directory `/`|
|Example: `C:\Users\User`|Example: `/home/user`|
|Separate drive letters are common|Different disks can be mounted into directories|

### Why is this important in cybersecurity?

Ethical hackers and system administrators must understand where Linux stores:

- Configuration files
    
- User files
    
- System programs
    
- Logs
    
- Device information
    
- Temporary files
    

Knowing the filesystem helps during system administration, troubleshooting, and authorized security assessments.

## 1.2 Linux Directory Structure

The Linux filesystem begins at `/`, called the **root directory**.

<figure>  
<img src="[https://upload.wikimedia.org/wikipedia/commons/5/5f/Linux_Directory_Structure.svg](https://upload.wikimedia.org/wikipedia/commons/5/5f/Linux_Directory_Structure.svg)" alt="Linux directory hierarchy"/>  
</figure>

> [!important]  
> `/` and `/root` are different directories.
> 
> - `/` = filesystem root
>     
> - `/root` = home directory of the root user
>     

## 1.3 Important Linux Directories

|Directory|Purpose|Example|
|---|---|---|
|`/`|Root of the entire filesystem|`/home`, `/etc`|
|`/bin`|Essential command binaries|`ls`, `cat`, `cp`|
|`/boot`|Bootloader and kernel-related files|GRUB, kernel images|
|`/dev`|Device files|`/dev/tty`, `/dev/sda`|
|`/etc`|System configuration files|`/etc/passwd`|
|`/home`|Normal users' home directories|`/home/gemechu`|
|`/lib`|Essential shared libraries|System libraries|
|`/media`|Common mount points for removable media|USB drives|
|`/mnt`|Temporary/manual mount point|Mounted filesystem|
|`/opt`|Optional/add-on application software|Vendor applications|
|`/sbin`|Essential system administration binaries|System utilities|
|`/tmp`|Temporary files|Temporary scripts|
|`/usr`|Programs, libraries, documentation|`/usr/bin`|

### Important subdirectories of `/usr`

|Directory|Purpose|
|---|---|
|`/usr/bin`|User programs|
|`/usr/sbin`|System administration programs|
|`/usr/lib`|Libraries used by programs|
|`/usr/src`|Source code, including kernel-related sources when installed|

> [!note] Modern Linux  
> On many modern distributions, `/bin`, `/sbin`, and `/lib` are symbolic links to corresponding directories under `/usr`. Their traditional purposes remain useful to understand.

## 1.4 Exploring the Linux Filesystem

### Command 1: `pwd`

```
pwd
```

**Purpose:** Print the current working directory.

Example:

```
/home/gemechu
```

### Command 2: `ls`

```
ls /
```

**Purpose:** List the contents of the root directory.

### Command 3: `ls -l`

```
ls -l /etc
```

**Purpose:** Display files with detailed information.

### Command 4: `cd`

```
cd /etc
```

**Purpose:** Change the current directory.

### Command 5: `tree`

```
tree /
```

**Purpose:** Display directory structures in tree format.

If `tree` is not installed:

```
sudo apt install tree
```

Then:

```
tree -L 2 /
```

`-L 2` limits the displayed depth to two levels.

> [!warning] Security  
> Do not recursively modify or delete system directories without understanding the consequences.

---

# 2. Linux Text Editors

## 2.1 What is a Text Editor?

A **text editor** is a program used to create, view, and modify text files.

Text editors are important in cybersecurity because we frequently edit:

- Configuration files
    
- Scripts
    
- Linux commands
    
- Network configuration
    
- Security tool settings
    
- Documentation
    

## 2.2 Types of Text Editors

|Command-line editors|Graphical editors|
|---|---|
|VIM|VS Code|
|Nano|Sublime Text|
|Emacs|Gedit|
|Neovim|Pluma|

This lesson focuses on VIM and Nano.

---

# 3. VIM Editor

## 3.1 What is VIM?

**VIM = Vi IMproved**

VIM is a powerful command-line text editor developed from the traditional Vi editor.

It is useful when editing files through a terminal, especially on remote Linux servers.

## 3.2 VIM Modes

VIM mainly operates using two fundamental modes in this lesson.

|Mode|Purpose|
|---|---|
|Normal mode|Navigation and editing commands|
|Insert mode|Writing text|

VIM opens in Normal mode by default.

### Important Keys

|Key|Action|
|---|---|
|`i`|Enter Insert mode|
|`Esc`|Return to Normal mode|
|`x`|Delete character under cursor|
|`u`|Undo|
|`Ctrl + r`|Redo|

## 3.3 Opening a File

### Syntax

```
vim filename
```

Example:

```
vim notes.txt
```

This opens `notes.txt` or creates it when saving if it does not exist.

## 3.4 Creating and Writing a File

### Practical Lab

Create a file named `takeme.txt`.

```
vim takeme.txt
```

Step 1: Press:

```
i
```

Step 2: Type:

```
This is The Inserted Text from Planet Mars!
```

Step 3: Press:

```
Esc
```

Step 4: Save and exit:

```
:wq
```

Press Enter.

### Explanation

- `:` opens the command-line area in VIM.
    
- `w` means write/save.
    
- `q` means quit.
    

## 3.5 Important VIM Commands

|Command|Meaning|
|---|---|
|`:w`|Save|
|`:q`|Quit|
|`:wq`|Save and quit|
|`:q!`|Quit without saving changes|
|`:wq!`|Force write and quit|
|`:u`|Undo|
|`:undo`|Undo|
|`Ctrl + r`|Redo|

> [!important]  
> `!` means force. It does not mean that VIM will always overcome every permission restriction.

## 3.6 Executing External Commands in VIM

To execute a shell command from VIM:

```
:!ls
```

This executes `ls` in the shell.

To filter the entire buffer through an external command:

```
:%!command
```

- `%` = entire file
    
- `!` = filter through an external command
    

> [!warning] Be careful  
> `:%!command` can replace your entire buffer with the command's output. Understand the command before executing it.

---

# 4. Nano Editor

## 4.1 What is Nano?

**Nano** is a beginner-friendly command-line text editor.

Unlike VIM, Nano allows you to start typing immediately after opening a file.

It is useful for quickly editing Linux configuration files and scripts.

## 4.2 Opening Nano

### Syntax

```
nano filename
```

Example:

```
nano notes.txt
```

If the file does not exist, Nano can create it when you save.

## 4.3 Creating a File Using Nano

### Practical Lab

Create:

```
nano Day4_MoreLinux.md
```

Write:

```
# Day 4 Linux Course Note

This is day 4 course note.

I am learning Linux Fundamentals.
```

## 4.4 Saving and Exiting Nano

|Shortcut|Action|
|---|---|
|`Ctrl + O`|Write Out / Save|
|`Ctrl + X`|Exit|
|`Ctrl + K`|Cut current line|
|`Ctrl + U`|Paste previously cut text|
|`Ctrl + W`|Search|
|`Ctrl + R`|Read/insert another file|
|`Alt + U`|Undo|
|`Alt + E`|Redo|

### Saving

Press:

```
Ctrl + O
```

Then press Enter to confirm the filename.

### Exiting

Press:

```
Ctrl + X
```

If prompted to save changes, answer appropriately.

> [!note]  
> The `^` symbol shown in Nano's shortcut menu means Ctrl. For example, `^X` means Ctrl + X.

## 4.5 Copy and Paste in Linux Terminal

In many Linux terminal applications:

|Shortcut|Action|
|---|---|
|`Ctrl + Shift + C`|Copy selected terminal text|
|`Ctrl + Shift + V`|Paste text into terminal|

These are terminal shortcuts, not universal Nano editor shortcuts.

---

# 5. Practical Lab: VIM and Nano

## Exercise 1: Create a File Using VIM

```
vim takeme.txt
```

Write:

```
This is The Inserted Text from Planet Mars!
```

Save and exit:

```
:wq
```

Verify:

```
cat takeme.txt
```

Expected output:

```
This is The Inserted Text from Planet Mars!
```

## Exercise 2: Create a Markdown File Using Nano

```
nano Day4_MoreLinux.md
```

Write:

```
# Day 4

This is day 4 course note.
```

Save using `Ctrl + O`, Enter, then exit using `Ctrl + X`.

Verify:

```
cat Day4_MoreLinux.md
```

## Exercise 3: Insert One File into Another

Open:

```
nano Day4_MoreLinux.md
```

Press:

```
Ctrl + R
```

Enter:

```
takeme.txt
```

This inserts the content of `takeme.txt` into the current Nano document.

Save the file.

> [!tip]  
> This is useful when combining notes, reports, or text files.

---

# 6. Linux User Management

## 6.1 What is a User?

A **user** is an account that allows someone or a service to interact with a Linux system.

Each user has an identity and permissions.

Linux uses user accounts to control access to:

- Files
    
- Directories
    
- Applications
    
- System resources
    

## 6.2 Users and Groups

A **group** is a collection of user accounts used to manage permissions.

Users can belong to one or more groups.

Example:

```
groups
```

Displays the groups of the current user.

```
id
```

Displays the user's UID, GID, and groups.

## 6.3 Types of Users

### Root User

- Username: `root`
    
- UID: `0`
    
- Has extensive administrative privileges.
    

### Normal Users

Normal users have restricted privileges.

> [!important] UID correction  
> The PDF presents normal user IDs as starting from 1–999. This is not a universal rule. UID ranges depend on Linux distribution and configuration. Some system accounts also use nonzero UIDs.

## 6.4 Checking the Current User

### Command

```
whoami
```

Example:

```
gemechu
```

**Purpose:** Display the current effective username.

### Command

```
id
```

Example output:

```
uid=1000(gemechu) gid=1000(gemechu) groups=1000(gemechu),27(sudo)
```

This output is illustrative; your actual UID and groups may differ.

## 6.5 Understanding sudo

**sudo = Superuser Do**

`sudo` allows an authorized user to execute a command with elevated privileges.

### Syntax

```
sudo command
```

Example:

```
sudo apt update
```

This runs the package update command with administrative privileges.

### Why sudo is important

Some operations require administrative permissions, such as:

- Installing software
    
- Creating users
    
- Changing system configuration
    
- Managing system services
    

### Security Principle

Use the least privilege necessary.

Do not execute every command with `sudo`. Normal user permissions are safer for ordinary tasks.

---

# 7. Creating Linux Users

Linux provides commands such as `useradd` and `adduser`.

## 7.1 useradd

### Syntax

```
sudo useradd username
```

Example:

```
sudo useradd student1
```

This creates a user account.

Depending on the distribution and options, it may not automatically create a home directory or configure an interactive password.

### Create a user with a home directory

```
sudo useradd -m student1
```

`-m` creates the user's home directory if it does not exist.

### Set the password

```
sudo passwd student1
```

Enter and confirm the password when prompted.

## 7.2 adduser

### Syntax

```
sudo adduser username
```

Example:

```
sudo adduser student2
```

On Debian-based systems such as Kali and Ubuntu, `adduser` is generally an interactive helper that guides you through account creation.

It normally asks for:

- Password
    
- User information
    
- Confirmation
    

## 7.3 useradd vs adduser

|useradd|adduser|
|---|---|
|Low-level account creation utility|Friendly account-creation helper on Debian-based systems|
|Often requires options for home directory and setup|Usually guides the user interactively|
|Common in scripts and administration|Convenient for beginners|

---

# 8. Linux Account Files

## 8.1 /etc/passwd

The file:

```
/etc/passwd
```

Contains user account information.

View it:

```
cat /etc/passwd
```

Search for a user:

```
grep student1 /etc/passwd
```

Example entry:

```
student1:x:1001:1001:Student:/home/student1:/bin/bash
```

### Structure

```
username:password_placeholder:UID:GID:comment:home_directory:login_shell
```

|Field|Meaning|
|---|---|
|username|Account name|
|x|Password information stored elsewhere|
|UID|User ID|
|GID|Primary group ID|
|comment|User information|
|home directory|User's home path|
|login shell|Shell used by the account|

## 8.2 /etc/shadow

The file:

```
/etc/shadow
```

Stores password-related information, including password hashes and account password aging data.

View it only with appropriate privileges:

```
sudo less /etc/shadow
```

> [!danger] Security  
> `/etc/shadow` contains sensitive authentication information. Never share its contents publicly or copy password hashes into public notes or repositories.

## 8.3 Important Distinction

|File|Information|
|---|---|
|`/etc/passwd`|Account details|
|`/etc/shadow`|Password hashes and password-aging information|

Modern Linux systems do not normally store plaintext passwords in `/etc/passwd`.

---

# 9. Switching to Root

## 9.1 Command

```
sudo su
```

This starts a root shell using sudo authorization.

Check:

```
whoami
```

Expected:

```
root
```

Exit the root shell:

```
exit
```

## 9.2 Safer Alternative

For a single administrative command:

```
sudo command
```

For an interactive root shell, a common alternative is:

```
sudo -i
```

> [!warning]  
> Root privileges can modify almost anything on the system. Mistakes made as root can damage the operating system or destroy data.

---

# 10. Ethical Hacking Application

## 10.1 Why Ethical Hackers Need Linux Filesystem Knowledge

During authorized security assessments, professionals may inspect:

- Configuration files
    
- User accounts
    
- File permissions
    
- System binaries
    
- Logs
    
- Application directories
    

Understanding the filesystem helps identify where relevant information may be stored.

## 10.2 Why User Management Matters

Security professionals investigate:

- Which accounts exist?
    
- Which users have administrative privileges?
    
- Which groups have elevated permissions?
    
- Are unnecessary accounts present?
    
- Are permissions configured correctly?
    
- Are authentication files protected?
    

## 10.3 Security Example: Checking Privileged Groups

```
groups
```

```
id
```

These commands help identify the current user's group memberships.

On many Debian-based systems, membership in the `sudo` group can allow administrative access.

## 10.4 Defensive Lessons

- Use strong authentication.
    
- Remove unnecessary accounts.
    
- Review administrative group membership.
    
- Protect sensitive authentication files.
    
- Apply least privilege.
    
- Avoid unnecessary root sessions.
    
- Maintain appropriate file permissions.
    

---

# 11. Common Mistakes and Troubleshooting

|Mistake|Explanation|Solution|
|---|---|---|
|Confusing `/` with `/root`|They are different directories|Remember filesystem root vs root user's home|
|Typing in VIM without Insert mode|VIM opens in Normal mode|Press `i`|
|Unable to exit VIM|Still in Insert mode|Press `Esc`, then `:q`|
|Losing VIM changes|Quit without saving|Use `:wq`|
|Confusing `Ctrl + O` in Nano|It saves the file|Press `Ctrl + O`, then Enter|
|`useradd` doesn't create home directory|Home creation may require `-m`|Use `sudo useradd -m username`|
|Permission denied|Command lacks required permissions|Check permissions; use sudo only if authorized|
|User cannot use sudo|User may lack sudo authorization|Check group membership and sudo configuration|
|Running every command as root|Increases risk|Use normal user privileges by default|

---

# 12. Quick Revision

## Important Commands

|Command|Purpose|
|---|---|
|`pwd`|Print current directory|
|`ls /`|List root directory|
|`cd /etc`|Change directory|
|`vim file.txt`|Open VIM|
|`nano file.txt`|Open Nano|
|`whoami`|Show current username|
|`id`|Show UID, GID, and groups|
|`groups`|Show group memberships|
|`sudo command`|Execute an authorized command with elevated privileges|
|`sudo useradd -m username`|Create a user with a home directory|
|`sudo adduser username`|Interactive account creation on Debian-based systems|
|`sudo passwd username`|Set or change a user's password|
|`cat /etc/passwd`|Display account information|
|`sudo less /etc/shadow`|Inspect password-related account information|
|`sudo su`|Start a root shell|
|`exit`|Leave the current shell|

## Key Definitions

- **Filesystem:** Structure used to organize files.
    
- **Root directory:** `/`, the starting point of Linux filesystem hierarchy.
    
- **Root user:** Administrative account with UID 0.
    
- **UID:** User ID.
    
- **GID:** Group ID.
    
- **sudo:** Tool for running authorized commands with elevated privileges.
    
- **VIM:** Powerful modal text editor.
    
- **Nano:** Beginner-friendly command-line text editor.
    
- **Home directory:** Personal directory assigned to a user.
    

## One-Minute Summary

Linux uses a hierarchical filesystem beginning at `/`. Important directories include `/etc`, `/home`, `/usr`, `/boot`, and `/tmp`.

VIM is a modal editor that uses Normal and Insert modes. Nano is easier for beginners because typing starts immediately.

Linux user management uses accounts, groups, UIDs, and permissions. The root account has UID 0. `sudo` allows authorized users to execute administrative commands. `/etc/passwd` contains account information, while `/etc/shadow` contains sensitive password-related information.

---

# 13. Practice Questions

## A. Multiple Choice

### 1. Which directory is the root of the Linux filesystem?

A. `/home`  
B. `/root`  
C. `/`  
D. `/etc`

### 2. Which command displays the current username?

A. `pwd`  
B. `whoami`  
C. `groups`  
D. `ls`

### 3. Which VIM key enters Insert mode?

A. `Esc`  
B. `i`  
C. `q`  
D. `u`

### 4. Which file contains password hashes on modern Linux systems?

A. `/etc/passwd`  
B. `/etc/group`  
C. `/etc/shadow`  
D. `/home`

### 5. What is the UID of the root user?

A. 1  
B. 1000  
C. 999  
D. 0

## B. Practical Exercises

### Exercise 1: File Creation

Create a file named `linux_practice.txt` using Nano.

Write:

```
I am learning Linux Fundamentals.
Linux is important for Ethical Hacking.
```

Save and verify the contents.

### Exercise 2: User Information

Run:

```
whoami
id
groups
```

Write down what each command displays.

### Exercise 3: User Creation

In your authorized Kali Linux virtual machine:

```
sudo useradd -m labuser
sudo passwd labuser
```

Verify the account:

```
grep labuser /etc/passwd
```

Do not perform account changes on systems you do not administer.

## C. Critical Thinking

1. Why should an ethical hacker understand `/etc`, `/home`, and `/usr` before performing a Linux security assessment?
    
2. Why is using a normal user account safer than working permanently as root?
    

---

# 14. Answer Key

## Multiple Choice Answers

|Question|Answer|Explanation|
|---|---|---|
|1|C|`/` is the filesystem root|
|2|B|`whoami` prints the effective username|
|3|B|`i` enters Insert mode|
|4|C|`/etc/shadow` contains password-related information|
|5|D|Root has UID 0|

## Critical Thinking Answers

### 1. Filesystem Knowledge

Understanding the filesystem helps security professionals locate configuration files, user data, system programs, and other relevant information during authorized investigations.

### 2. Least Privilege

Using a normal account limits the impact of mistakes. Root privileges should be used only when necessary because administrative commands can change critical system files and settings.

---

# 15. Obsidian Internal Links

Related notes:

- [[Linux Fundamentals]]
    
- [[Linux File System]]
    
- [[Linux Commands]]
    
- [[Linux Permissions]]
    
- [[Linux User Management]]
    
- [[VIM Editor]]
    
- [[Nano Editor]]
    
- [[Linux Privilege Escalation]]
    
- [[Network Security]]
    
- [[Ethical Hacking Fundamentals]]
    

Tags:

#linux #cybersecurity #ethical-hacking #linux-fundamentals #vim #nano #user-management

---

# 16. Final Study Checklist

- I understand Linux filesystem hierarchy.
    
- I can explain `/`, `/root`, `/home`, and `/etc`.
    
- I can create and edit files using VIM.
    
- I can create and edit files using Nano.
    
- I know how to save and exit both editors.
    
- I understand users, groups, UID, and GID.
    
- I can use `whoami`, `id`, and `groups`.
    
- I understand the purpose of `sudo`.
    
- I can create a user in my Kali VM.
    
- I understand `/etc/passwd` and `/etc/shadow`.
    
- I understand why root access must be used carefully.
    

> [!success] Learning Principle  
> Do not just read the commands. Execute them in your Kali Linux virtual machine, observe the output, explain what happened, and repeat until you can perform each task without looking at the note.