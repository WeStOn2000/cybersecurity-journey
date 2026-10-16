# 🛡️ Operating System Fundamentals

**Platform:** TryHackMe  
**Topics:** Operating Systems, OS Responsibilities, Kernel Space, User Space, GUI, and CLI

---

## 1. Introduction to Operating Systems

### What is an Operating System?

An Operating System (OS) is system software that manages computer hardware, software resources, and provides services for applications.

The OS acts as an intermediary between users, applications, and hardware.

### Examples of Operating Systems

| Operating System | Common Uses |
|---|---|
| Windows | Personal computers, gaming, enterprise |
| Linux | Servers, cybersecurity, cloud computing |
| macOS | Apple computers |
| Android | Smartphones and tablets |
| iOS | Apple mobile devices |

### Practical Example: My Cybersecurity Lab

My cybersecurity lab consists of:

- **Host OS:** Windows 11
- **Guest OS:** Ubuntu Linux
- **Hypervisor:** Oracle VirtualBox
- **Purpose:** Cybersecurity training and experimentation

---

## 2. Responsibilities of an Operating System

An operating system manages several important aspects of a computer.

### 2.1 Process Management

A **process** is a running instance of a program.

The operating system manages processes by:

- Allocating CPU time
- Scheduling process execution
- Managing process creation and termination
- Coordinating access to system resources

**Example:** Running Firefox and the Ubuntu terminal simultaneously.

### 2.2 Memory Management

Memory management controls how RAM is allocated to applications.

The operating system:

- Allocates memory to processes
- Tracks memory usage
- Reclaims unused memory
- Helps prevent unauthorized memory access

**Cybersecurity relevance:** Memory protection helps prevent applications from accessing sensitive information belonging to other processes.

### 2.3 File System Management

The operating system manages files, directories, storage devices, and file permissions.

Examples of Linux commands:

```bash
ls
cd ~/Downloads
mkdir cybersecurity
pwd
```

**Command definitions:**

- `ls` — Lists directory contents.
- `cd` — Changes the current directory.
- `mkdir` — Creates a directory.
- `pwd` — Displays the current working directory.

### 2.4 Device Management

The operating system communicates with hardware through device drivers.

Examples include:

- Keyboards
- Storage devices
- Displays
- Network adapters
- Printers

A **device driver** is software that allows the operating system to communicate with a hardware device.

### 2.5 Security and Access Control

The operating system protects resources through:

- User authentication
- File permissions
- Process isolation
- Privilege management
- Access control policies

**Cybersecurity relevance:** Understanding operating system permissions helps security professionals investigate unauthorized access and privilege escalation.

---

## 3. Kernel Space vs. User Space

Operating systems separate execution into different privilege levels to protect critical system resources.

### 3.1 Kernel Space

**Kernel space** is the privileged execution environment where the operating system kernel operates.

The kernel is the core component of an operating system.

It manages critical resources and performs privileged operations.

#### Kernel Responsibilities

- Managing memory
- Scheduling processes
- Handling hardware interrupts
- Managing device drivers
- Enforcing security boundaries
- Providing system calls

**Important:** Kernel code has elevated privileges and can access protected system resources.

A vulnerability in the kernel can have serious security consequences.

### 3.2 User Space

**User space** is the restricted execution environment where most applications operate.

Examples include:

- Firefox
- Terminal applications
- Text editors
- OpenVPN
- Python programs

Applications normally cannot directly access protected kernel memory or perform privileged hardware operations.

Instead, they request services from the kernel.

### 3.3 System Calls

A **system call** is a controlled mechanism that allows an application to request services from the operating system kernel.

For example, Firefox uses operating system services to communicate over a network.

```text
Firefox (User Space)
        |
        | Requests network communication
        v
    System Call
        |
        v
Linux Kernel (Kernel Space)
        |
        | Processes the request
        v
Network Driver
        |
        v
Network Hardware
```

System calls allow applications to perform necessary operations without receiving unrestricted access to the system.

### 3.4 Practical Example: sudo

Consider the command:

```bash
sudo apt update
```

**Command breakdown:**

- `sudo` — Executes a command with elevated privileges, usually as root.
- `apt` — Ubuntu's package management tool.
- `update` — Refreshes package information.

**Important distinction:**

Using `sudo` does not automatically move an application into kernel space.

The application normally continues running in user space with elevated permissions.

### 3.5 Kernel Space vs. User Space

| Kernel Space | User Space |
|---|---|
| Highly privileged | Restricted privileges |
| Runs kernel code | Runs most applications |
| Accesses protected resources | Requests services through the kernel |
| Critical to OS operation | Isolated from critical kernel memory |
| Kernel vulnerabilities can compromise the OS | Application vulnerabilities may have more limited impact |

### Cybersecurity Relevance

This separation helps protect system integrity.

Attackers may attempt **privilege escalation**, which means obtaining permissions beyond those originally granted.

A kernel vulnerability can be particularly dangerous because successful exploitation may allow attackers to execute code with kernel-level privileges.

---

## 4. GUI vs. CLI

There are two common ways users interact with operating systems.

### 4.1 GUI — Graphical User Interface

A **GUI** allows users to interact with computers using graphical elements.

Examples include:

