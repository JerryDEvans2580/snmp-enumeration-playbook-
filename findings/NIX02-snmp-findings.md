# Finding: SNMP Information Disclosure via Default Community String

## Finding ID

SNMP-001

---

## Title

SNMPv2c Information Disclosure Through Default Community String

---

## Severity

Medium

---

## CVSS v3.1

### Vector

```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```

### Base Score

5.3

---

## Description

The target exposes SNMPv2c on UDP port 161 and accepts requests using the default community string `public`.

Successful authentication using this community string allowed retrieval of system, network, and service information without requiring valid user credentials.

SNMPv2c does not provide encryption or strong authentication mechanisms. As a result, sensitive management information becomes accessible to unauthenticated users.

---

## Affected Service

| Property         | Value   |
| ---------------- | ------- |
| Service          | SNMP    |
| Protocol         | UDP     |
| Port             | 161     |
| Version          | SNMPv2c |
| Community String | public  |

---

## Discovery Method

### Initial Enumeration

```bash
snmpwalk -v2c -c public <TARGET IP>
```

The target responded with management information immediately, confirming that the community string was valid.

---

## Evidence

### Host Information

```text
Linux NIX02 5.4.0-90-generic
```

### Hostname

```text
NIX02
```

### Administrative Contact

```text
devadmin@inlanefreight.htb
```

### Description

```text
InFreight SNMP v0.91
```

---

## Network Information Disclosure

SNMP exposed network-related information including:

### Local Address

```text
<TARGET IP>
```

### Loopback Address

```text
127.0.0.1
```

### Default Gateway

```text
<TARGET IP>
```

### Network Interfaces

```text
lo
VMware VMXNET3 Ethernet Controller
```

---

## Service Enumeration Disclosure

The TCP listener table exposed active services running on the host.

### Discovered Services

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

An attacker can use the disclosed information to:

* Identify operating systems
* Determine kernel versions
* Discover usernames
* Enumerate administrative contacts
* Map internal network architecture
* Identify exposed services
* Prioritize vulnerability research
* Improve attack planning

Although the vulnerability does not directly allow code execution, it significantly increases visibility into the target environment.

---

## Exploitation Scenario

An unauthenticated attacker discovers UDP port 161 exposed on the network.

Using the default community string `public`, the attacker retrieves system information, administrative contact details, internal addressing information, and active service data.

The attacker then uses this intelligence to perform focused enumeration and vulnerability assessment against the discovered services.

---

## Root Cause

The issue is caused by:

* Use of SNMPv2c
* Use of the default community string `public`
* Excessive exposure of management information

---

## Recommendations

### Disable SNMP

Disable the service if it is not required.

### Restrict Access

Allow SNMP access only from trusted management hosts.

### Replace Default Community Strings

Avoid using:

```text
public
private
```

Use long, randomly generated community strings.

### Upgrade to SNMPv3

Use SNMPv3 to provide:

* Authentication
* Encryption
* Access control

### Limit Exposed MIB Data

Restrict accessible OID trees to only required management information.

---

## Conclusion

SNMP enumeration successfully disclosed sensitive host, network, and service information using the default community string `public`.

The information obtained significantly improved reconnaissance capabilities and provided valuable intelligence for further assessment activities.
