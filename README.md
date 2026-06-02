# SNMP Enumeration Playbook

## Overview

This repository documents a practical SNMP enumeration workflow against a Linux target exposing SNMPv2c with the default community string `public`.

The objective was to assess the information disclosure risks associated with exposed SNMPv2c services and identify data that could support further attack surface analysis.

---

## Enumeration Workflow

1. Validate SNMP access
2. Perform broad SNMP enumeration
3. Identify valuable host information
4. Enumerate network information
5. Identify active services
6. Map the attack surface
7. Plan follow-up enumeration

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
```bash
* <TARGET IP>
* 127.0.0.1
```
```bash
Discovered gateway:

* <TARGET IP>
```

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

## Attack Surface Identified

The following services were identified through SNMP:

- SSH
- SMTP
- POP3
- IMAP
- IMAPS
- POP3S
- MySQL
- MySQL X Protocol

These services represent potential entry points for further enumeration and vulnerability assessment.

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

- snmpwalk
- grep
- tee
- less

## Techniques Used

- SNMP Enumeration
- Information Disclosure Analysis
- Service Discovery
- Attack Surface Mapping

---

## Key Lesson

SNMP enumeration is not simply collecting large amounts of output.

The primary goal of enumeration is not to collect the largest amount of data, but to identify intelligence that supports future attack paths, service-specific enumeration, and vulnerability research.

## Why SNMP Matters

Unlike traditional port scanning, SNMP can reveal:

- Hostnames
- Administrative contacts
- Operating system details
- Network configuration
- Running services
- Internal addressing information

This makes SNMP a valuable source of reconnaissance data during a penetration test.

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
