# Network Pivoting

## Overview

Network Pivoting is a technique used during Red Team engagements to access systems located on an internal network that are not directly reachable from the attacker's machine.

After obtaining an initial foothold on a compromised host, that system is used as an intermediary to communicate with additional network segments. This allows the attacker to continue the engagement without requiring direct connectivity to the internal environment.

---

## Objectives

The objectives of Network Pivoting include:

- Access isolated internal networks.
- Enumerate internal hosts and services.
- Route traffic through a compromised system.
- Continue post-exploitation activities.
- Prepare for lateral movement within the environment.

---

## What is Pivoting?

Pivoting is the process of using a compromised machine as a bridge to reach systems that are inaccessible from the attacker's host.

In the CRTA lab environment, the compromised Web Server contains two network interfaces.

| Interface | Network |
|-----------|---------|
| External Interface | Connected to the attacker network |
| Internal Interface | Connected to the internal enterprise network |

Because the attacker cannot directly communicate with the internal network, the compromised Web Server becomes the pivot point.

---

# Lab Scenario

At this stage of the engagement:

- Initial access has already been obtained on the Web Server.
- Valid SSH credentials have been identified.
- The attacker can access the external interface of the Web Server.
- The internal network remains inaccessible from the attacker's machine.

The objective is to establish communication with the internal network through the compromised Web Server.

---

# Verifying SSH Access

Before establishing a pivot, verify that the recovered credentials provide remote access to the compromised server.

## Command

```bash
ssh username@192.168.xx.xx
```

### Purpose

Attempts to establish an SSH session with the compromised machine.

### Where it is used

Used immediately after recovering valid SSH credentials.

### Example

```bash
ssh msfadmin@192.168.xx.xx
```

### Expected Result

A successful login confirms that the credentials are valid and can be used for further post-exploitation activities.

---

# Legacy SSH Compatibility

The CRTA lab uses an older Linux system that supports legacy SSH algorithms.

Modern OpenSSH clients may reject the connection because older algorithms are disabled by default. :contentReference[oaicite:1]{index=1}

## Command

```bash
ssh \
-o HostKeyAlgorithms=+ssh-rsa \
-o PubkeyAcceptedAlgorithms=+ssh-rsa \
username@192.168.xx.xx
```

### Purpose

Temporarily enables legacy RSA algorithms required by older SSH servers.

### Where it is used

Used when connecting to older systems that do not support modern SSH algorithms.

### Command Breakdown

| Option | Description |
|---------|-------------|
| `-o` | Specifies an SSH configuration option. |
| `HostKeyAlgorithms` | Enables the server host key algorithm. |
| `PubkeyAcceptedAlgorithms` | Allows legacy public key authentication. |
| `+ssh-rsa` | Temporarily enables the RSA algorithm. |

---

# Switching to the Root User

Once authenticated, administrative privileges may be required for certain operations.

## Command

```bash
sudo -i
```

### Purpose

Starts an interactive shell with elevated privileges.

### Where it is used

Used after successful SSH authentication when administrative access is required.

---

# SOCKS Proxy Pivoting

The CRTA notes use a SOCKS proxy to tunnel traffic through the compromised machine, allowing tools on the attacker's host to communicate with internal systems. :contentReference[oaicite:2]{index=2}

---

# Installing Proxychains

Proxychains forwards supported applications through a SOCKS proxy.

## Configuration File

```bash
sudo nano /etc/proxychains.conf
```

### Purpose

Opens the Proxychains configuration file.

### Where it is used

Used before creating a SOCKS tunnel.

---

## Configuration

Ensure that:

- `dynamic_chain` is enabled.
- The SOCKS proxy listens on the configured local port.

Example:

```text
dynamic_chain

socks5 127.0.0.1 9050
```

---

# Creating the SOCKS Tunnel

## Command

```bash
ssh -D 9050 username@192.168.xx.xx
```

### Purpose

Creates a local SOCKS proxy through the compromised machine.

### Where it is used

Used after SSH authentication to forward traffic into the internal network.

### Command Breakdown

| Option | Description |
|---------|-------------|
| `-D` | Creates a dynamic SOCKS proxy. |
| `9050` | Local listening port. |

### Expected Result

The attacker's machine can route supported applications through the compromised server.

---

# Verifying Internal Connectivity

Once the tunnel has been established, internal systems can be reached using Proxychains.

## Netcat

```bash
proxychains nc 192.168.xx.xx 445
```

### Purpose

Tests connectivity to a specific TCP port on an internal host.

### Where it is used

Used to verify that the pivot tunnel is functioning correctly.

---

## Nmap

```bash
proxychains nmap -sn 192.168.xx.xx
```

### Purpose

Performs host discovery through the SOCKS tunnel.

### Where it is used

Used after confirming that Proxychains is functioning correctly.

---

# Key Takeaways

- Pivoting allows communication with isolated internal networks.
- The compromised Web Server acts as the bridge between network segments.
- SSH pivoting requires valid credentials.
- Proxychains forwards supported applications through a SOCKS proxy.
- Successful pivoting prepares the environment for internal enumeration and lateral movement.

## References

- CRTA Course Material
- Active Directory Lab Exercises

