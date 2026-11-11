# 🐧 Linux Fundamentals — Final Class

> **Course:** GeezTech Security Training  
> **Topic:** Finishing for Linux  
> **Purpose:** Linux command mastery for cybersecurity and ethical hacking

---

## 1. Script Installation & Dependencies

### Git Clone

Download a GitHub repository:

```
git clone <repository-url>
```

Example:

```
git clone https://github.com/lc/gau
```

### Dependencies

Dependencies are libraries/modules required for a program to work.

|Language|Installation|
|---|---|
|Python|`pip install package`|
|Python requirements|`pip install -r requirements.txt`|
|Go|`go install package`|
|Ruby|`gem install package`|

**Important:** Python projects may require a virtual environment to avoid dependency conflicts.

---

## 2. Linux Help System

### Manual

```
man ls
```

- `man` = manual
    
- Arrow keys = navigate
    
- `q` = quit
    

### Help Options

```
ls --help
```

Some commands support:

```
command -h
command --help
```

**Remember:** Use `man` when you need detailed documentation.

---

## 3. Processes & Process Management

### What is a Process?

A process is a running instance of a program.

- **PID:** Process ID
    
- **Foreground:** Runs in the terminal and occupies it.
    
- **Background:** Runs without occupying the terminal.
    

### View Processes

```
ps
ps -A
ps -u username
```

|Command|Purpose|
|---|---|
|`ps`|Processes in current terminal|
|`ps -A`|All processes|
|`ps -u username`|Processes owned by a user|
|`top`|Live process monitoring|
|`htop`|Interactive process monitoring|

### Kill & Control Processes

```
kill PID
kill -9 PID
```

Important signals:

|Signal|Number|Meaning|
|---|---|---|
|SIGSTOP|19|Stop process|
|SIGCONT|18|Resume process|
|SIGKILL|9|Force kill|

Examples:

```
kill -19 1234
kill -18 1234
kill -9 1234
```

**Warning:** `kill -9` should be a last resort because the process cannot clean up normally.

### htop

```
htop
```

- Search for a process.
    
- Select the process.
    
- Press `F9` to send a signal.
    
- Select the appropriate signal.
    

---

## 4. Foreground & Background Jobs

### Run in Background

```
command &
```

### Suspend a Running Job

```
Ctrl + Z
```

### Resume in Foreground

```
fg
```

### Resume in Background

```
bg
```

### Stop a Command

```
Ctrl + C
```

**Difference:**

- `Ctrl+C` → Interrupt command.
    
- `Ctrl+Z` → Suspend command.
    

---

## 5. Linux Redirection & /dev/null

### Standard Streams

|Stream|File Descriptor|Meaning|
|---|---|---|
|STDIN|0|Standard input|
|STDOUT|1|Standard output|
|STDERR|2|Standard error|

### Redirect Output

```
command > output.txt
```

### Redirect Errors

```
command 2> errors.txt
```

### Ignore Errors

```
command 2>/dev/null
```

### Ignore All Output

```
command >/dev/null 2>&1
```

### Append Output

```
command >> output.txt
```

**Key concept:** `/dev/null` is a special device that discards anything written to it.

---

## 6. Symbolic Links

### Definition

A symbolic link (symlink) is a shortcut/reference to another file or directory.

### Create Symlink

```
ln -s target link_name
```

Example:

```
ln -s /home/user/file.txt shortcut.txt
```

### Identify Symlink

```
ls -l
```

Symlinks display:

```
shortcut.txt -> /home/user/file.txt
```

**Remember:** `-s` creates a symbolic link.

---

## 7. Aliases

### Definition

An alias gives a short name to a command or command combination.

### Create Alias

```
alias ll='ls -la'
```

Now:

```
ll
```

### Remove Alias

```
unalias ll
```

### Make Alias Permanent

|Shell|Configuration|
|---|---|
|Bash|`~/.bashrc`|
|Zsh|`~/.zshrc`|
|Fish|`~/.config/fish/config.fish`|

For Bash:

```
nano ~/.bashrc
```

Add:

```
alias ll='ls -la'
```

Reload:

```
source ~/.bashrc
```

---

## 8. tmux — Terminal Multiplexer

### Definition

tmux allows you to manage multiple terminal sessions, windows, and panes inside one terminal.

### Start

```
tmux
```

### Important Shortcuts

> Prefix: `Ctrl + A` (if configured as in the handout)

|Action|Shortcut|
|---|---|
|Split horizontally|`Ctrl+A`, then `o`|
|Split vertically|`Ctrl+A`, then `e`|
|Create window|`Ctrl+A`, then `c`|
|Rename window|`Ctrl+A`, then `,`|
|Switch window|`Ctrl+A`, then number|
|Switch pane|`Ctrl+A`, then arrow|
|Close pane|`Ctrl+A`, then `x`|

### Configuration

```
nano ~/.tmux.conf
```

Configuration from the handout:

```
unbind C-b
unbind l
set -g prefix C-a
unbind %
bind e split-window -h
bind o split-window -v
set -g base-index 1
setw -g pane-base-index 1
```

**Note:** `Ctrl+A` is the prefix key.

---

## 9. wget — Download Files

### Definition

`wget` downloads files from websites or servers.

### Syntax

```
wget URL
```

Example:

```
wget https://example.com/file.pdf
```

---

## 10. find — Search Files & Directories

### Definition

`find` searches for files and directories based on specified conditions.

### Syntax

```
find [path] [options] [expression]
```

### Examples

Search by filename:

```
find / -name "linux"
```

Search in home:

```
find /home -name "*.txt"
```

Find files:

```
find . -type f
```

Find directories:

```
find . -type d
```

Find files with permission 777:

```
find /home -perm 777
```

Find files with at least those permissions:

```
find /home -perm -777
```

**Remember:**

- `-name` → Search by name
    
- `-type f` → Files
    
- `-type d` → Directories
    
- `-perm` → Permissions
    

---

## 11. Quick Revision Table

|Command|Function|
|---|---|
|`git clone`|Download repository|
|`pip install`|Install Python package|
|`man`|Read command manual|
|`ps`|View processes|
|`kill`|Send signal to process|
|`top`|Monitor processes|
|`htop`|Interactive process manager|
|`fg`|Bring job to foreground|
|`bg`|Resume job in background|
|`Ctrl+C`|Interrupt command|
|`Ctrl+Z`|Suspend command|
|`/dev/null`|Discard output|
|`ln -s`|Create symbolic link|
|`alias`|Create command shortcut|
|`tmux`|Manage terminal sessions|
|`wget`|Download files|
|`find`|Search files/directories|

---

## 12. Mentor's Practical Advice

### What you must master

- Process management and signals.
    
- Linux input/output redirection.
    
- Finding files efficiently.
    
- Symbolic links and aliases.
    
- Background jobs.
    
- tmux navigation and pane management.
    
- Git repository cloning and dependency installation.
    

### Cybersecurity connection

These skills help you:

- Manage tools and processes.
    
- Install security scripts.
    
- Navigate large filesystems.
    
- Automate repetitive commands.
    
- Manage multiple terminals during security labs.
    

### Final Challenge

Without copying commands, demonstrate:

1. Clone a GitHub repository.
    
2. Find a file using `find`.
    
3. Display running processes using `ps`.
    
4. Open `htop` and identify a PID.
    
5. Run a command in the background.
    
6. Redirect errors to `/dev/null`.
    
7. Create a symbolic link.
    
8. Create a permanent alias.
    
9. Configure tmux.
    
10. Download a file using `wget`.
    

---

> **My standard:** I do not memorize commands blindly. I understand what they do, when to use them, and why they matter.