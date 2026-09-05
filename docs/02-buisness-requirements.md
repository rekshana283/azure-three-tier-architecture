# Business Requirements

## Business Scenario

A fictional e-commerce company wants to host its customer-facing web application on Microsoft Azure.

The application should provide a secure and reliable platform for customers while allowing the technical team to monitor, maintain, and troubleshoot the environment.

The architecture is designed using a 3-tier model to separate the web, application, and database components.

---

## Functional Requirements

The application should:

- Allow customers to access the website through the internet
- Support HTTPS communication
- Serve the application's web interface
- Process backend application requests
- Store and retrieve application data
- Support increased traffic when required
- Provide controlled access to application resources

---

## Security Requirements

The architecture should:

- Protect public-facing application traffic
- Use Web Application Firewall protection
- Separate application layers through network segmentation
- Restrict unnecessary network communication
- Avoid direct public access to the database
- Secure application secrets
- Use identity-based access where possible
- Apply least-privilege permissions
- Provide controlled administrative access

---

## Availability Requirements

The application should be designed to:

- Avoid unnecessary single points of failure
- Support multiple application instances
- Use health checks
- Distribute traffic across healthy instances
- Support availability features provided by Azure services
- Provide backup and recovery capabilities

---

## Monitoring Requirements

The environment should provide visibility into:

- Application availability
- Application errors
- Backend health
- Resource utilization
- Application response time
- Database performance
- Network-related issues

Monitoring should use appropriate Azure monitoring and logging services.

---

## Operational Requirements

The support team should be able to:

- Investigate application availability issues
- Troubleshoot network connectivity
- Review application and infrastructure logs
- Identify the affected application layer
- Investigate database connectivity problems
- Review identity and access issues
- Validate changes after troubleshooting
- Document incidents and resolutions

---

## Cost Requirements

The architecture should consider:

- Resource right-sizing
- Auto-scaling where appropriate
- Removing unused resources
- Monitoring resource utilization
- Storage optimization
- Budget monitoring
- Cost Management

Cost optimization should be balanced with security, performance, and availability requirements.

---

## Requirements Summary

| Area | Requirement |
|---|---|
| Application | Customer-facing e-commerce application |
| Architecture | 3-tier architecture |
| Network | Segmented Azure Virtual Network |
| Security | Application Gateway, WAF, NSGs |
| Database | Azure SQL with private connectivity |
| Identity | Microsoft Entra ID and RBAC |
| Secrets | Azure Key Vault |
| Monitoring | Azure Monitor, Log Analytics, Application Insights |
| Availability | Multiple instances and health checks |
| Recovery | Backup and disaster recovery planning |
| Operations | Troubleshooting and technical documentation |
| Cost | Monitoring and optimization |

---

## Design Goal

The overall goal is to create an Azure architecture that is:

```text
Secure
   +
Scalable
   +
Highly Available
   +
Monitorable
   +
Supportable
   +
Cost-Aware
