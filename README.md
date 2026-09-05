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
Project Objectives

The main objectives of this project are:

Design a real-world Azure 3-tier application architecture

Separate application components using network segmentation

Secure public and internal application traffic

Apply identity and access management principles

Design monitoring, logging, and alerting

Plan for high availability and disaster recovery

Identify practical cloud cost optimization opportunities

Develop troubleshooting procedures and document architecture decisions



---

Business Scenario

A fictional e-commerce company wants to host a customer-facing web application on Microsoft Azure.

The application should:

Allow customers to access the website through the internet

Support secure HTTPS communication

Separate frontend, backend, and database components

Prevent direct public access to the database

Support increased application traffic

Provide monitoring and logging

Protect application secrets

Provide backup and recovery capabilities

Control administrative access

Maintain reasonable cloud costs


A 3-tier architecture was selected to meet these requirements.


---

Network Design



The architecture uses an Azure Virtual Network to provide logical network isolation.

The network is divided into separate logical areas for the different application layers.

Web Subnet

The Web Subnet contains the web-facing application components.

Application Subnet

The Application Subnet contains backend application and API services.

Database Connectivity

The database layer uses private connectivity so that database services are not directly exposed to the public internet.

Network Security Groups

Network Security Groups are used to control traffic between the different application layers.

The intended traffic pattern is:

Internet
   |
   v
Web Tier
   |
   v
Application Tier
   |
   v
Database Tier

Each layer should only allow the communication required for its function.


---

Application Traffic Flow



A typical application request follows these steps:

1. The user sends an HTTPS request.


2. The request reaches Azure Application Gateway.


3. Web Application Firewall evaluates the incoming request.


4. Valid traffic is forwarded to the Web Tier.


5. The Web Tier communicates with the Application Tier.


6. The Application Tier accesses Azure SQL Database through private connectivity.


7. The response travels back through the application layers.


8. The user receives the application response.



This layered flow reduces unnecessary direct communication between external users and internal services.


---

Security Architecture



Security is applied across multiple layers of the architecture.

Network Security

The design includes:

Azure Virtual Network

Network Security Groups

Private Endpoints

Network segmentation

Restricted traffic paths


Application Security

The application entry point uses:

HTTPS

Azure Application Gateway

Web Application Firewall

Secure backend communication


Database Security

The database is designed to avoid direct public exposure.

Private connectivity is preferred for communication between the application and database layers.

Secrets Management

Azure Key Vault is included for securely managing sensitive information such as:

Application secrets

Certificates

API credentials

Connection information


Sensitive information should not be stored directly in application source code.


---

Identity & Access Management



Microsoft Entra ID is used as the identity foundation of the architecture.

The design applies:

Authentication

Authorization

Azure RBAC

Managed Identity

Least-privilege access


Example Access Model

Role	Intended Access

Administrator	Infrastructure management
Cloud Support Engineer	Monitoring and troubleshooting
Developer	Application resources
Application Identity	Required service access


Managed Identity can be used where supported to reduce the need for storing credentials in application configuration.


---

Monitoring & Observability



Monitoring is an important part of the operational design.

The architecture includes:

Azure Monitor

Log Analytics

Application Insights

Metrics

Application logs

Alerts


Monitoring Areas

Component	Monitoring Areas

Application Gateway	Requests, errors, backend health
Web Tier	CPU, memory, availability
Application Tier	API failures, latency
Database	Connections, performance
Application	Exceptions, response time


Example Alerts

Possible alerts include:

High resource utilization

Increased response time

Application errors

Backend health failures

Database connectivity problems

Availability issues


Centralized monitoring helps support engineers identify the affected layer before making configuration changes.


---

High Availability



The architecture considers high availability by avoiding unnecessary single points of failure.

The design includes:

Multiple application instances

Health checks

Load distribution

Auto-scaling considerations

Availability Zones where supported

Database high availability capabilities


If one application instance becomes unavailable, traffic can be directed towards healthy instances.

Example Failure Scenario

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


---

Backup & Disaster Recovery



Backup and disaster recovery are considered as part of the overall architecture.

The design includes:

Database backup

Recovery planning

Azure Backup where applicable

Disaster recovery strategy

Recovery procedures

RTO and RPO considerations


RTO

Recovery Time Objective defines how quickly the service should be restored after a failure.

RPO

Recovery Point Objective defines the acceptable amount of recent data loss.

Actual RTO and RPO values should be determined according to business requirements.


---

Cost Optimization



Cost management is included as part of the architecture design.

The project considers:

Right-sizing resources

Auto-scaling

Removing unused resources

Monitoring resource utilization

