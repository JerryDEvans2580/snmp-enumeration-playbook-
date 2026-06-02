# Targeted OID Enumeration

## Overview

During the initial SNMP walk, several MIB branches were identified as valuable sources of reconnaissance information.

Rather than reviewing the entire SNMP tree repeatedly, specific OIDs can be queried directly to retrieve targeted information.

---

# System Information

## OID

```text
1.3.6.1.2.1.1
```
Why It Matters

System information can assist with:

- OS fingerprinting
- Kernel vulnerability research
- Host identification
- Infrastructure mapping

## Command

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.1
```

## Information Retrieved

### Operating System

```text
Linux NIX02 5.4.0-90-generic
```

### Contact Information

```text
devadmin@inlanefreight.htb
```

### Hostname

```text
NIX02
```

### Description

```text
InFreight SNMP v0.91
```

---

# Network Interfaces

## OID

```text
1.3.6.1.2.1.2.2
```

## Command

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.2.2
```

## Information Retrieved

### Interfaces

```text
lo
VMware VMXNET3 Ethernet Controller
```

### Interface Status

The interface table exposed:

* Interface names
* Interface types
* MAC addresses
* Operational status
* Traffic counters

---

# ARP Information

## OID

```text
1.3.6.1.2.1.3
```

## Command

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.3
```

## Information Retrieved

### Gateway

```text
<TARGET>
```

### MAC Address

```text
00:50:56:94:A0:A0
```

This information can assist with network mapping and infrastructure identification.

---

# IP Address Enumeration

## OID

```text
1.3.6.1.2.1.4
```

## Command

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.4
```

## Information Retrieved

### IP Addresses

```text
<TARGET>
127.0.0.1
```

### Network Information

```text
<TARGET>
```

### Default Route

```text
<TARGET>
```

This branch exposed internal addressing information and routing details.

---

# TCP Listener Enumeration

## OID

```text
1.3.6.1.2.1.6.13
```

## Command

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.6.13
```

## Information Retrieved

### Listening Services

```text
22
25
110
143
993
995
3306
33060
```

### Service Mapping

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

# Why Targeted OIDs Matter

A complete SNMP walk can generate thousands of lines of output.

Targeted OIDs provide:

* Faster enumeration
* Reduced noise
* Easier analysis
* Focused information gathering

For this assessment, the most valuable branches were:

```text
1.3.6.1.2.1.1
1.3.6.1.2.1.2.2
1.3.6.1.2.1.3
1.3.6.1.2.1.4
1.3.6.1.2.1.6.13
```

These branches revealed nearly all useful reconnaissance information discovered during the engagement.
