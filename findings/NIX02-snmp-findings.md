# NIX02 - SNMP Information Disclosure

## Finding Summary

The target exposed SNMPv2c using the default community string `public`, allowing unauthenticated access to sensitive system and network information.

---

## Severity

Medium

---

## Service Information

| Field            | Value   |
| ---------------- | ------- |
| Service          | SNMP    |
| Protocol         | UDP     |
| Port             | 161     |
| Version          | SNMPv2c |
| Community String | public  |

---

## Discovery

SNMP was identified during network enumeration.

The service accepted requests using the default community string `public`.

Enumeration was performed using:

```bash
snmpwalk -v2c -c public <TARGET IP>
```

---

## Evidence

### Host Information

```text
Hostname: NIX02
```

```text
Linux NIX02 5.4.0-90-generic
```

### Administrative Contact

```text
devadmin@inlanefreight.htb
```

### Custom Description

```text
InFreight SNMP v0.91
```

---

## Network Information Disclosed

The SNMP service exposed:

* Internal IP addresses
* Network interfaces
* Routing information
* ARP information
* Interface statistics

### Network Interfaces

```text
lo
VMware VMXNET3 Ethernet Controller
```

### IP Addresses

```text
<TARGET IP>
127.0.0.1
```

### Gateway

```text
<TARGET IP>
```

---

## Service Enumeration via SNMP

The TCP listener table exposed active services.

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

## Impact

An attacker can use this information to:

* Enumerate usernames
* Identify operating systems
* Determine kernel versions
* Discover internal network architecture
* Identify exposed services
* Research vulnerabilities
* Plan further attacks

Although SNMP itself did not provide direct code execution, it significantly improved visibility into the target environment.

---

## Risk Analysis

The primary issue is the exposure of SNMPv2c using a publicly known community string.

SNMPv2c does not provide:

* Encryption
* Strong authentication
* Granular access control

As a result, sensitive management information becomes available to unauthenticated users.

---

## Recommendations

1. Disable SNMP if not required.
2. Remove default community strings.
3. Restrict SNMP access using ACLs.
4. Migrate to SNMPv3.
5. Enable authentication and encryption.
6. Limit exposed MIB views to only necessary data.

---

## Conclusion

SNMP enumeration successfully revealed valuable reconnaissance information including host details, contact information, network configuration, and active services.

The exposed data could be leveraged to support additional enumeration, service-specific attacks, and vulnerability research during a penetration test.
