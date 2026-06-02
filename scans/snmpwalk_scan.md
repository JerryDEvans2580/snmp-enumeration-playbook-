# Basic SNMP Enumeration

## Objective

The objective of this phase was to enumerate information exposed through SNMP and identify valuable reconnaissance data without authentication.

---

## Initial Enumeration

SNMP enumeration was performed using the default community string `public`.

```bash
snmpwalk -v2c -c public TARGET
```

The target immediately responded with SNMP data, confirming that:

* SNMP was enabled
* SNMPv2c was accessible
* The community string `public` was valid
* Information disclosure was possible

---

## Host Information Discovery

The first section of the output revealed valuable host information.

### Operating System

```text
Linux NIX02 5.4.0-90-generic
```

Identified:

* Linux operating system
* Ubuntu distribution
* Kernel version 5.4.0-90-generic

### Administrative Contact

```text
devadmin <devadmin@inlanefreight.htb>
```

Identified:

* Internal email address
* Potential username
* Administrative contact information

### Hostname

```text
NIX02
```

Identified:

* Internal hostname
* Naming convention used within the environment

### System Description

```text
InFreight SNMP v0.91
```

Identified:

* Custom system description
* Possible internal application naming

---

## Network Enumeration

SNMP exposed network-related information.

### Network Interfaces

Discovered interfaces:

```text
lo
VMware VMXNET3 Ethernet Controller
```

This information helped map the internal network configuration.

---

## TCP Listener Enumeration

```text
Relevant OID:
1.3.6.1.2.1.6.13
```

```bash
snmpwalk -v2c -c public <TARGET IP> 1.3.6.1.2.1.6.13
```

Discovered listening services:

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

Unlike traditional port scanning, these services were identified directly through SNMP management data.

---

## Observations

A full SNMP walk generated a very large amount of output.

The most valuable information was discovered in:

* System information
* Contact information
* Network configuration
* TCP listener tables

Later sections primarily contained counters, statistics, and protocol telemetry.

---
## Lessons During Enumeration

The full SNMP walk generated a large amount of output.

Most valuable information appeared near the beginning of the enumeration output.

After identifying host information and active services, continuing the full walk produced mostly counters and monitoring data.

This demonstrated the value of transitioning from broad enumeration to targeted OID-based enumeration.

## Conclusion

SNMP enumeration successfully exposed significant reconnaissance data including:

* Host information
* Administrative contacts
* Internal addressing
* Network configuration
* Active services

The information gathered during this phase provided a clear understanding of the target environment and supported further service-specific enumeration.


