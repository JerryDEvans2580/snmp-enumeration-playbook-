# SNMP Enumeration Methodology

## Objective

The objective of this assessment was to determine whether SNMP exposed useful information that could support further reconnaissance and attack surface analysis.

---

# Phase 1 - Service Identification

During initial reconnaissance, SNMP was identified as accessible on UDP port 161.

Rather than relying solely on traditional port scanning, SNMP was selected as the primary source of information gathering because management protocols often expose significantly more information than standard service enumeration.

---

# Phase 2 - Initial SNMP Walk

The first step was performing a broad enumeration of the SNMP tree.

```bash
snmpwalk -v2c -c public TARGET
```

The target immediately returned management data, confirming:

* SNMP was enabled
* SNMPv2c was accessible
* The community string `public` was valid
* Information disclosure was possible

---

# Phase 3 - Identifying Valuable Data

The first section of the output contained the most useful reconnaissance information.

Examples included:

### Operating System

```text
Linux NIX02 5.4.0-90-generic
```

### Administrative Contact

```text
devadmin@inlanefreight.htb
```

### Hostname

```text
NIX02
```

### System Description

```text
InFreight SNMP v0.91
```

These findings immediately provided:

* Host identification
* User enumeration opportunities
* Version information
* Internal naming conventions

---

# Phase 4 - Recognizing Output Saturation

As enumeration continued, the amount of returned data increased significantly.

Most of the additional output consisted of:

* Interface counters
* ICMP statistics
* TCP statistics
* Routing metrics
* Performance monitoring data

While useful for system administrators, this information provided limited value for initial reconnaissance.

At this point the full walk was interrupted to avoid spending excessive time reviewing low-value telemetry data.

---

# Phase 5 - Transition to Targeted Enumeration

After identifying useful areas within the MIB tree, enumeration shifted toward targeted OID queries.

This approach provided several advantages:

* Faster execution
* Less output noise
* Easier analysis
* More efficient information gathering

---

# Phase 6 - Service Discovery Through SNMP

One particularly valuable discovery was the TCP listener table.

Relevant OID:

```text
1.3.6.1.2.1.6.13
```

Query:

```bash
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.6.13
```

This revealed active services running on the target.

Discovered ports included:

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

This information was obtained directly from SNMP management data.

---

# Phase 7 - Service Validation

After discovering services through SNMP, additional validation was performed using traditional service enumeration techniques.

The purpose of validation was to:

* Confirm service availability
* Identify service versions
* Verify exposure
* Support later vulnerability assessment

SNMP acted as the primary intelligence source, while other tools were used for confirmation.

---

# Key Lessons Learned

## SNMP Can Reveal More Than Port Scanning

A traditional scan only reveals that a port is open.

SNMP can reveal:

* Hostnames
* Usernames
* Contact information
* Internal network structure
* Running services
* Network configuration

---

## Broad Enumeration Is Useful Initially

A full SNMP walk is valuable during the first stage because it quickly exposes the types of information available.

---

## Targeted Enumeration Is More Efficient

After identifying useful branches, targeted OID enumeration becomes significantly more effective than repeatedly walking the entire tree.

---

## Focus on Intelligence, Not Volume

The objective of SNMP enumeration is not to collect the largest possible amount of output.

The objective is to identify information that improves understanding of the target environment and supports future attack paths.

---

# Conclusion

The most valuable information discovered during this assessment was:

* Hostname
* Operating system
* Kernel version
* Administrative contact information
* Network configuration
* Active services

SNMP provided a detailed view of the target environment and significantly enhanced reconnaissance capabilities compared to traditional port scanning alone.
