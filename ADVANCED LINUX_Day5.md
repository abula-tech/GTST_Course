# Advanced Linux User — Day 5

> GTST Course | Linux Fundamentals  
> Source: Advanced Linux User!.pdf

## 1. Further User Management

### Change a user's password

```
sudo passwd username
```

Example: `sudo passwd gtst`

### Change a user's UID

```
sudo usermod -u NEW_UID username
```

Example: `sudo usermod -u 1923 gtst`

### Delete a user and their home directory

```
sudo userdel -r username
```

**Caution:** `-r` removes the user's home directory and mail spool. Verify the account and data first.

### Switch to another user

```
su - username
```

The `-` starts a login shell and loads that user's login environment.

---

## 2. Sudoers File

The **sudoers** configuration controls which users can run commands with `sudo` and what privileges they receive.

Edit it safely:

```
sudo visudo
```

`visudo` checks syntax before saving. A user may not be able to use sudo because they are not authorized in sudoers or an appropriate administrator group.

On Kali/Debian, a common authorized approach is:

```
sudo usermod -aG sudo username
```

Log out and back in for group membership to take effect.

> Grant administrative access only to trusted users. A sudoers syntax error can break sudo access.

---

## 3. Linux File Ownership and Permissions

Every file and directory has:

- A user owner
- A group owner
- Permissions

View them:

```
ls -l
```

Example:

```
-rwxr-xr-- 1 gemechu students 120 Nov 5 10:00 script.sh
```

The first character indicates type (`-` regular file, `d` directory). The next three characters are owner permissions, the next three group permissions, and the last three other permissions.

### Change ownership

```
sudo chown user:group filename
```

Example:

```
sudo chown gtst:root Perm.txt
```

Only user owner:

```
sudo chown gtst Perm.txt
```

Only group owner:

```
sudo chown :root Perm.txt
```

---

## 4. Permission Types

|Permission|Symbol|File meaning|Directory meaning|
|---|---|---|---|
|Read|`r`|Read contents|List entries|
|Write|`w`|Modify contents|Create/delete/rename entries (normally with execute)|
|Execute|`x`|Run executable|Enter/traverse directory|

Permission categories:

- `u` — user/file owner
- `g` — group owner
- `o` — others
- `a` — all (user, group, others)

---

## 5. CHMOD — Change Permissions

Syntax:

```
chmod MODE filename
```

### Symbolic examples

```
chmod a+x filename   # add execute to all
chmod u+x filename   # add execute to owner
chmod g+x filename   # add execute to group
chmod o+x filename   # add execute to others
chmod a-x filename   # remove execute from all
chmod a+rwx filename # give all rwx
chmod u-rw filename  # remove owner read/write
chmod g-x filename   # remove group execute
chmod o-wx filename  # remove others write/execute
```

### Numeric permissions

|Permission|Value|
|---|---|
|Read (`r`)|4|
|Write (`w`)|2|
|Execute (`x`)|1|

Add values for each category:

- `7 = 4+2+1 = rwx`
- `6 = 4+2 = rw-`
- `5 = 4+1 = r-x`
- `4 = r--`
- `3 = 2+1 = -wx`
- `2 = -w-`
- `1 = --x`
- `0 = ---`

Examples:

```
chmod 621 filename
chmod 777 filename
chmod 640 filename
chmod 755 filename
```

`chmod 621` means owner `rw-`, group `-w-`, others `--x`. `chmod 777` gives everyone `rwx`; avoid it as a routine fix because it grants broad access.

### Numeric to symbolic

|Numeric|Symbolic|
|---|---|
|`631`|`rw- -wx --x`|
|`200`|`-w- --- ---`|
|`755`|`rwx r-x r-x`|
|`640`|`rw- r-- ---`|

---

## 6. Special File Permissions

The course covers three special bits:

|Bit|Numeric prefix|Purpose|
|---|---|---|
|SUID|`4` (e.g. `4755`)|Executable runs with file owner's effective UID|
|SGID|`2` (e.g. `2755`)|Executable runs with file group's effective GID; on directories, new entries commonly inherit the directory group|
|Sticky bit|`1` (e.g. `1777`)|In shared directories, restricts deletion/renaming to entry owner, directory owner, or privileged user|

SUID/SGID programs can create privilege risks if misconfigured or vulnerable. Do not set special bits on random programs.