- Windows
- Icons
- Buttons
- Menus
- File managers

#### Advantages

- Easier for beginners
- Visual navigation
- Convenient for everyday tasks
- Requires less memorization of commands

#### Disadvantages

- Some tasks require many manual interactions
- Repetitive operations can be inefficient
- Automation may be less straightforward

### 4.2 CLI — Command-Line Interface

A **CLI** allows users to interact with computers by entering text commands.

Examples include:

- Bash
- PowerShell
- Windows Command Prompt

#### Advantages

- Efficient for repetitive tasks
- Supports scripting and automation
- Useful for remote system administration
- Provides access to many security tools
- Allows precise control over system operations

#### Disadvantages

- Requires learning command syntax
- Incorrect commands can have significant consequences
- Less visually intuitive for beginners

### 4.3 GUI vs. CLI Comparison

| Feature | GUI | CLI |
|---|---|---|
| Interaction | Graphical elements | Text commands |
| Learning curve | Generally easier initially | Requires command knowledge |
| Automation | Possible, but sometimes more complex | Well suited for scripting |
| Resource usage | Often higher | Often lower |
| Remote administration | Supported | Widely used |
| Cybersecurity tools | Graphical security tools | Terminal-based security tools |

---

## 5. Linux Commands Practised

During my Ubuntu cybersecurity lab sessions, I encountered the following commands:

| Command | Purpose |
|---|---|
| `pwd` | Display current directory |
| `ls` | List directory contents |
| `cd` | Change directory |
| `mkdir` | Create directory |
| `sudo` | Execute commands with elevated privileges |
| `apt update` | Refresh package information |
| `ip addr` | Display network interface information |
| `openvpn` | Establish VPN connections |

### Practical Example: Connecting to TryHackMe

```bash
cd ~/Downloads
sudo openvpn --config ./configuration.ovpn
```

**Explanation:**

1. `cd ~/Downloads` navigates to the Downloads directory.
2. `sudo` requests elevated privileges.
3. `openvpn` starts the OpenVPN application.
4. `--config` specifies the configuration file.
5. `./configuration.ovpn` represents the VPN configuration file in the current directory.

The filename must match the actual configuration file.

### Verifying the VPN Connection

```bash
ip addr show tun0
```

The `tun0` interface is commonly created when an OpenVPN tunnel is established.

A successful OpenVPN connection normally displays:

```text
Initialization Sequence Completed
```

---

## 6. Cybersecurity Applications

Understanding operating systems is essential for several cybersecurity specializations.

| Career | Why OS Knowledge Matters |
|---|---|
| SOC Analyst | Investigating suspicious processes and system logs |
| Penetration Tester | Identifying vulnerabilities and misconfigurations |
| Security Engineer | Configuring and securing operating systems |
| Malware Analyst | Understanding malicious process behavior |
| Digital Forensics Analyst | Investigating files, memory, and system activity |
| Cloud Security Engineer | Securing cloud-hosted operating systems |

### Important Cybersecurity Terminology

**Privilege Escalation**

Obtaining permissions beyond those originally granted.

**Process Isolation**

Separating processes to limit unauthorized access to one another.

**System Call**

A mechanism that allows applications to request services from the operating system kernel.

**Access Control**

Restricting access to resources according to security policies.

**Attack Surface**

The collection of possible entry points an attacker might exploit.

**Authentication**

The process of verifying the identity of a user, device, or system.

**Authorization**

The process of determining what an authenticated identity is permitted to access or perform.

---

## 7. Key Takeaways

Through TryHackMe and my Ubuntu cybersecurity lab, I learned that:

1. Operating systems manage hardware and software resources.
2. Process management controls how programs execute.
3. Memory management allocates and protects system memory.
4. File systems organize data and manage access permissions.
5. Kernel space operates with elevated privileges.
6. User space provides a restricted environment for applications.
7. System calls allow applications to request kernel services.
8. `sudo` provides elevated permissions without automatically moving applications into kernel space.
9. GUI and CLI are different methods of interacting with an operating system.
10. Understanding operating systems is essential for cybersecurity investigations and system administration.

---

## 8. Knowledge Check

### Question 1
What are three major responsibilities of an operating system?

### Question 2
What is the difference between kernel space and user space?

### Question 3
Why do applications use system calls?

### Question 4
What is the difference between a GUI and a CLI?

### Question 5
Why is privilege escalation a cybersecurity concern?

### Question 6
Does using `sudo` automatically move an application into kernel space?

### Question 7
Why is process isolation important for operating system security?

---

## 9. Next Learning Objectives

The next stage of my cybersecurity learning focuses on Linux fundamentals.

### Topics to Study

1. Linux file system structure
2. File permissions
3. Users and groups
4. Process management
5. Linux networking commands
6. System logs
7. Bash scripting

These skills will support future cybersecurity labs, system administration, and the development of my JARVIS cybersecurity assistant.

---

## Summary

Operating systems provide the foundation for modern computing by managing hardware, processes, memory, files, and security permissions.

Understanding the separation between kernel space and user space is especially important because it explains how operating systems protect critical resources.

Knowledge of GUI and CLI environments also provides the foundation for Linux administration, cybersecurity investigations, and security automation.