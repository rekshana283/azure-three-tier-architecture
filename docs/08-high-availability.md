# High Availability

![High Availability Design](../diagrams/07-high-availability-design.png)

## Overview

High availability is an important consideration in the design of the Azure 3-tier application.

The architecture is designed to reduce unnecessary single points of failure and maintain application availability when individual components experience problems.

---

## High Availability Objectives

The design aims to:

- Reduce single points of failure
- Distribute application traffic
- Use multiple application instances
- Monitor backend health
- Support automatic scaling where appropriate
- Use Azure availability capabilities
- Provide database availability and recovery options

---

## Application Availability

The Web and Application Tiers can use multiple application instances.

A load distribution component such as Azure Application Gateway can direct traffic towards healthy backend instances.

Example:


                    Application Gateway
                           |
              +------------+------------+
              |                         |
              v                         v
       Application A              Application B
          HEALTHY                    HEALTHY

If one instance becomes unavailable, traffic can continue towards another healthy instance.


---

## Health Checks

Health checks help determine whether backend application instances are available to receive traffic.

The application gateway can use backend health information when distributing requests.

Example:

Backend Instance
       |
       v
   Health Check
       |
   +---+---+
   |       |
 Healthy  Unhealthy
   |       |
   v       X
Receive   Remove
Traffic   from Traffic


---

## Failure Scenario

Consider a situation where one application instance stops responding.

Application Instance A
        |
        X
     FAILURE

Application Instance B
        |
        v
     HEALTHY

        |
        v

Application Gateway
        |
        v

Traffic continues to healthy instance

This reduces the impact of an individual instance failure.


---

## Auto-Scaling Considerations

The architecture considers scaling application capacity based on workload.

Auto-scaling can help increase application capacity when demand increases and reduce unnecessary capacity when demand decreases.

Scaling decisions should consider:

CPU utilization

Memory utilization

Request volume

Application response time

Business requirements



---

## Availability Zones

Where supported by the selected Azure services and region, Availability Zones can be considered to improve resilience against failures affecting a single physical location within a region.

The actual availability-zone design depends on Azure service capabilities and regional support.


---

## Database Availability

Azure SQL Database provides built-in availability capabilities as part of the managed service.

The architecture also considers:

Database backup

Recovery options

Service availability

Disaster recovery planning


Database availability requirements should be aligned with business requirements.


---

## Monitoring Availability

Availability should be monitored using Azure Monitor and Application Insights.

Important areas include:

Application availability

Backend health

Failed requests

Response time

Resource utilization

Database connectivity



---

## High Availability Troubleshooting

When an application component becomes unavailable, the investigation can follow:

Application Issue
       |
       v
Check Application Gateway
       |
       v
Check Backend Health
       |
       v
Identify Failed Instance
       |
       v
Check Application Logs
       |
       v
Check Resource Health
       |
       v
Check Recent Changes
       |
       v
Restore / Replace Unhealthy Component
       |
       v
Validate Application


---

## High Availability Benefits

The design provides:

Reduced dependency on a single application instance

Better traffic distribution

Health-based routing

Improved resilience

Scaling considerations

Better operational visibility

Recovery planning



---

## Design Goal

The overall high availability approach is:

Multiple Instances
       +
Health Checks
       +
Traffic Distribution
       +
Monitoring
       +
Recovery Planning
       =
Improved Application Resilience

High availability is treated as an architectural requirement rather than relying on a single component to provide resilience.
