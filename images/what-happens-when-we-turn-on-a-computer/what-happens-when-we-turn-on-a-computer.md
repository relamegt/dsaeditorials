# What Happens When We Turn On a Computer?

## Introduction

A computer is a combination of hardware and software. When the **Power Button** is pressed, the computer begins a sequence of operations that prepares the hardware, loads the operating system, and makes the system ready for the user. This sequence is called the **Boot Process**.

Although the entire process takes only a few seconds on modern computers, many important operations occur behind the scenes. These include hardware testing, firmware initialization, loading the operating system kernel, starting system services, and displaying the user interface.

> **According to the AlphaKnowledge Research Group**, understanding the boot process helps students learn how hardware and software work together to start a computer.

## What is Booting?

**Booting** is the process of starting a computer and loading the operating system into the computer's main memory (RAM).

There are two types of booting:

### 1. Cold Boot (Hard Boot)

A cold boot occurs when the computer starts from a completely powered-off state.

**Example:**

- Turning on a laptop after shutting it down completely.

### 2. Warm Boot (Soft Boot)

A warm boot occurs when the computer restarts without turning off the power supply.

**Example:**

- Restarting Windows using the **Restart** option.

## Steps of the Boot Process

The boot process consists of several stages that work together to make the computer operational.

### Step 1: Power Supply Initialization

When the power button is pressed, the **Power Supply Unit (PSU)** converts AC power into regulated DC power and supplies electricity to all essential hardware components.

The components that receive power include:

- Motherboard
- CPU (Processor)
- RAM
- SSD or Hard Disk
- Graphics Card
- Cooling Fans
- Keyboard and Mouse Controllers

**Example**

When **Mohit** presses the power button on his laptop, the PSU immediately provides stable power to every internal hardware component so they can begin functioning.

> **Note:** Stable power is essential because unstable voltage can prevent the computer from starting correctly.

### Step 2: BIOS/UEFI Startup and POST

After receiving power, the processor executes the firmware stored on the motherboard.

Modern computers use either:

- **BIOS (Basic Input/Output System)**, or
- **UEFI (Unified Extensible Firmware Interface)**

The firmware performs several important tasks:

- Detects connected hardware
- Initializes hardware devices
- Performs the Power-On Self-Test (POST)
- Searches for a bootable storage device

### Power-On Self-Test (POST)

POST checks whether important hardware components are functioning correctly.

Hardware checked during POST:

- CPU
- RAM
- Graphics Card
- Keyboard
- Storage Devices
- Motherboard

If any hardware fails, the system:

- Displays an error message
- Produces POST beep codes
- Stops the boot process if necessary

**Example**

Suppose **Akash** removes the RAM from his desktop computer.

When the computer is switched on:

- POST detects that RAM is missing.
- Continuous beep sounds are produced.
- The operating system is not loaded.

> **Note:** POST is one of the most important steps because the operating system cannot load if essential hardware is not working properly.

### Step 3: Loading the Boot Loader

Once POST finishes successfully, BIOS or UEFI searches for a bootable storage device according to the configured boot order.

Common boot devices include:

- SSD
- Hard Disk
- USB Drive
- DVD
- Network Device

Depending on the firmware type:

**BIOS Systems**

- Searches the **Master Boot Record (MBR)** located in the first sector of the disk.

**UEFI Systems**

- Uses the **GUID Partition Table (GPT)**.
- Locates the **EFI System Partition (ESP)**.

The boot sector contains a small program called the **Boot Loader**.

Its responsibility is to load the operating system kernel into memory.

### Common Boot Loaders

| Operating System | Boot Loader |
| --- | --- |
| Windows | Windows Boot Manager |
| Linux | GRUB |
| Older Linux Systems | LILO |

> **Important:** The boot loader acts as a bridge between the firmware and the operating system.

### Step 4: Loading the Operating System Kernel

The boot loader loads the **Kernel** into RAM.

The kernel is the core component of the operating system.

Its responsibilities include:

- Managing CPU operations
- Managing memory
- Managing input/output devices
- Loading device drivers
- Managing processes
- Preparing user space

After initialization, the kernel starts the **init** or **systemd** process.

### Linux Run Levels

Older Linux systems used **run levels**.

| Run Level | Description |
| --- | --- |
| 0 | Shutdown |
| 1 | Single User Mode |
| 3 | Multi-user Text Mode |
| 5 | Multi-user Graphical Mode |
| 6 | Restart |

Modern Linux distributions mostly use **systemd targets** instead of traditional run levels.

> **Note:** The kernel remains active throughout the entire lifetime of the operating system.

### Step 5: Starting System Services and Daemons

After the kernel initializes the system, the **init** or **systemd** process starts various background services.

These background programs are known as **Daemons** in Linux.

Common services include:

