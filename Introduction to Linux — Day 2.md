# Introduction to Linux — Day 2

## 1. What is Linux?

- **Linux:** An open-source kernel.
    
- **Kernel:** Connects software and hardware and manages computer resources.
    
- **Operating System (OS):** Software that manages computer hardware and runs applications.
    

## 2. History of Linux

- **1969:** UNIX was developed by a team led by Ken Thompson and Dennis Ritchie.
    
- **1983:** Richard Stallman announced the GNU project.
    
- **1991:** Linus Torvalds created the Linux kernel.
    
- **GNU + Linux:** Together provide a complete operating system.
    

## 3. What is a Shell?

A **shell** is a command-line interpreter that lets users communicate with the operating system by entering commands.

### Types of Shells

- `sh` — Bourne shell
    
- `bash` — Bourne Again Shell
    
- `zsh` — Z Shell
    
- `fish` — Friendly Interactive Shell
    

**Check your current shell:**

```
echo $SHELL
```

## 4. Main OS Components

- **Kernel:** Manages hardware and system resources.
    
- **Software:** Programs used to perform tasks.
    
- **Desktop Environment (DE):** Provides the graphical desktop interface.
    
- **Window Manager:** Controls window placement, size, and appearance.
    
- **File Extensions:** Indicate file types, such as `.txt` and `.pdf`.
    

## 5. Linux Desktop Environments

- **MATE:** Traditional, lightweight desktop.
    
- **GNOME:** Modern desktop with animations.
    
- **KDE Plasma:** Highly customizable desktop.
    
- **XFCE:** Lightweight and suitable for lower-resource computers.
    

**Window manager example:** `i3`

## 6. Why Use Linux?

- Can run efficiently on many computers.
    
- Widely used on servers and in software development.
    
- Provides many cybersecurity and digital-forensics tools.
    
- Open-source and customizable.
    
- Supports many distributions.
    

## 7. Linux Distributions (Distros)

A **Linux distribution** combines the Linux kernel with system software and other tools.

Examples:

- **Debian-based:** Ubuntu, Kali Linux, Parrot OS
    
- **Arch-based:** Garuda Linux, BlackArch
    
- **Other distributions:** Fedora, Red Hat, Gentoo
    
- **Android:** Uses the Linux kernel.
    

## 8. Cybersecurity Linux Distros

- **Kali Linux:** Penetration testing and digital forensics.
    
- **Parrot OS:** Security, privacy, and development.
    
- **BlackArch:** Security-focused Arch-based distribution.
    
- **Garuda Linux:** Arch-based general-purpose distribution.
    

### Package Managers and Shells

|Distribution|Package Manager|Shell in the slides|
|---|---|---|
|Kali Linux|`apt`|`zsh`|
|Parrot OS|`apt`|`bash`|
|Garuda Linux|`pacman`|`fish`|

## 9. Ways to Use Linux

1. **Main OS:** Linux is the primary operating system.
    
2. **Dual Boot:** Install Linux alongside another OS.
    
3. **Live Boot:** Run Linux from a bootable USB.
    
4. **Cloud Terminal:** Access a Linux terminal online.
    
5. **Virtual Machine (VM):** Run Linux inside another OS.
    
6. **WSL 2:** Run a Linux environment on Windows.
    
7. **Termux:** Run Linux-like command-line tools on Android.
    

## 10. Virtualization

**Virtualization** allows one physical computer to run virtual machines.

Examples of virtualization software:

- VirtualBox
    
- VMware
    
- Hyper-V
    
- QEMU
    

**Check virtualization on Windows:**

1. Open Task Manager.
    
2. Select Performance.
    
3. Select CPU.
    
4. Check whether **Virtualization** is enabled.
    

## Key Terms to Remember

- **Kernel:** Manages hardware and system resources.
    
- **Shell:** Interprets user commands.
    
- **OS:** Manages the computer and runs applications.
    
- **Distro:** A complete Linux-based operating system distribution.
    
- **DE:** Provides a graphical desktop interface.
    
- **VM:** A virtual computer running inside a physical computer.
    
- **WSL 2:** Runs a Linux environment on Windows.
    

## Quick Revision

- Command to identify your shell: `echo $SHELL`
    
- Kali Linux is based on: Debian
    
- Kali Linux package manager: `apt`
    
- Lightweight desktop examples: XFCE and MATE
    
- Linux kernel creator: Linus Torvalds
    
- GNU project founder: Richard Stallman