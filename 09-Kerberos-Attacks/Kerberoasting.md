# Kerberoasting

## Overview

Kerberoasting is a Kerberos-based attack technique that targets service accounts registered with Service Principal Names (SPNs). Within an Active Directory environment, authenticated users can request service tickets for these accounts as part of the normal Kerberos authentication process.

The security of these service tickets depends on the strength of the associated service account password. Weak or predictable passwords increase the risk of offline password recovery.

In the CRTA course, Kerberoasting is introduced as an example of how Kerberos authentication can be abused when service accounts are not properly secured.

---

## Objectives

The objectives of studying Kerberoasting are to:

- Understand the role of Service Principal Names (SPNs).
- Learn how Kerberos service tickets are used for authentication.
- Understand why service accounts are attractive targets.
- Identify the risks associated with weak service account passwords.
- Recognize defensive measures that reduce exposure.

---

# Kerberos Authentication Review

Kerberoasting relies on the normal Kerberos authentication process.

A simplified workflow is shown below:

1. A user authenticates to the domain.
2. The Domain Controller issues a Ticket Granting Ticket (TGT).
3. The user requests access to a service.
4. The Domain Controller issues a Ticket Granting Service (TGS) ticket for the requested service.
5. The client presents the TGS ticket to the service.

This process occurs during legitimate authentication and forms the basis of the Kerberoasting technique.

---

# Service Principal Names (SPNs)

A Service Principal Name uniquely identifies a service within an Active Directory domain.

Examples of services that may register SPNs include:

- Database services
- Web applications
- File services
- Custom enterprise applications

Service accounts associated with SPNs often require elevated permissions to perform their intended functions, making them valuable targets during security assessments.

---

# Why Service Accounts Matter

Service accounts differ from standard user accounts because they are commonly used to run applications and services.

Characteristics may include:

- Long-lived passwords.
- Elevated privileges.
- Broad access to enterprise resources.
- Infrequent password rotation.

These characteristics increase the importance of securing service accounts.

---

# Security Considerations

Weak service account passwords increase the likelihood of credential compromise.

Organizations should ensure that:

- Service accounts use strong, unique passwords.
- Passwords are rotated regularly.
- Privileged service accounts are limited to only the permissions they require.
- Unused SPNs are removed.

---

# Detection Considerations

Security teams should monitor for activity that deviates from normal authentication behavior.

Examples include:

- Unusual requests for multiple service tickets.
- Service ticket requests from unexpected hosts.
- Abnormal authentication patterns involving service accounts.

Monitoring and logging help identify suspicious activity within the domain.

---

# Mitigation

The following practices help reduce the risk associated with Kerberoasting:

- Use strong passwords for service accounts.
- Implement managed service accounts where appropriate.
- Limit the privileges assigned to service accounts.
- Review and remove unnecessary SPNs.
- Continuously monitor Kerberos authentication events.

---

# Key Takeaways

- Kerberoasting targets Kerberos service accounts associated with SPNs.
- The technique relies on normal Kerberos authentication.
- Weak service account passwords increase organizational risk.
- Proper password management and monitoring significantly reduce exposure.
- Service account security is an important component of Active Directory defense.

---

## References

- CRTA Course Material
- Active Directory Lab Exercises
