# Active Directory

## Overview

Active Directory (AD) is Microsoft's centralized directory service that manages users, computers, groups, printers, shared resources, and security policies within an enterprise environment.

It stores information about network objects in a centralized database and provides authentication, authorization, and resource management services for domain-joined systems.

Within the CRTA lab environment, Active Directory forms the foundation of the internal enterprise network and is the primary target during post-exploitation activities.

---

## Objectives

The primary objectives of this section are:

- Understand the Active Directory architecture.
- Identify the components of an AD environment.
- Understand Kerberos authentication.
- Understand Active Directory authorization.
- Learn common Active Directory objects.
- Enumerate domain information using PowerView.

---

# Active Directory Architecture

Active Directory provides centralized management of enterprise resources.

It allows administrators to:

- Manage user accounts.
- Manage computer accounts.
- Configure security policies.
- Control access to network resources.
- Manage shared folders and printers.

All information is maintained centrally by the Domain Controller.

---

# Forest

A Forest is the highest logical container in Active Directory.

It consists of one or more domains that trust one another.

### Key Characteristics

- First domain becomes the Root Domain.
- Domains within the forest trust each other.
- A forest represents a single security boundary.

---

# Domain

A Domain is a logical security boundary within Active Directory.

It contains:

- Users
- Computers
- Groups
- Organizational Units
- Group Policies

Each domain is managed by one or more Domain Controllers.

---

# Domain Controller

A Domain Controller (DC) is the server responsible for hosting Active Directory services.

Its primary responsibilities include:

- Authenticating users.
- Storing the Active Directory database.
- Enforcing security policies.
- Processing Kerberos authentication.
- Providing LDAP services.

---

# Organizational Units (OUs)

Organizational Units (OUs) are logical containers used to organize Active Directory objects.

### Purpose

- Organize users and computers.
- Apply Group Policies.
- Delegate administrative control.

---

# Groups

Groups are collections of users or computers used to simplify permission management.

### Types of Groups

| Group Type | Purpose |
|------------|---------|
| Security Group | Used to assign permissions and access rights. |
| Distribution Group | Used for email distribution. |

Groups may contain privileged or non-privileged users depending on their assigned role.

---

# Active Directory Objects

Active Directory consists of multiple object types.

| Object | Description |
|--------|-------------|
| Domain User | User account used to authenticate within the domain. |
| Domain Group | Collection of users used for permission management. |
| Domain Computer | Computer joined to the Active Directory domain. |
| Domain Controller | Central authentication server. |
| Group Policy Object (GPO) | Collection of policies applied to users and computers. |

---

# Kerberos Authentication

Kerberos is the default authentication protocol used within Active Directory.

Instead of sending passwords across the network, Kerberos relies on tickets to authenticate users and authorize access to services. 

The authentication process consists of the following stages:

1. The user authenticates with the Domain Controller.
2. The Domain Controller validates the credentials.
3. A Ticket Granting Ticket (TGT) is issued.
4. The TGT is used to request a Ticket Granting Service (TGS) ticket.
5. The TGS is presented to the target service to obtain access.

---

## Ticket Granting Ticket (TGT)

A Ticket Granting Ticket (TGT) is issued after successful user authentication.

### Purpose

- Proves the user's identity.
- Used to request additional service tickets.
- Stored in memory after authentication.

---

## Ticket Granting Service (TGS)

A Ticket Granting Service (TGS) ticket is issued when a user requests access to a specific service.

### Purpose

- Provides authorization to access a service.
- Generated after presenting a valid TGT.
- Issued for a specific service.

---

# Kerberos Delegation

Kerberos Delegation allows a service to access another service on behalf of an authenticated user.

This functionality is commonly used in multi-tier enterprise applications. :contentReference[oaicite:2]{index=2}

### Delegation Process

1. User authenticates using Kerberos.
2. User accesses a service.
3. That service requests access to another service.
4. Kerberos allows the request using the user's identity.

---

## Types of Delegation

### Unconstrained Delegation

Allows a server to request access to any service on behalf of a user.

### Constrained Delegation

Allows access only to specifically configured services.

---

# Authorization in Active Directory

Authentication verifies the identity of a user.

Authorization determines whether that user is permitted to access a particular resource.

Authorization decisions are based on the user's Security Token. :contentReference[oaicite:3]{index=3}

The Security Token contains:

- User Rights
- Group Security Identifiers (SIDs)
- User Security Identifier (SID)

Windows evaluates this token against the Access Control List (ACL) assigned to the requested resource.

---

# Access Control List (ACL)

An Access Control List (ACL) defines which users or groups can access a resource.

Each ACL consists of one or more Access Control Entries (ACEs).

Each ACE specifies:

- Which SID is affected.
- Whether access is allowed or denied.
- The permissions assigned.

---

## Types of ACL

### Discretionary Access Control List (DACL)

Defines which users and groups are permitted or denied access to a resource.

### System Access Control List (SACL)

Defines which actions should be audited for security monitoring.

---

# Security Identifier (SID)

A Security Identifier (SID) is a unique value assigned to every security principal within Active Directory.

SIDs uniquely identify:

- Users
- Groups
- Computers
- Domains

Permissions are assigned using SIDs rather than object names.

---

# Active Directory Enumeration

PowerView is used throughout the CRTA lab to enumerate Active Directory information.

---

## Import PowerView

### Command

```powershell
Import-Module .\PowerView.ps1
```

### Purpose

Loads the PowerView module into the current PowerShell session.

### Where it is Used

Executed before using any PowerView enumeration commands.

---

## Enumerate Domain Users

### Command

```powershell
Get-NetUser
```

### Purpose

Enumerates domain user accounts.

### Where it is Used

Used during Active Directory enumeration after obtaining access to a domain-joined system.

---

## Display User Names

### Command

```powershell
Get-NetUser | Select GivenName
```

### Purpose

Displays the names of domain users.

---

## Enumerate Domain Information

### Command

```powershell
Get-Domain -Verbose
```

### Purpose

Displays detailed information about the current Active Directory domain.

---

## Enumerate Domain Controllers

### Command

```powershell
Get-DomainController
```

### Purpose

Displays information about available Domain Controllers.

---

## Enumerate Domain SID

### Command

```powershell
Get-DomainSID -Verbose
```

### Purpose

Retrieves the Security Identifier (SID) of the current domain.

---

# Key Takeaways

- Active Directory provides centralized identity and resource management.
- The Domain Controller is responsible for authentication and directory services.
- Forests contain one or more trusted domains.
- Organizational Units organize Active Directory objects.
- Kerberos uses TGT and TGS tickets instead of transmitting passwords.
- Authorization is performed using Security Tokens and Access Control Lists.
- PowerView is used to enumerate domain information after obtaining access to a domain-joined system.

## References

- CRTA Course Material
- Active Directory Lab Exercises

