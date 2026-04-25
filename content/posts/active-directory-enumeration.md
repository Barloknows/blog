---
title: "Active Directory Enumeration from Zero"
date: 2025-04-18
draft: false
categories: ["Study Notes"]
tags: ["Active Directory", "CPTS", "Enumeration", "BloodHound"]
excerpt: "A complete walkthrough of AD enumeration — from initial foothold to domain user discovery using BloodHound, ldapdomaindump, and manual LDAP queries."
---

When starting a penetration test in an Active Directory environment, enumeration is everything. Before a single exploit is fired, you need to build a map of the domain — users, groups, computers, trust relationships, and ACL edges that could become attack paths.

## Initial Reconnaissance

Assuming you have a valid domain user credential (even a low-priv one), start by dumping basic domain information over LDAP. The fastest route is `ldapdomaindump`:

```bash
# Quick full-domain snapshot
$ ldapdomaindump -u 'DOMAIN\user' \
    -p 'password' -o ./loot/ dc01.domain.local
```

This outputs HTML and JSON files giving you users, groups, computers, and password policies at a glance.

## BloodHound Collection

For graph-based path analysis, BloodHound is irreplaceable. Run SharpHound from a Windows host in the domain, or use `bloodhound-python` remotely:

```bash
$ bloodhound-python \
    -u user -p password -d domain.local \
    -ns 10.10.10.1 -c All
```

> Use `-c DCOnly` for a quick pass first. Full collection with `-c All` generates significantly more traffic and is easier to detect.

## Manual LDAP Queries

Sometimes you need targeted queries that automated tools miss:

```bash
# Kerberoastable accounts
$ ldapsearch -H ldap://dc01 \
    -b 'DC=domain,DC=local' \
    '(&(objectClass=user)(servicePrincipalName=*))' \
    sAMAccountName servicePrincipalName
```

## Key Takeaways

Enumeration isn't a box to tick — it compounds. Each piece of information shapes what you look at next. Build your map before you start pulling at threads.
