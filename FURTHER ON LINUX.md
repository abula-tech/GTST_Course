# Further on Linux --- Day 4

> GTST Course | Linux Fundamentals  
> Source: Further on Linux.pdf

## 1. Linux File Hierarchy

### What is a filesystem?

A filesystem is the directory structure used by an operating system to  
organize files and directories.

- Windows commonly uses drive letters such as `C:`.
- Linux organizes files under one main directory called `/` (root).
- Every file and directory in Linux starts from `/`.

### Root directory vs root user

- `/` --- the root of the entire filesystem.
- `/root` --- the home directory of the root user.
- `root` --- the superuser account, usually UID `0`.

**Remember:** `/` and `/root` are different.

### Important Linux directories

Directory Purpose

---

`/` Top of the filesystem hierarchy  
`/bin` Essential command binaries (e.g., `ls`, `cp`, `cat`, `pwd`)  
`/boot` Boot files, including kernel and bootloader-related files  
`/dev` Device files representing devices and interfaces  
`/etc` System-wide configuration files  
`/home` Home directories for normal users  
`/lib` Essential shared libraries and kernel-related modules  
`/media` Common mount point for removable media  
`/mnt` Temporary mount point often used by administrators  
`/opt` Optional/add-on application software  
`/sbin` System administration binaries  
`/tmp` Temporary files  
`/usr` User applications, utilities, libraries, and documentation

### Important subdirectories under `/usr`

- `/usr/bin` --- many user commands and programs.
- `/usr/sbin` --- many system-administration commands.
- `/usr/lib` --- libraries used by programs.
- `/usr/src` --- source code, including kernel source when installed.

### Useful commands to explore the hierarchy

```
ls /
ls /etc
ls /home
pwd
```

To inspect a directory with details:

```
ls -l /etc
```

> Modern Linux distributions may merge `/bin`, `/sbin`, and `/lib` into  
> `/usr` through symbolic links. Their traditional purposes are still  
> useful to learn.

---

## 2. Linux Text Editors

Text editors are programs used to create and modify text files.

### Command-line editors

- Vim
- Nano
- Emacs
- Neovim

### Graphical editors

- VS Code
- Gedit
- Sublime Text
- Pluma

---

## 3. VIM Editor

VIM means **Vi IMproved**. It is a powerful terminal text editor.

### Open or create a file

```
vim filename.txt
```

### VIM modes

Mode Purpose

---

Normal/Command mode Navigate and run editing commands  
Insert mode Type or insert text  
Command-line mode Enter commands such as save and quit

### Essential VIM workflow

1. Open a file: `vim notes.txt`
2. Press `i` to enter Insert mode.
3. Type your text.
4. Press `Esc` to return to Normal mode.
5. Type `:w` and press Enter to save.
6. Type `:q` and press Enter to quit.

### Important VIM commands

Command Meaning

---

`i` Enter Insert mode  
`Esc` Return to Normal mode  
`:w` Save  
`:q` Quit  
`:wq` Save and quit  
`:q!` Quit without saving changes  
`u` Undo  
`Ctrl+r` Redo

**Note:** `:wq!` saves and quits with force; `!` is not normally  
necessary if you have permission.

### Example

```
vim takeme.txt
```

Inside VIM:

```
i
This is the inserted text from Planet Mars!
Esc
:wq
Enter
```

---

## 4. NANO Editor

Nano is a beginner-friendly terminal text editor.

### Open or create a file

```
nano filename.txt
```

Then type your text directly.

### Useful Nano shortcuts

Shortcut Meaning

---

`Ctrl+O` Write/save file  
`Enter` Confirm filename when saving  
`Ctrl+X` Exit  
`Alt+U` Undo  
`Alt+E` Redo  
`Ctrl+R` Read/insert another file  
`Ctrl+K` Cut current line/selection  
`Ctrl+U` Paste cut text  
`Ctrl+W` Search

In Nano's shortcut notation, `^` means **Ctrl**.

**Important:** Nano's copy/paste shortcuts can vary by terminal.  
`Ctrl+Shift+C` and `Ctrl+Shift+V` are commonly terminal copy/paste  
shortcuts, not Nano's own editing shortcuts.

### Example

```
nano Day4_MoreLinux.md
```

Write:

```
This is Day 4 course note.
```

Save with `Ctrl+O`, press Enter, then exit with `Ctrl+X`.

---

## 5. Linux User Management

A **user** is an account that can access a computer system. Linux users  
have user IDs (UIDs), groups, files, and permissions.

### Types of users

- **Root user:** UID `0`; superuser with extensive administrative  
    privileges.
