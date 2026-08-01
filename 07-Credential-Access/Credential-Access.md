# Credential Access

## Overview

Credential Access is the phase of a Red Team engagement where the objective is to obtain authentication material that can be used to access additional systems, services, or accounts within the target environment.

Compromised credentials often provide access to privileged accounts and enable further actions such as Active Directory enumeration, lateral movement, and privilege escalation.

Credential Access is performed only after obtaining an initial foothold and, in many cases, elevated privileges on the compromised host.

---

## Objectives

The primary objectives of Credential Access are:

- Identify stored credentials.
- Recover authentication material.
- Enumerate privileged accounts.
- Obtain credentials for additional systems.
- Prepare for lateral movement.
- Support Active Directory attacks.

---

# Credential Access Methodology

Credential Access generally follows a structured workflow.

1. Enumerate the compromised system.
2. Identify locations where credentials may be stored.
3. Recover authentication material.
4. Validate recovered credentials.
5. Use valid credentials for further access.

---

# Common Credential Sources

Credentials may be found in several locations within a compromised environment.

Common sources include:

- User sessions
- Configuration files
- Saved credentials
- Password managers
- Scripts
- Scheduled tasks
- Service accounts
- Active Directory

---

# Enumerating Logged-on Users

Identifying logged-on users helps determine which credentials may currently be available.

## Command

```cmd
query user
```

### Purpose

Displays users currently logged on to the system.

### Where it is Used

Executed after obtaining access to identify active user sessions.

### Expected Result

Lists all active user sessions.

---

# Display Current User

## Command

```cmd
whoami
```

### Purpose

Displays the current user context.

### Where it is Used

Used throughout the engagement to verify the active security context.

---

# Enumerating Stored Credentials

Windows may store credentials for previously authenticated users.

## Command

```cmd
cmdkey /list
```

### Purpose

Displays stored credentials on the current system.

### Where it is Used

Executed during credential enumeration after gaining access to a Windows host.

### Expected Result

Lists credentials stored by Windows Credential Manager.

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

# Enumerating Domain Users

## Command

```powershell
Get-NetUser
```

### Purpose

Enumerates domain user accounts.

### Where it is Used

Executed after importing PowerView on a domain-joined system.

---

# Enumerating Domain Groups

## Command

```powershell
Get-NetGroup
```

### Purpose

Displays Active Directory groups.

### Where it is Used

Used to identify privileged groups within the domain.

---

# Enumerating Domain Administrators

## Command

```powershell
Get-NetGroupMember "Domain Admins"
```

### Purpose

Displays members of the Domain Admins group.

### Where it is Used

Used during Active Directory enumeration to identify privileged accounts.

---

# Enumerating Shared Resources

Shared folders may contain sensitive information such as scripts or configuration files.

## Command

```cmd
net share
```

### Purpose

Displays shared resources on the current system.

### Where it is Used

Executed during post-exploitation to identify accessible shares.

---

# Searching for Configuration Files

Configuration files may contain usernames, passwords, or connection strings.

Typical locations include:

- Application directories
- Configuration files
- Deployment scripts
- Backup files

Any recovered credentials should be validated before use.

---

# Service Accounts

Service accounts are commonly used to run Windows services.

These accounts may possess elevated privileges and should be identified during enumeration.

Typical enumeration includes:

- Installed services
- Service accounts
- Service permissions

---

# Active Directory Credentials

Within an Active Directory environment, credential material may include:

- User credentials
- Service account credentials
- Computer account credentials
- Kerberos tickets

These credentials may be leveraged during later phases of the engagement.

---

# Credential Validation

Recovered credentials should always be validated before use.

Validation confirms:

- Username
- Password
- Account status
- Access level

Only valid credentials should be used for subsequent operations.

---

# Preparing for Lateral Movement

After recovering valid credentials, the next objective is to authenticate to additional systems within the environment.

Recovered credentials may provide access to:

- Workstations
- Application Servers
- Domain Controllers
- File Servers

Successful authentication enables the engagement to progress into the Lateral Movement phase.

---

# Best Practices

During Credential Access:

- Document every recovered credential.
- Record the source of each credential.
- Validate credentials before use.
- Avoid unnecessary authentication attempts.
- Minimize actions that may generate alerts.

---

# Key Takeaways

- Credential Access focuses on recovering authentication material.
- Enumeration is essential before attempting credential recovery.
- Stored credentials and Active Directory accounts are valuable targets.
- Valid credentials enable access to additional systems.
- Credential Access prepares the environment for Lateral Movement and Kerberos-based attacks.
