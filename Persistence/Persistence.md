# Persistence

## Overview

Persistence is the phase of a Red Team engagement where the objective is to maintain authorized access to a compromised environment across multiple sessions. During a security assessment, persistence mechanisms are evaluated to demonstrate how an attacker may attempt to retain access after system reboots, user logouts, or credential changes.

Within the CRTA lab environment, persistence is introduced after successful privilege escalation, credential access, and lateral movement to demonstrate the importance of securing long-term access mechanisms.

---

## Objectives

The primary objectives of Persistence are:

- Understand the purpose of persistence techniques.
- Identify common persistence mechanisms within enterprise environments.
- Evaluate the security impact of persistent access.
- Understand how persistence supports later stages of an engagement.
- Recognize defensive controls that reduce persistence opportunities.

---

# Persistence in the Attack Lifecycle

Persistence is established after an attacker has successfully compromised one or more systems within the target environment.

The general workflow is:

1. Initial Access
2. Privilege Escalation
3. Credential Access
4. Lateral Movement
5. Persistence
6. Objective Completion

Persistence ensures that access can be re-established without repeating the initial compromise.

---

# Why Persistence is Important

Maintaining access allows an attacker to continue authorized assessment activities throughout the engagement.

Persistence may support activities such as:

- Continuing internal enumeration.
- Accessing additional systems.
- Monitoring the environment.
- Completing engagement objectives.
- Evaluating an organization's detection capabilities.

---

# Common Persistence Locations

Enterprise systems provide multiple locations where persistent access mechanisms may exist.

Examples include:

- User startup locations.
- Scheduled tasks.
- Windows services.
- Login scripts.
- Registry configuration.
- System configuration files.
- Administrative accounts.

Each mechanism should be evaluated within the approved scope of the engagement.

---

# Active Directory Considerations

Within an Active Directory environment, persistence should be evaluated carefully because changes may affect multiple systems.

Areas commonly reviewed include:

- Privileged accounts.
- Service accounts.
- Group memberships.
- Administrative permissions.
- Domain configuration.

Changes should always remain within the approved engagement scope.

---

# Security Considerations

Persistence mechanisms increase the amount of time an attacker may remain within an environment.

Potential security impacts include:

- Continued unauthorized access.
- Re-entry after system restarts.
- Extended access to enterprise resources.
- Increased opportunities for lateral movement.
- Greater difficulty in identifying compromise.

For this reason, organizations should continuously review systems for unauthorized persistence mechanisms.

---

# Detection Considerations

Security teams should monitor for changes that may indicate persistence.

Examples include:

- Creation of new administrative accounts.
- Unexpected scheduled tasks.
- Changes to Windows services.
- Startup configuration modifications.
- Registry modifications.
- Authentication activity from dormant accounts.

Continuous monitoring assists in identifying abnormal behavior before it results in long-term compromise.

---

# Mitigation

Organizations can reduce persistence opportunities by implementing appropriate security controls.

Recommended practices include:

- Apply the principle of least privilege.
- Review administrative accounts regularly.
- Remove unused accounts.
- Audit startup locations.
- Monitor scheduled tasks.
- Review service configurations.
- Enable centralized logging.
- Perform regular security assessments.

---

# Operational Considerations

During a Red Team engagement:

- Operate only within the approved scope.
- Document all persistence mechanisms used.
- Avoid unnecessary changes to production systems.
- Remove temporary persistence mechanisms before concluding the engagement.
- Include all persistence findings within the final report.

---

# Best Practices

The following practices strengthen enterprise security against persistence techniques:

- Implement strong access control.
- Review privileged accounts frequently.
- Monitor authentication events.
- Apply security updates promptly.
- Audit system configuration changes.
- Perform periodic Active Directory reviews.
- Conduct regular Red Team and Blue Team exercises.

---

# Key Takeaways

- Persistence enables continued access after the initial compromise.
- Long-term access increases the importance of continuous monitoring.
- Administrative accounts and system configuration should be protected.
- Proper auditing assists in identifying unauthorized persistence.
- Removing persistence mechanisms is an important part of completing a Red Team engagement.

---

## References

- CRTA Course Material
- Active Directory Lab Exercises
