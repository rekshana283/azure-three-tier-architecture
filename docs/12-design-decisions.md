# Design Decisions

## Overview

This document explains the main architectural decisions made for the Azure 3-tier web application design.

Each decision is based on security, availability, scalability, monitoring, supportability, and cost considerations.

---

## Decision 1: Use 3-Tier Architecture

The application is separated into:


Web Tier
   |
   v
Application Tier
   |
   v
Database Tier

Reason

Separating the application into logical layers improves:

Security

Maintainability

Scalability

Troubleshooting

Access control



---

## Decision 2: Use Application Gateway

Azure Application Gateway is selected as the main application entry point.

Reason

It provides:

Application-level traffic routing

Backend health monitoring

HTTPS capabilities

Integration with Web Application Firewall


This provides a controlled entry point before traffic reaches the application.


---

## Decision 3: Use Web Application Firewall

Web Application Firewall is included at the application entry point.

Reason

It provides an additional security layer for incoming web traffic and can help protect against common web-based attacks.

WAF activity can also be reviewed during troubleshooting.


---

## Decision 4: Separate Network Layers

The architecture uses separate network areas for the Web and Application Tiers.

Reason

Network segmentation helps:

Reduce unnecessary communication

Limit exposure

Apply different security rules

Simplify troubleshooting



---

## Decision 5: Use Network Security Groups

Network Security Groups are used to control network traffic.

Reason

NSGs allow the architecture to restrict unnecessary inbound and outbound communication.

Rules should follow the principle of least access.


---

## Decision 6: Use Private Database Connectivity

The database is designed to use private connectivity through an Azure Private Endpoint where applicable.

Reason

The database should not require direct public internet exposure.

Private connectivity helps reduce the public attack surface and provides a controlled network path to the database.


---

## Decision 7: Use Microsoft Entra ID and Azure RBAC

Microsoft Entra ID is used as the identity foundation and Azure RBAC is used for resource authorization.

Reason

This provides centralized identity and role-based access control.

Permissions can be assigned according to responsibilities and resource scope.


---

## Decision 8: Use Managed Identity

Managed Identity is preferred for supported Azure service-to-service authentication.

Reason

It reduces the need to store credentials directly in application code or configuration.

This supports better security and credential management.


---

## Decision 9: Use Azure Key Vault

Azure Key Vault is included for sensitive information.

Reason

Secrets, certificates, and other sensitive values should not be hard-coded into application source code.

Key Vault provides a dedicated service for managing protected information.


---

## Decision 10: Use Azure Monitor and Log Analytics

Azure Monitor and Log Analytics are included for infrastructure and operational monitoring.

Reason

Centralized monitoring helps support engineers:

Detect issues

Review resource health

Analyze logs

Investigate incidents

Identify performance problems



---

## Decision 11: Use Application Insights

Application Insights is included for application-level observability.

Reason

Infrastructure metrics alone may not explain application problems.

Application Insights can provide visibility into:

Requests

Response times

Exceptions

Failed requests

Application availability



---

## Decision 12: Design for High Availability

Multiple application instances and health-based traffic distribution are considered.

Reason

A single application instance can become a single point of failure.

Using multiple instances can improve resilience when an individual instance becomes unavailable.


---

## Decision 13: Consider Availability Zones

Availability Zones are considered where supported by the selected Azure services and region.

Reason

They can improve resilience against failures affecting a single physical location within an Azure region.

The final implementation should be based on service and regional availability.


---

## Decision 14: Include Backup and Disaster Recovery

Backup and recovery planning are included as part of the architecture.

Reason

Application availability alone does not protect against data loss or major failures.

The design therefore considers:

Database backups

Recovery procedures

Backup retention

RTO

RPO

Recovery testing



---

## Decision 15: Include Cost Management

Cost monitoring is considered throughout the architecture.

Reason

Cloud resources can generate unnecessary costs when they are oversized, unused, or poorly monitored.

The design therefore considers:

Right-sizing

Resource cleanup

Auto-scaling

Storage optimization

Budget monitoring

Cost analysis



---

## Decision 16: Focus on Supportability

The architecture includes troubleshooting and operational considerations.

Reason

A production-style architecture should not only be designed to work; it should also be designed to be monitored, investigated, and maintained.

The design therefore includes:

Monitoring
   +
Logging
   +
Troubleshooting
   +
Documentation
   =
Supportable Architecture


---

## Security vs Cost

Security controls should not be removed simply to reduce cost.

Cost optimization should consider the potential operational and security impact of each change.

The preferred approach is:

Security
    +
Availability
    +
Performance
    +
Cost Awareness


---

## Design Trade-Offs

Architectural decisions may involve trade-offs.

For example:

Area	Consideration

Security	More controls can increase complexity
Availability	Redundancy can increase resource usage
Performance	Higher capacity can increase cost
Monitoring	More telemetry can increase data volume
Private Connectivity	Improves isolation but requires network and DNS planning
Auto-Scaling	Improves elasticity but requires suitable scaling rules


The final configuration should be based on actual workload and business requirements.


---

## Overall Design Principles

The architecture follows these principles:

Security by design

Least privilege

Network segmentation

Private connectivity

Identity-based access

High availability

Observability

Disaster recovery planning

Cost awareness

Operational supportability



---

## Final Architecture Goal

The overall design aims to provide:

Secure
   +
Scalable
   +
Highly Available
   +
Observable
   +
Recoverable
   +
Supportable
   +
Cost-Aware

The architecture is intended as a design and documentation case study and should be adapted to actual business, security, compliance, workload, and regional requirements before production implementation.
