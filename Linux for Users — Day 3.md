# Linux for Users — Day 3

## 1. Overview of Kali Linux

- Kali Linux is a Debian-based distribution for penetration testing and digital forensics.
    
- It was previously known as BackTrack.
    
- Users can switch between desktop environments.
    

## 2. Kali Linux Tool Categories

1. **Information Gathering:** Collect information about systems, hosts, and networks.
    
2. **Vulnerability Analysis:** Identify security weaknesses.
    
3. **Web Application Analysis:** Analyze website security.
    
4. **Database Assessment:** Assess database security.
    
5. **Password Attacks:** Test password security.
    
6. **Wireless Attacks:** Assess Wi-Fi and other wireless security.
    
7. **Reverse Engineering:** Analyze software and binary files.
    
8. **Exploitation Tools:** Test whether vulnerabilities can be exploited.
    
9. **Sniffing & Spoofing:** Analyze network traffic and test network security.
    
10. **Post Exploitation:** Assess access and security impact after exploitation.
    
11. **Forensics:** Investigate cyber incidents.
    
12. **Reporting Tools:** Prepare security reports.
    
13. **Social Engineering Tools:** Test human-related security weaknesses.
    
14. **System Services:** Start and manage system services.
    
15. **Usually Used Applications:** Perform common tasks.
    

## 3. Desktop and File Managers

- **GNOME, KDE Plasma:** Desktop environments.
    
- **Dolphin, Thunar, Nautilus:** File managers.
    
- **Workspace Manager:** Organizes work across different workspaces.
    

## 4. Linux Terminal

A **terminal** provides access to a shell, where users execute commands to interact with the operating system.

### Terminal Symbols

- `$` — Usually indicates a regular user.
    
- `#` — Usually indicates the root user.
    
- `~` — Home directory.
    
- `.` — Current directory.
    
- `*` — Wildcard matching multiple characters.
    

## 5. Basic Linux Commands

|Command|Purpose|Example|
|---|---|---|
|`ls`|List files and directories|`ls -la`|
|`cd`|Change directory|`cd Documents`|
|`pwd`|Show current directory path|`pwd`|
|`echo`|Display text|`echo "Hello"`|
|`cat`|Display file contents|`cat file.txt`|
|`head`|Show first lines|`head file.txt`|
|`tail`|Show last lines|`tail file.txt`|
|`less`|View a file page by page|`less file.txt`|
|`touch`|Create an empty file or update timestamps|`touch file.txt`|
|`mkdir`|Create a directory|`mkdir linux`|
|`clear`|Clear terminal display|`clear`|
|`rm`|Remove files|`rm file.txt`|
|`cp`|Copy files|`cp a.txt b.txt`|
|`mv`|Move or rename files|`mv a.txt linux/`|
|`grep`|Search text patterns|`grep "hello" file.txt`|
|`wc`|Count lines, words, and bytes|`wc file.txt`|

## 6. Useful Command Options

### `ls`

- `ls -l` — Long listing format.
    
- `ls -a` — Include hidden files.
    
- `ls -R` — List recursively.
    
- `ls -la` — Combine options.
    

### `cd`

- `cd /` — Go to the root directory.
    
- `cd ~` — Go to your home directory.
    
- `cd ..` — Go up one directory.
    
- `cd ../..` — Go up two directories.
    
- `cd "folder name"` — Enter a directory containing spaces.
    

### `echo`

```
echo "Hello" > file.txt
echo "World" >> file.txt
```

- `>` — Write output, replacing existing file contents.
    
- `>>` — Append output to the file.
    

### `rm`

- `rm -i file.txt` — Ask before removal.
    
- `rm -r folder` — Remove a directory recursively.
    
- `rm -f file.txt` — Force removal without prompting.
    

**Warning:** `rm -rf` can delete files and directories recursively without confirmation. Check the path carefully.

### `grep`

- `grep -i "hello" file.txt` — Case-insensitive search.
    
- `grep -n "hello" file.txt` — Show matching line numbers.
    
- `grep -c "hello" file.txt` — Count matching lines.
    
- `grep -l "hello" *` — List matching filenames.
    
- `grep -R "hello" folder/` — Search recursively.
    
- `grep -v "hello" file.txt` — Show lines that do not match.
    

### `wc`

- `wc -l file.txt` — Count lines.
    
- `wc -w file.txt` — Count words.
    
- `wc -c file.txt` — Count bytes.
    

## 7. Running Multiple Commands

### AND (`&&`)

Runs the next command only if the previous command succeeds.

```
mkdir linux && cd linux
```

### OR (`||`)

Runs the next command only if the previous command fails.

```
cd missing || echo "Directory not found"
```

### Pipe (`|`)

Passes the output of one command as input to another.

```
ls -l | less
```

## 8. Important Commands to Study Next

- `sed` — Edit or transform text streams.
    
- `awk` — Process and analyze structured text.
    
- `tee` — Display command output and save it to a file.
    

## Quick Revision

- `pwd` shows the current directory.
    
- `ls -a` displays hidden files.
    
- `grep` searches text.
    
- `wc -w` counts words.
    
- `&&` runs the next command after success.
    
- `||` runs the next command after failure.
    
- `|` passes output to another command.
    
- `>` overwrites; `>>` appends.