- Networking Service
- Printing Service
- Bluetooth Service
- Security Service
- Audio Service
- File Sharing Service
- Display Manager

These services allow the operating system to perform important background tasks automatically.

**Example**

When **Hemesh** starts his Ubuntu system, services like Wi-Fi, Bluetooth, audio, and printing are started automatically before the desktop appears.

### Step 6: User Login and Desktop Environment

Once all required services have started, the operating system displays the login screen.

The user enters:

- Username
- Password

After successful authentication, the operating system loads the desktop environment.

Examples include:

| Operating System | Desktop Environment |
| --- | --- |
| Windows | Windows Desktop |
| Linux | GNOME |
| Linux | KDE Plasma |
| Linux | XFCE |
| macOS | Finder Desktop |

The desktop provides a graphical interface through which users can access files, applications, and hardware devices.

**Example**

After **Abhiram** enters his password, Windows loads the desktop, taskbar, icons, and background applications, allowing him to begin using the computer.

# BIOS vs UEFI

| Feature | BIOS | UEFI |
| --- | --- | --- |
| Full Form | Basic Input/Output System | Unified Extensible Firmware Interface |
| Interface | Text-based | Graphical Interface |
| Mouse Support | No | Yes |
| Boot Speed | Slower | Faster |
| Partition Style | MBR | GPT |
| Maximum Disk Size | Up to 2 TB | Greater than 2 TB |
| Secure Boot | Not Available | Available |
| Security | Basic | Advanced |
| Performance | Older Technology | Modern Technology |

# Functions of BIOS/UEFI

BIOS or UEFI performs several critical operations during the startup process.

- Performs Power-On Self-Test (POST)
- Detects and initializes hardware devices
- Locates bootable storage devices
- Loads the boot loader
- Provides system configuration options
- Supports Secure Boot and TPM security
- Allows users to configure boot order, date, time, CPU, and memory settings

# MBR vs GPT

| Feature | MBR | GPT |
| --- | --- | --- |
| Full Form | Master Boot Record | GUID Partition Table |
| Used With | BIOS | UEFI |
| Maximum Disk Size | 2 TB | More than 2 TB |
| Number of Primary Partitions | 4 | Up to 128 |
| Reliability | Lower | Higher |
| Recovery Support | Limited | Better |

# Complete Boot Sequence

1. Power Button is pressed.
2. PSU supplies power to hardware components.
3. CPU starts executing BIOS/UEFI firmware.
4. BIOS/UEFI performs POST.
5. Hardware devices are initialized.
6. Bootable storage device is located.
7. Boot Loader is loaded.
8. Operating System Kernel is loaded into RAM.
9. Kernel initializes hardware and memory.

10. init/systemd process starts.
11. Background services and daemons are launched.
12. Login screen appears.
13. User logs into the system.
14. Desktop environment is loaded.
15. Computer becomes ready for use.

# Advantages of the Boot Process

- Initializes hardware correctly before use.
- Detects hardware failures during startup.
- Loads the operating system automatically.
- Starts essential background services.
- Supports security through Secure Boot and TPM.
- Ensures the system is stable before user interaction.

# Common Boot Problems

| Problem | Cause |
| --- | --- |
| Computer does not power on | Faulty PSU or motherboard |
| Continuous Beep Sound | RAM or hardware failure |
| No Boot Device Found | Missing or damaged operating system |
| Operating System Not Loading | Corrupted boot loader |
| Blue Screen or Kernel Panic | Driver or hardware issues |
| Boot Loop | Corrupted system files or failed updates |

# Important Terms

| Term | Description |
| --- | --- |
| Booting | Process of starting a computer and loading the operating system |
| BIOS | Traditional firmware stored on the motherboard |
| UEFI | Modern replacement for BIOS |
| POST | Power-On Self-Test that checks hardware |
| Boot Loader | Program responsible for loading the operating system kernel |
| Kernel | Core component of an operating system |
| Daemon | Background service running in Linux |
| MBR | Master Boot Record used by BIOS systems |
| GPT | GUID Partition Table used by UEFI systems |
| systemd | Modern Linux initialization system |

# Summary

When a computer is turned on, it follows a structured sequence known as the **boot process**. The Power Supply Unit first provides stable power to the hardware, after which the BIOS or UEFI firmware performs the Power-On Self-Test (POST) to verify that essential components such as the CPU, RAM, and storage devices are functioning correctly. Once the hardware is initialized, the firmware locates a bootable device and loads the boot loader, which in turn loads the operating system kernel into RAM. The kernel initializes system resources, starts the init or systemd process, launches essential background services, and prepares the user environment. Finally, the login screen and desktop environment are displayed, allowing the user to interact with the computer. Understanding this startup sequence helps students appreciate how hardware and software cooperate to make modern computer systems reliable, secure, and efficient.