- **Normal users:** Usually have nonzero UIDs. Exact UID ranges depend  
    on the distribution and configuration.

### Check the current user

```
whoami
```

### Run a command with administrative privileges

```
sudo command
```

Example:

```
sudo apt update
```

`sudo` allows an authorized user to execute a command with elevated  
privileges. It does not automatically make every user a sudo  
administrator.

### Create users

```
sudo useradd username
```

or, on Debian/Kali systems:

```
sudo adduser username
```

- `useradd` --- command-line utility for creating a user; often  
    requires options for a complete setup.
- `adduser` --- interactive helper that guides you through creating a  
    user and setting a password.

Example:

```
sudo adduser student
```

### User account files

---

File Purpose

---

`/etc/passwd` User account information; passwords  
are not stored here in modern  
systems

## `/etc/shadow` Password hashes and  
password-related aging information;  
access is restricted

Inspect account information:

```
cat /etc/passwd
```

Search for a specific account:

```
grep '^student:' /etc/passwd
```

> Never share password hashes or sensitive account information  
> unnecessarily.

### Switch to a root shell

```
sudo su
```

Exit the root shell:

```
exit
```

**Security principle:** Use normal user privileges for everyday work.  
Use `sudo` only when needed. Avoid running commands as root without  
understanding their effect.

---

## 6. Practical Exercises

### Exercise 1 --- Create a file using VIM

```
vim takeme.txt
```

Insert:

```
This is the inserted text from Planet Mars!
```

Save and exit using `:wq`.

### Exercise 2 --- Create a Markdown note using Nano

```
nano Day4_MoreLinux.md
```

Write:

```
This is Day 4 course note.
```

Save and exit.

### Exercise 3 --- Insert another file into Nano

Open the destination:

```
nano Day4_MoreLinux.md
```

Move the cursor where you want the content, then press `Ctrl+R` and  
enter:

```
takeme.txt
```

Save the destination file.

### Exercise 4 --- Practice user commands

```
whoami
id
cat /etc/passwd
```

If you have permission and a suitable practice environment:

```
sudo adduser practiceuser
```

---

## 7. Additional Commands Worth Learning

### `id` --- display user and group IDs

```
id
id username
```

### `groups` --- show group membership

```
groups
groups username
```

### `getent` --- query account databases

```
getent passwd username
getent group groupname
```

### `su` --- switch user

```
su username
```

### `sudo -l` --- check allowed sudo commands

```
sudo -l
```

---

## 8. Cybersecurity Connection

Linux user management is important for system security.

- **Least privilege:** Give users only the permissions they need.
- **Account auditing:** Review accounts and group memberships.
- **Privilege escalation awareness:** Unexpected administrative  
    privileges can be a security risk.
- **Configuration security:** Protect files under `/etc`.
- **Password security:** `/etc/shadow` is restricted because it  
    contains password hashes and related information.

Useful investigation commands:

```
whoami
id
groups
sudo -l
ls -l /etc/passwd /etc/shadow
```

---

## 9. Quick Revision

- Linux filesystem begins at `/`.
- `/root` is the root user's home directory.
- `/etc` contains configuration files.
- `/home` contains normal users' home directories.
- `/dev` contains device files.
- `/tmp` is used for temporary files.
- VIM: `i` to insert, `Esc` to return, `:wq` to save and quit.
- Nano: `Ctrl+O` to save, `Ctrl+X` to exit.
- `whoami` shows the current username.
- `id` shows UID, GID, and groups.
- Root user has UID `0`.
- `sudo` runs an authorized command with elevated privileges.
- `/etc/passwd` stores account information.
- `/etc/shadow` stores password hashes and password-aging information.

---

## 10. Self-Test

Try answering without looking at the notes:

1. What is the difference between `/` and `/root`?
2. Which directory contains system configuration files?
3. Where are normal users' home directories stored?
4. What does `Esc` do in VIM?
5. Which VIM command saves and quits?
6. Which Nano shortcut saves a file?
7. What does `whoami` display?
8. What is the UID of root?
9. What is the difference between `/etc/passwd` and `/etc/shadow`?
10. Why should you avoid using root privileges for everyday tasks?

---

## 11. Practice Discipline

- Repeat every command in your Kali terminal.
- Create your own examples instead of only copying.
- Explain each command in one sentence.
- Commit your notes to GitHub after reviewing them.
- Practice in a VM or lab environment before changing important system  
    files.

**Next step:** Review the Linux filesystem and editor commands, then  
practice user management in your Kali VirtualBox VM.