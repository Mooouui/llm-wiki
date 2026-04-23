---
title: "CMDB"
type: concept
tags: [ITSM, configuration-management, data-integrity]
sources: [configure-the-cmdb]
last_updated: 2026-04-22
---

# CMDB (Configuration Management Database)

A Configuration Management Database (CMDB) is a centralized repository that stores information about configuration items (CIs) — hardware, software, network assets, and their relationships — within an organization's IT environment.

## Core Principles

- **Start simple, grow incrementally** — building a comprehensive CMDB immediately is a common mistake; begin with core use cases and expand
- **Data integrity is paramount** — inaccurate CMDB data causes downstream reports and processes to fail
- **Multiple sources require governance** — when Discovery, import sets, and third-party tools all write to the CMDB, the risk of duplicates and inconsistencies increases sharply

## Key Components

- **CI Classes** — hierarchical taxonomy of configuration items (e.g., Server → Linux Server → specific subclass). Extend existing classes rather than creating new ones to avoid license, governance, and interoperability issues.
- **CI Attributes** — properties of a CI (serial number, host name, IP address, RAM, etc.)
- **Relationships** — connections between CIs (dependency, containment, etc.)
- **Identification Rules** — define how CIs are uniquely identified using stable attributes
- **Reconciliation Rules** — determine which data source is authoritative for each class/attribute

## Key Tools

- [[ServiceNow|CI Class Manager]] — centralized management interface
- [[IRE|Identification & Reconciliation Engine]] — processes all data before it enters the CMDB
- [[MultisourceCMDB|CMDB 360]] — tracks all discovery source values at the attribute level

## Sources

- [[configure-the-cmdb|Configure the CMDB]] — comprehensive configuration guide
