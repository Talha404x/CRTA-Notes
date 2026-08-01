# External Operations

## Overview

External Operations represent the initial phase of a Red Team engagement where the objective is to identify and compromise systems that are publicly accessible. During this phase, the attacker has no prior access to the target environment and relies entirely on information gathered from external sources and exposed services.

The primary goal is to obtain an initial foothold by identifying vulnerabilities or misconfigurations in externally accessible systems while collecting sufficient intelligence to support later stages of the engagement.

---

## Objectives

The primary objectives of External Operations include:

- Collecting information about the target environment.
- Identifying externally accessible systems.
- Discovering exposed network services.
- Enumerating technologies and service versions.
- Identifying potential attack vectors.
- Obtaining an initial foothold within the target environment.

---

## External Attack Methodology

External Operations generally follow a structured workflow.

1. Information Gathering
2. Host Discovery
3. Scanning
4. Enumeration
5. Initial Access
6. Post-Exploitation
7. Persistence
8. Removing Footprints

Each phase builds upon the information collected during the previous stage.

---

# Cyber Kill Chain

The Cyber Kill Chain represents the sequence of activities performed by an attacker during an external compromise.

| Phase | Description |
|--------|-------------|
| Reconnaissance | Collect information about the target. |
| Scanning & Enumeration | Identify live hosts, services, operating systems, and technologies. |
| Gaining Access | Exploit identified weaknesses to compromise the target. |
| Post-Exploitation | Expand control after obtaining access. |
| Maintaining Persistence | Preserve access for future operations. |
| Removing Footprints | Reduce evidence of attacker activity. |

---

# Information Gathering

Information Gathering is the process of collecting information about the target environment before attempting exploitation.

The collected information helps identify technologies, exposed services, network architecture, and potential attack vectors.

This phase forms the foundation for all subsequent stages of the engagement.

There are two approaches to reconnaissance.

| Type | Description |
|------|-------------|
| Passive Reconnaissance | Information is collected without directly interacting with the target. |
| Active Reconnaissance | Information is collected through direct interaction with target systems. |

---

# Passive Reconnaissance

Passive reconnaissance involves gathering publicly available information without generating traffic toward the target infrastructure.

Typical sources include:

- Public websites
- Public documentation
- Technology information
- Publicly available resources

Since no direct communication occurs with the target environment, passive reconnaissance is generally less likely to be detected.

---

# Active Reconnaissance

Active reconnaissance involves establishing direct communication with target systems.

Examples include:

- Connecting to exposed services
- Identifying open ports
- Detecting operating systems
- Enumerating service versions

Unlike passive reconnaissance, active reconnaissance generates network traffic and may be detected by defensive monitoring systems.

---

# Host Discovery

Host Discovery is performed to identify systems that are currently active on the target network.

Identifying live hosts allows subsequent scanning and enumeration activities to focus only on reachable systems.

---

## Host Discovery using Netdiscover

### Command

```bash
netdiscover -i <interface> -r 192.168.xx.0/24
```

### Purpose

Discovers active hosts within a local network.

### Where it is used

Used during the Host Discovery phase before performing port scanning or service enumeration.

### Command Breakdown

| Option | Description |
|---------|-------------|
| `-i` | Specifies the network interface to use. |
| `-r` | Specifies the target network range in CIDR notation. |

### Example

```bash
netdiscover -i eth0 -r 192.168.xx.0/24
```

### Expected Result

The command displays active hosts discovered within the specified subnet along with their corresponding MAC addresses.

---

# Scanning

Once live hosts have been identified, scanning is performed to determine which network services are accessible.

Scanning helps identify:

- Open TCP ports
- Open UDP ports
- Running services
- Potential attack surface

This information is used during the enumeration phase.

---

# Enumeration

Enumeration is the process of collecting detailed information about the services identified during scanning.

Typical enumeration activities include:

- Service version detection
- Operating system identification
- Network service identification
- Technology identification

The objective is to understand the target environment in sufficient detail to identify potential weaknesses.

---

# Initial Access

Initial Access is the phase in which identified vulnerabilities or weaknesses are leveraged to compromise the target system.

The attack path depends entirely on the information collected during reconnaissance, scanning, and enumeration.

Successful exploitation establishes the first foothold within the target environment and enables the engagement to progress into post-exploitation activities.

---

# Post-Exploitation

Once initial access has been achieved, the attacker begins interacting with the compromised system.

Typical objectives include:

- Expanding access
- Discovering additional systems
- Collecting credentials
- Performing privilege escalation
- Preparing for lateral movement

---

# Maintaining Persistence

Persistence ensures continued access to the compromised environment.

The objective is to maintain access even if the original entry point is no longer available.

---

# Removing Footprints

After completing the engagement objectives, evidence generated during the attack should be minimized.

Removing footprints helps reduce traces of attacker activity and complicates forensic analysis.

---

# Key Takeaways

- External Operations represent the initial phase of a Red Team engagement.
- Information gathering provides the foundation for all subsequent attack stages.
- Host discovery identifies reachable systems before detailed analysis begins.
- Scanning identifies exposed services.
- Enumeration collects detailed information about discovered services.
- Initial access is achieved by exploiting identified weaknesses.
- Successful compromise enables later phases such as privilege escalation, credential access, and lateral movement.

## References

- CRTA Course Material
- Active Directory Lab Exercises

