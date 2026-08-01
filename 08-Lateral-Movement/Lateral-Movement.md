# Lateral Movement

## Overview

Lateral Movement is the process of moving from one compromised system to another within the target environment. After obtaining valid credentials or administrative privileges, the attacker attempts to access additional hosts in order to expand control over the network and progress toward the engagement objectives.

Within the CRTA lab environment, lateral movement is performed after successful credential access and Active Directory enumeration.

---

## Objectives

The primary objectives of Lateral Movement are:

- Access additional systems within the domain.
- Expand the attack surface.
- Identify privileged systems.
- Reach critical assets such as application servers and domain controllers.
- Prepare for Kerberos-based attacks and persistence.

---

# Lateral Movement Methodology

Lateral Movement generally follows a structured workflow.

1. Identify accessible hosts.
2. Verify recovered credentials.
3. Enumerate remote services.
4. Authenticate to remote systems.
5. Execute commands remotely.
6. Continue internal enumeration.
7. Repeat the process until engagement objectives are achieved.

---

# Requirements

Before attempting lateral movement, the following conditions should be satisfied:

- Initial access has been obtained.
- Valid credentials are available.
- Internal network connectivity has been established.
- Target systems are reachable.

---

# Identifying Target Systems

Potential targets include:

- Employee Workstations
- Application Servers
- File Servers
- Domain Controllers

Priority should be given to systems that provide access to privileged users or sensitive resources.

---

# Verifying Network Connectivity

Before authenticating to a remote system, verify that the target is reachable.

## Command

```cmd
ping 192.168.xx.xx
```

### Purpose

Verifies network connectivity to the remote host.

### Where it is Used

Executed before attempting remote authentication.

### Expected Result

Successful replies confirm that the target system is reachable.

---

# Enumerating Shared Resources

Administrative shares are commonly used during lateral movement.

## Command

```cmd
net view \\192.168.xx.xx
```

### Purpose

Displays shared resources available on the remote system.

### Where it is Used

Used to identify accessible network shares.

### Expected Result

Lists the shared folders configured on the target system.

---

# Enumerating Remote Systems

## Command

```cmd
net view
```

### Purpose

Displays visible systems within the current network.

### Where it is Used

Used during internal network enumeration.

---

# Remote Authentication

After valid credentials have been obtained, they can be used to authenticate to additional systems.

Successful authentication allows the attacker to continue post-exploitation activities on remote hosts.

---

# PowerShell Remoting

PowerShell Remoting allows administrators to remotely manage Windows systems.

During an engagement, valid credentials may permit authenticated remote access.

## Command

```powershell
Enter-PSSession -ComputerName <Target-System>
```

### Purpose

Creates an interactive PowerShell session on a remote system.

### Where it is Used

Used after obtaining valid credentials for a remote Windows host.

### Command Breakdown

| Option | Description |
|--------|-------------|
| `-ComputerName` | Specifies the remote system. |

---

# Executing Remote Commands

## Command

```powershell
Invoke-Command -ComputerName <Target-System> -ScriptBlock { hostname }
```

### Purpose

Executes commands remotely without establishing an interactive session.

### Where it is Used

Used for remote administration and verification.

---

# Accessing Administrative Shares

Windows automatically creates administrative shares for system management.

Examples include:

- C$
- ADMIN$
- IPC$

These shares may be accessible using administrative credentials.

---

# Verifying the Current User

After successfully accessing a remote system, verify the security context.

## Command

```cmd
whoami
```

### Purpose

Displays the currently authenticated user.

### Where it is Used

Executed immediately after obtaining access to a remote system.

---

# Host Identification

## Command

```cmd
hostname
```

### Purpose

Displays the hostname of the current system.

### Where it is Used

Used to confirm that the remote session has been established on the intended target.

---

# Domain Enumeration

After accessing additional systems, domain information should continue to be collected.

Typical enumeration includes:

- Logged-on users
- Running services
- Domain groups
- Domain administrators
- Shared folders
- Installed applications

The collected information assists in identifying additional attack paths.

---

# Security Considerations

Lateral movement generates authentication events across multiple systems.

To reduce the likelihood of detection:

- Authenticate only when necessary.
- Avoid unnecessary remote connections.
- Use valid credentials obtained during the engagement.
- Document every accessed system.
- Operate within the approved engagement scope.

---

# Transition to Kerberos Attacks

Once privileged accounts and service accounts have been identified, the engagement proceeds to Kerberos-based attacks.

The following techniques are covered separately within this repository:

- Kerberoasting
- Silver Ticket
- Golden Ticket

---

# Key Takeaways

- Lateral Movement expands attacker access within the internal network.
- Valid credentials are the primary requirement for successful movement.
- Administrative shares and PowerShell Remoting provide methods for remote administration.
- Each newly compromised system should be enumerated before proceeding further.
- Lateral Movement prepares the environment for Kerberos attacks and persistence.

## References

- CRTA Course Material
- Active Directory Lab Exercises