Inspect permissions:

```
ls -l
```

Authorized system audit:

```
find / -type f -perm -4000 2>/dev/null
find / -type f -perm -2000 2>/dev/null
```

Run such searches only on systems you own or are authorized to inspect.

---

## 7. Software Installation on Linux

Linux package managers install, update, and remove software:

- APT — Debian, Ubuntu, Kali
- Pacman — Arch
- Pkg — FreeBSD

This lesson focuses on APT and DPKG.

A **repository** is a software source/server providing packages and package metadata.

### APT commands

```
sudo apt update                 # refresh package lists
apt search cmatrix              # search for a package
sudo apt install cmatrix        # install
sudo apt remove cmatrix         # remove, generally keep config
sudo apt purge cmatrix          # remove package and package config
sudo apt upgrade                # upgrade installed packages
```

**Remember:** `apt update` refreshes package lists; it does not upgrade installed software. `apt upgrade` upgrades packages based on those lists.

### Package dependencies

A package may require other packages or libraries to work. These are called **dependencies**. APT normally resolves and installs dependencies automatically.

---

## 8. DPKG — Debian Package Manager

DPKG works with local `.deb` files. Unlike APT, it does not automatically resolve dependencies.

```
sudo dpkg -i package.deb       # install local package
sudo dpkg -r package-name      # remove package
sudo dpkg -P package-name      # purge package
```

If installation reports missing dependencies, review the proposed changes before using:

```
sudo apt --fix-broken install
```

---

## 9. Practical Lab: cmatrix

1. Update repository lists:
    
    ```
    sudo apt update
    ```
    
2. Search:
    
    ```
    apt search cmatrix
    ```
    
3. Install:
    
    ```
    sudo apt install cmatrix
    ```
    
4. Run:
    
    ```
    cmatrix
    ```
    
    Press `q` or `Ctrl+C` to exit, depending on version.
5. Remove:
    
    ```
    sudo apt remove cmatrix
    ```
    

---

## 10. Course Exercises

1. Create `Perm.txt`.
2. Give it the permissions specified by your instructor.
3. Convert numeric `631` to symbolic.
4. Convert numeric `200` to symbolic.
5. In a lab VM, create users `gtst` and `test` and set passwords as instructed.
6. Change `Perm.txt` user owner to `gtst` and group owner to `root`.
7. Change the password of `gtst`.
8. Change the UID of `gtst` to `1923`.
9. Delete user `test`.

Example commands (lab VM only):

```
sudo adduser gtst
sudo adduser test
sudo chown gtst:root Perm.txt
sudo passwd gtst
sudo usermod -u 1923 gtst
sudo userdel -r test
```

Use disposable test accounts. UID changes can affect file ownership; do not do this on important systems without checking.

---

## 11. Quick Revision

- `passwd` changes a user's password.
- `usermod -u` changes a user's UID.
- `userdel -r` deletes a user and home directory.
- `su - username` switches to a login shell.
- `visudo` safely edits sudoers.
- `ls -l` displays permissions and ownership.
- `chown` changes ownership; `chmod` changes permissions.
- `r=4`, `w=2`, `x=1`.
- `u`, `g`, `o`, `a` mean user, group, other, all.
- SUID, SGID, sticky are special permission bits.
- `apt update` refreshes package lists; `apt upgrade` upgrades installed packages.
- `apt remove` keeps package configuration in general; `apt purge` removes it.
- `dpkg -i` installs a local `.deb` package.

---

## 12. Self-Test

Try answering without looking:

1. What does `sudo visudo` do?
2. Difference between `chown` and `chmod`?
3. What does `rwx` mean?
4. Numeric value of `r-x`?
5. What does `chmod 640 file` mean?
6. What is SUID?
7. Why can SUID programs be security-sensitive?
8. Difference between `apt update` and `apt upgrade`?
9. Difference between `apt remove` and `apt purge`?
10. Difference between APT and DPKG?

---

## 13. Practice Rules

- Change permissions only on files you created.
- Check results with `ls -l`.
- Don't use `chmod 777` without understanding the risk.
- Never edit sudoers without `visudo`.
- Use test accounts in your Kali VM.
- Read APT's proposed changes before confirming.
- Commit reviewed notes to GitHub.

**Next step:** Practice `chmod`, `chown`, APT, and user-management commands in your Kali VirtualBox lab.