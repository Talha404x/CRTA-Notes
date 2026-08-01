# Lab Setup

## Overview

The Red Team laboratory provides a controlled environment for performing offensive security exercises without affecting production systems. It simulates a small enterprise network consisting of externally accessible services, internal infrastructure, and an Active Directory environment.

The lab is designed to demonstrate the complete attack path from initial access to post-exploitation within an isolated environment.

---

## Objectives

The primary objectives of the lab setup are:

- Build an isolated Red Team laboratory.
- Simulate an enterprise network architecture.
- Deploy vulnerable and Windows-based systems.
- Configure an internal Active Directory environment.
- Prepare the environment for later exploitation phases.

---

# Lab Architecture

The laboratory consists of two isolated network segments.

| Network | Purpose |
|----------|----------|
| External Network | Simulates publicly accessible systems. |
| Internal Network | Simulates the organization's internal infrastructure. |

The Web Server acts as the bridge between both networks, allowing communication between the external and internal environments.

---

# Virtual Machines

The laboratory consists of the following systems.

| Machine | Role |
|----------|------|
| Kali Linux | Attacker machine |
| Metasploitable 2 | Vulnerable Web Server |
| Windows Server 2016 | Domain Controller |
| Windows 10 | Employee Machine |
| Windows Server 2012 | Application Server |

---

# Network Design

The lab uses two isolated network segments.

| Network | Address Range |
|----------|---------------|
| External Network | `192.168.xx.0/24` |
| Internal Network | `192.168.xx.0/24` |

Example addressing:

| System | Example Address |
|---------|-----------------|
| Host-Only Adapter | `192.168.xx.1` |
| Web Server (External) | `192.168.xx.xx` |
| Web Server (Internal) | `192.168.xx.xx` |
| Domain Controller | `192.168.xx.xx` |
| Employee Machine | `192.168.xx.xx` |
| Application Server | `192.168.xx.xx` |

> Actual IP addresses may vary depending on the lab configuration.

---

# Network Topology

The attacker machine is connected only to the external network.

The Web Server has two network interfaces.

- External interface connected to the attacker network.
- Internal interface connected to the Active Directory environment.

The Domain Controller, Employee Machine, and Application Server are connected only to the internal network.

This architecture simulates a real-world enterprise where public-facing servers provide limited access to the internal infrastructure.

---

# Installing the Virtual Machines

Deploy the following virtual machines using the preferred virtualization platform.

- Kali Linux
- Metasploitable 2
- Windows Server 2016
- Windows 10
- Windows Server 2012

Configure each virtual machine according to its assigned role before continuing with the Active Directory configuration.

---

# Configuring Static Network Interfaces

The Web Server uses static IP addressing to maintain consistent connectivity across reboots.

### Open the network configuration file

```bash
sudo nano /etc/network/interfaces
```

**Purpose**

Opens the Linux network configuration file for editing.

**Where it is used**

Used while configuring permanent network settings on the Metasploitable Web Server.

---

### Configure the External Interface

```text
auto eth0
iface eth0 inet static
address 192.168.xx.xx
netmask 255.255.255.0
```

**Purpose**

Assigns a static IP address to the external network interface.

---

### Configure the Internal Interface

```text
auto eth1
iface eth1 inet static
address 192.168.xx.xx
netmask 255.255.255.0
```

**Purpose**

Assigns a static IP address to the internal network interface.

---

### Restart Networking

```bash
sudo /etc/init.d/networking restart
```

**Purpose**

Restarts the networking service to apply the new configuration.

**Where it is used**

Executed after modifying the network configuration file.

---

# Verifying Connectivity

After configuring the interfaces, verify network communication between the systems.

Connectivity should be confirmed between:

- Kali Linux and the Web Server (external network).
- Web Server and the internal network.
- Internal systems within the Active Directory environment.

Successful communication confirms that the network has been configured correctly.

---

# Domain Controller Configuration

The Domain Controller is responsible for managing authentication, authorization, and directory services within the lab.

The following server roles are installed:

- Active Directory Domain Services (AD DS)
- DNS Server

After installation, the server is promoted to a Domain Controller by creating a new forest.

The NetBIOS name is automatically generated during the promotion process.

---

# Employee Machine Configuration

The Employee Machine represents a standard domain workstation.

After installation:

- Configure a static IP address.
- Configure the DNS server to point to the Domain Controller.
- Join the system to the Active Directory domain.

---

# Application Server Configuration

The Application Server represents an internal enterprise server.

After installation:

- Configure a static IP address.
- Configure the DNS server to point to the Domain Controller.
- Join the Active Directory domain.

---

# Joining Systems to the Domain

After the Domain Controller has been configured, the Employee Machine and Application Server are joined to the Active Directory domain.

Once joined successfully, both systems become members of the domain and can authenticate using domain accounts.

---

# Creating Domain Users

Create the required domain user accounts from the Domain Controller.

These accounts are later used during authentication, authorization, and privilege escalation exercises throughout the course.

---

# Lab Verification

The lab setup is considered complete after verifying that:

- All virtual machines are operational.
- Static IP addresses are configured correctly.
- Systems can communicate within their respective networks.
- Active Directory Domain Services are functioning correctly.
- Internal machines have successfully joined the domain.
- Domain users can authenticate successfully.

---

# Key Takeaways

- The laboratory simulates a small enterprise network.
- Separate external and internal networks improve realism.
- Static addressing provides consistent communication between systems.
- The Web Server bridges both network segments.
- Active Directory forms the foundation for later Red Team operations.
- Proper lab configuration is essential before beginning exploitation activities.
