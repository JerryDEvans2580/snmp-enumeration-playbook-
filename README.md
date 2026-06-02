# SNMP Enumeration Playbook

## Overview

This repository documents a practical SNMP enumeration workflow against a Linux target exposing SNMPv2c with the default community string `public`.

The objective was to identify information disclosure vulnerabilities and enumerate services, host information, and network details through SNMP.

---

## Initial Enumeration

The initial enumeration was performed using:

```bash
snmpwalk -v2c -c public <TARGET IP>
```

The target responded successfully, confirming that the community string `public` was valid and that SNMP information could be retrieved without authentication.

---

## Information Discovered

### Host Information

| Field            | Value                                                           |
| ---------------- | --------------------------------------------------------------- |
| Hostname         | NIX02                                                           |
| Operating System | Ubuntu Linux                                                    |
| Kernel Version   | 5.4.0-90-generic                                                |
| Contact          | [devadmin@inlanefreight.htb](mailto:devadmin@inlanefreight.htb) |
| Description      | InFreight SNMP v0.91                                            |

### Network Information

Discovered network interfaces:

* Loopback (lo)
* VMware VMXNET3 Ethernet Controller

Discovered IP addresses:

* <TARGET IP>
* 127.0.0.1

Discovered gateway:

* <TARGET IP>

### Exposed Services

The TCP listener table revealed the following services:

| Port  | Service          |
| ----- | ---------------- |
| 22    | SSH              |
| 25    | SMTP             |
| 110   | POP3             |
| 143   | IMAP             |
| 993   | IMAPS            |
| 995   | POP3S            |
| 3306  | MySQL            |
| 33060 | MySQL X Protocol |

---

## Security Impact

The exposed SNMP service allowed unauthenticated access to:

* Hostname information
* Operating system details
* Kernel version
* Administrative contact information
* Network configuration
* Listening services
* Internal addressing information

This information can be used to support:

* Attack surface mapping
* Service enumeration
* Username enumeration
* Vulnerability research
* Further exploitation planning

---

## Tools Used

* snmpwalk
* grep
* tee
* less

---

## Key Lesson

SNMP enumeration is not simply collecting large amounts of output.

The primary goal is to identify valuable intelligence that can support later phases of an assessment, including service discovery, user enumeration, and vulnerability research.

## Next Steps

Based on the discovered services:

### SSH
- Version identification
- Authentication testing

### SMTP
- VRFY
- EXPN
- User enumeration

### IMAP / POP3
- Capability enumeration
- Authentication testing

### MySQL
- Version detection
- Access validation
