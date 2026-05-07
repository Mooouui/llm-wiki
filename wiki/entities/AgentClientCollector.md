---
title: "Agent Client Collector"
type: entity
tags: [ServiceNow, CMDB, Discovery, ITOM, agent-based, real-time]
sources: [ingest-data-into-the-cmdb]
last_updated: 2026-04-27
---

# Agent Client Collector (ACC)

ServiceNow Agent Client Collector (ACC) is a lightweight agent-based solution for real-time discovery and monitoring of infrastructure components including servers, cloud resources, and endpoints. It is part of the [[ServiceNow]] ITOM suite.

## Key Differentiators from [[ServiceNowDiscovery]]

- **Agent-based** — requires an agent installed on each target host, unlike the agentless Discovery
- **Real-time** — provides continuous visibility, not schedule-based
- **Software utilization data** — collects usage metrics not available through agentless methods, supporting Software Asset Management (SAM)

## Use Cases

- Visibility and Monitoring
- Software Asset Management
- Security Incident Response
- Service Management
- Discovery of intermittently connected workstations
- Discovery in secure networks where external discovery solutions are prohibited

## Sources

- [[ingest-data-into-the-cmdb|Ingest Data into the CMDB]] — ACC overview and feature set
