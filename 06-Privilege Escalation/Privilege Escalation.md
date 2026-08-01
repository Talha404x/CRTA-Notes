# Privilege Escalation

## Overview

Privilege Escalation is the process of obtaining higher privileges on a compromised system after achieving initial access. During a Red Team engagement, an attacker typically begins with a low-privileged account and attempts to elevate privileges to gain administrative or SYSTEM-level access.

Higher privileges provide greater control over the target system and enable access to sensitive resources required for later stages of the engagement, including credential access, persistence, and lateral movement.

---

## Objectives

The primary objectives of Privilege Escalation are:

- Identify privilege escalation opportunities.
- Obtain administrative or SYSTEM privileges.
- Access protected resources.
- Prepare the compromised system for post-exploitation.
- Support credential access and lateral movement.

---

# Privilege Escalation Methodology

Privilege escalation generally follows a structured process.

1. Enumerate the compromised system.
2. Identify misconfigurations.
3. Identify vulnerable services.
4. Review user privileges.
5. Exploit privilege escalation vectors.
6. Verify elevated privileges.

---

# Enumeration

Enumeration is the most important phase of privilege escalation.

The objective is to collect information about the operating system, installed software, services, users, groups, permissions, and security configurations.

The collected information helps identify potential privilege escalation opportunities.

---

# Identifying the Current User

## Windows

### Command

```cmd
whoami
```

### Purpose

Displays the currently authenticated user.

### Where it is Used

Executed immediately after obtaining access to identify the current security context.

### Expected Result

Displays the username of the current session.

---

## Linux

### Command

```bash
whoami
```

### Purpose

Displays the current logged-in user.

---

# Display User Privileges

## Command

```cmd
whoami /priv
```

### Purpose

Displays the privileges assigned to the current user.

### Where it is Used

Used during privilege escalation enumeration to identify dangerous privileges that may be abused.

### Expected Result

Lists all privileges available to the current user account.

---

# Display Group Membership

## Command

```cmd
whoami /groups
```

### Purpose

Displays all security groups associated with the current user.

### Where it is Used

Used to identify privileged group memberships.

---

# Display System Information

## Command

```cmd
systeminfo
```

### Purpose

Displays detailed information about the operating system.

### Where it is Used

Used during system enumeration to identify the operating system version, installed updates, and system architecture.

---

# Network Configuration

## Command

```cmd
ipconfig /all
```

### Purpose

Displays network interface configuration.

### Where it is Used

Used to understand the network configuration of the compromised host.

---

# Enumerating Local Users

## Command

```cmd
net user
```

### Purpose

Displays local user accounts.

### Where it is Used

Used to identify available user accounts.

---

# Enumerating Local Groups

## Command

```cmd
net localgroup
```

### Purpose

Displays local security groups.

### Where it is Used

Used to identify administrative groups and privileged accounts.

---

# Enumerating Running Processes

## Command

```cmd
tasklist
```

### Purpose

Displays running processes.

### Where it is Used

Used to identify security software, applications, and potential escalation opportunities.

---

# Enumerating Running Services

## Command

```cmd
sc query
```

### Purpose

Displays running Windows services.

### Where it is Used

Used to identify vulnerable or misconfigured services.

---

# File Permission Enumeration

During privilege escalation, directories and files should be inspected for weak permissions.

Examples include:

- Writable directories
- Writable executables
- Writable service binaries
- Writable configuration files

Misconfigured permissions may allow privilege escalation.

---

# Scheduled Tasks

Scheduled tasks should be reviewed to identify tasks executed with elevated privileges.

Misconfigured scheduled tasks may provide an opportunity to execute arbitrary commands with higher privileges.

---

# Installed Software

Installed software should be reviewed to identify:

- Outdated applications.
- Misconfigured software.
- Vulnerable third-party applications.

Such software may provide privilege escalation opportunities.

---

# Service Misconfigurations

Services running with elevated privileges should be inspected for configuration weaknesses.

Examples include:

- Weak service permissions.
- Writable service executables.
- Unquoted service paths.
- Weak registry permissions.

These misconfigurations may allow execution of attacker-controlled code with elevated privileges.

---

# Registry Configuration

Registry settings should be reviewed for privilege escalation opportunities.

Examples include:

- Service configuration.
- Auto-start entries.
- Installed applications.
- System configuration.

---

# Linux Enumeration

On Linux systems, system information should also be collected.

Common areas include:

- Current user
- User groups
- Running services
- Installed packages
- Scheduled jobs
- SUID binaries
- Writable directories

---

## Display User Identity

```bash
id
```

### Purpose

Displays the current user's UID, GID, and group memberships.

### Where it is Used

Used during Linux privilege escalation enumeration.

---

## Display Kernel Version

```bash
uname -a
```

### Purpose

Displays kernel and operating system information.

---

## Display Distribution Information

```bash
cat /etc/os-release
```

### Purpose

Displays Linux distribution information.

---

## Find SUID Files

```bash
find / -perm -4000 2>/dev/null
```

### Purpose

Searches the filesystem for SUID binaries.

### Where it is Used

Used to identify executables that run with elevated privileges.

---

## Find Writable Directories

```bash
find / -writable 2>/dev/null
```

### Purpose

Displays writable directories on the system.

---

## Display Scheduled Cron Jobs

```bash
crontab -l
```

### Purpose

Displays scheduled cron jobs for the current user.

---

# Verification

After performing privilege escalation, verify the newly obtained privileges.

## Windows

```cmd
whoami
```

If successful, the account should display an administrative or SYSTEM context.

---

## Linux

```bash
id
```

If successful, the output should indicate elevated privileges such as UID 0 (root).

---

# Post-Escalation Activities

After obtaining elevated privileges, the engagement can continue with:

- Credential Access
- Active Directory Enumeration
- Lateral Movement
- Persistence
- Kerberos Attacks

---

# Key Takeaways

- Privilege Escalation occurs after obtaining initial access.
- Enumeration is the most critical phase.
- Misconfigurations often provide escalation opportunities.
- Administrative privileges significantly increase attacker capabilities.
- Successful privilege escalation enables later stages of the Red Team engagement.

## References

- CRTA Course Material
- Active Directory Lab Exercises

