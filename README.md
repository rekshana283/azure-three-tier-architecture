# Azure Secure & Highly Available 3-Tier Web Application

![Project Overview](diagrams/11-project-overview.png)

![Azure](https://img.shields.io/badge/Microsoft%20Azure-Cloud-blue)
![Architecture](https://img.shields.io/badge/Project-Architecture%20Design-informational)
![Cloud Support](https://img.shields.io/badge/Focus-Cloud%20Support-success)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## Project Overview

This project presents the design of a secure, scalable, and highly available 3-tier web application architecture using Microsoft Azure.

The project is based on a fictional e-commerce application and demonstrates how a real-world cloud application can be designed, secured, monitored, and supported.

The architecture separates the application into three logical tiers:

- Web Tier
- Application Tier
- Database Tier

The project also covers Azure networking, security, identity and access management, monitoring, high availability, disaster recovery, cost optimization, and troubleshooting.

This is a design and documentation project. Azure resources are not deployed as a production environment.

---

## Architecture Overview

![Azure 3-Tier Architecture](diagrams/01-azure-3-tier-architecture.png)

The proposed architecture follows a layered approach where each tier has a specific responsibility.

### Web Tier

The Web Tier handles the user-facing part of the application and receives requests after they pass through Azure Application Gateway and Web Application Firewall.

### Application Tier

The Application Tier contains backend application services and APIs responsible for processing business logic.

### Database Tier

The Database Tier stores application data using Azure SQL Database. Database access is designed to use private connectivity rather than direct public access.

---

## High-Level Architecture


                         INTERNET USERS
                               |
                               v
                    +----------------------+
                    | Azure Application    |
                    | Gateway + WAF        |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |      WEB TIER        |
                    | Azure App Services   |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |  APPLICATION TIER    |
                    | Backend APIs / App   |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |    DATABASE TIER     |
                    |   Azure SQL Database |
                    +----------------------+

