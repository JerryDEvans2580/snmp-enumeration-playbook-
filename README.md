# SNMP Enumeration Playbook

This repository documents a practical SNMP enumeration workflow using `snmpwalk`.

## Goal

The goal is to identify sensitive information exposed through SNMP, including:

- system information
- hostnames
- contact emails
- running services
- TCP listeners
- installed software
- potential attack surface

## Tools Used

- snmpwalk
- grep
- tee

## Example Command

```bash
snmpwalk -v2c -c public <target-ip>
