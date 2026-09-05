# Security Design

![Security Architecture](../diagrams/04-azure-security-architecture.png)

## Overview

Security is applied across the different layers of the Azure 3-tier architecture.

The design follows a layered security approach to reduce unnecessary exposure and control access to application resources.

---

## Security Objectives

The main security objectives are:

- Protect public-facing application traffic
- Restrict unnecessary network communication
- Protect application and database resources
- Prevent direct public database access
- Secure sensitive information
- Control administrative access
- Apply least-privilege access
- Monitor security-related activity

---

## Perimeter Security

Azure Application Gateway is used as the main application entry point.

Web Application Firewall provides an additional security layer for incoming web traffic.

The intended flow is:


Internet
   |
   v
Application Gateway
   |
   v
Web Application Firewall
   |
   v
Web Tier

This helps inspect incoming requests before they reach the application.


---

## Network Security

The architecture uses network segmentation to separate application components.

Network Security Groups are used to control network traffic between the different layers.

The design follows the principle of allowing only required communication.

Web Tier
   |
   | Required Application Traffic
   v
Application Tier
   |
   | Private Database Traffic
   v
Database

Unnecessary direct communication between layers should be restricted.


---

## Database Security

Azure SQL Database is designed to avoid direct public exposure.

Private connectivity can be provided through an Azure Private Endpoint.

The intended architecture is:

Application Tier
       |
       v
Private Endpoint
       |
       v
Azure SQL Database

This reduces the need for database traffic to travel over a public endpoint.


---

## Identity Security

Microsoft Entra ID provides the identity foundation for the environment.

Authentication and authorization are treated as separate security concerns.

Azure RBAC is used to control access to Azure resources based on assigned roles.

Access should be granted according to the user's responsibilities.


---

## Least-Privilege Access

Users and services should receive only the permissions required to perform their tasks.

Example:

Administrator
     |
     v
Infrastructure Management

Cloud Support Engineer
     |
     v
Monitoring + Troubleshooting

Developer
     |
     v
Application Resources

Application Identity
     |
     v
Required Service Access

Excessive permissions should be avoided.


---

## Managed Identity

Managed Identity can be used by supported Azure services to authenticate to other Azure resources without storing credentials directly in application code or configuration.

For example, an application service can use its managed identity to access an approved Key Vault resource.


---

## Secrets Management

Azure Key Vault is included for managing sensitive information.

Examples include:

Application secrets

Certificates

API credentials

Connection information


Secrets should not be hard-coded in source code or stored in publicly accessible locations.


---

## HTTPS

The public application endpoint should use HTTPS to protect data exchanged between users and the application.

The intended flow is:

User
 |
 | HTTPS
 v
Application Gateway
 |
 v
Web Tier

Secure communication should also be considered for internal application traffic where appropriate.


---

## Security Monitoring

Security-related activity should be monitored using appropriate Azure monitoring services.

Useful areas to review include:

WAF activity

Authentication activity

Access changes

Network activity

Application errors

Resource activity

Database connectivity


Logs and metrics can help identify suspicious activity or configuration problems.


---

## Security Troubleshooting

When investigating a security-related issue, the support engineer should:

1. Identify the affected resource.


2. Check recent configuration changes.


3. Review identity and access permissions.


4. Review NSG rules.


5. Check WAF activity.


6. Review relevant logs.


7. Verify the intended access path.


8. Apply a controlled change if required.


9. Validate the result.


10. Document the investigation.




---

## Security Principles

The architecture follows these principles:

Defense in depth

Least privilege

Network segmentation

Private connectivity

Secure secrets management

Identity-based access

Controlled public exposure

Continuous monitoring



---

## Security Design Goal

The overall goal is to provide a secure application architecture where:

Public Traffic
      |
      v
Protected Entry Point
      |
      v
Isolated Application Layers
      |
      v
Private Database Connectivity
      |
      v
Protected Data

Security controls are distributed across the architecture rather than relying on a single security mechanism.