Storage optimization

Azure Cost Management

Budget alerts


The objective is to balance:

Security
    +
Performance
    +
Availability
    +
Cost

Cost optimization should not compromise required security or availability.


---

Troubleshooting & Cloud Support



A major part of this project is the operational troubleshooting approach.

The troubleshooting process follows:

Identify
   |
   v
Collect Evidence
   |
   v
Isolate the Layer
   |
   v
Check Logs and Metrics
   |
   v
Test the Suspected Cause
   |
   v
Apply Controlled Fix
   |
   v
Validate
   |
   v
Document


---

Scenario 1 — Application Not Accessible

Symptoms

Users report that the website cannot be opened.

Investigation

Check Application Gateway availability

Check listener configuration

Check WAF activity

Check backend health

Check Web Tier availability

Check NSG rules

Review application logs

Check recent configuration changes


Possible Causes

Incorrect listener configuration

Backend unavailable

NSG blocking traffic

Application failure

Incorrect routing



---

Scenario 2 — Application Cannot Connect to Database

Symptoms

The application cannot retrieve or store data.

Investigation

Check database availability

Check Private Endpoint

Check DNS resolution

Check NSG rules

Check connection configuration

Review application logs

Check recent network changes


Possible Causes

DNS resolution issue

Network rule blocking traffic

Database unavailable

Incorrect connection configuration



---

Scenario 3 — Application Is Slow

Symptoms

Users report high application response times.

Investigation

Check Application Insights

Review application response time

Check CPU and memory usage

Check API latency

Review database performance

Check traffic volume

Review scaling configuration


Possible Causes

High resource utilization

Slow backend API

Database performance issue

Increased traffic

Application issue



---

Scenario 4 — Unauthorized Access

Symptoms

A user can access a resource they should not be able to access.

Investigation

Review Microsoft Entra ID identity

Review RBAC assignments

Check inherited permissions

Review Managed Identity access

Check Key Vault permissions

Review recent access changes


Possible Causes

Excessive RBAC permissions

Incorrect role assignment

Inherited access

Incorrect identity configuration



---

Azure Services in the Design

Azure Service	Purpose

Azure Virtual Network	Network isolation
Application Gateway	Application traffic routing
Web Application Firewall	Web traffic protection
Azure App Service / Compute	Application hosting
Azure SQL Database	Relational database
Private Endpoint	Private service connectivity
Network Security Group	Network traffic filtering
Microsoft Entra ID	Identity management
Azure RBAC	Authorization
Managed Identity	Secure service authentication
Azure Key Vault	Secret management
Azure Monitor	Infrastructure monitoring
Log Analytics	Centralized logging
Application Insights	Application monitoring
Azure Backup	Backup strategy
Cost Management	Cost monitoring



---

Design Decisions

Requirement	Design Decision

Secure public access	Application Gateway + WAF
Application separation	Three-tier architecture
Network isolation	Separate subnets
Database protection	Private connectivity
Identity management	Microsoft Entra ID
Authorization	Azure RBAC
Secret management	Azure Key Vault
Monitoring	Azure Monitor + Log Analytics
Application monitoring	Application Insights
Availability	Multiple application instances
Recovery	Backup and DR planning
Cost control	Cost Management + optimization



---

Project Documentation

Detailed documentation is maintained in the docs directory.

Project Planning

Project Overview

Business Requirements


Architecture

Architecture Design

Network Design


Security

Security Design

Identity & Access Management


Operations

Monitoring & Observability

High Availability

Backup & Disaster Recovery


Cost & Support

Cost Optimization

Troubleshooting Guide

Design Decisions



---

Skills Demonstrated

Azure

Azure Architecture

Azure Networking

Application Gateway

Web Application Firewall

Azure SQL

Azure Monitor

Microsoft Entra ID

Azure RBAC

Azure Key Vault

Private Endpoints


Cloud Support

Troubleshooting methodology

Network connectivity analysis

Log analysis

Monitoring and alerting

Incident investigation

Root cause analysis

Technical documentation


Architecture

3-tier architecture

Network segmentation

Security design

High availability

Disaster recovery

Cost optimization



---

Project Scope

This repository represents an Azure architecture design and documentation case study.

The architecture is designed for learning and portfolio purposes.

Azure resources were not deployed as a production environment.

The project focuses on understanding how Azure services can be selected, connected, secured, monitored, and supported in a real-world application scenario.


---

Author

Rekshana Fathima

Aspiring Cloud & DevOps Professional

Areas of Interest

Cloud Computing

Microsoft Azure

AWS

Cloud Support

DevOps

Infrastructure

Troubleshooting

