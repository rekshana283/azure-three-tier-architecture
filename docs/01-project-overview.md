# Project Overview

![Project Overview](../diagrams/11-project-overview.png)

## Project Name

Azure Secure & Highly Available 3-Tier Web Application

## Project Type

Azure Architecture Design & Cloud Support Case Study

## Overview

This project presents the design of a secure, scalable, and highly available 3-tier web application architecture using Microsoft Azure.

The application is based on a fictional e-commerce business scenario. The goal is to demonstrate how Azure services can be combined to build a structured cloud architecture while considering networking, security, identity, monitoring, availability, disaster recovery, cost, and operational support.

This project focuses on architecture planning and technical documentation rather than production deployment.

## Architecture Model

The application follows a 3-tier architecture:

1. Web Tier
2. Application Tier
3. Database Tier

Each tier has a separate responsibility and is designed to communicate only with the required components.

## Web Tier

The Web Tier represents the customer-facing application layer.

Incoming internet traffic is designed to pass through Azure Application Gateway with Web Application Firewall before reaching the application.

The Web Tier is responsible for serving the application's user-facing content.

## Application Tier

The Application Tier contains backend application services and APIs.

This layer handles business logic and communicates with the Database Tier when application data is required.

The Application Tier is not intended to be directly accessible from the public internet.

## Database Tier

The Database Tier uses Azure SQL Database for storing application data.

Database access is designed through private connectivity to reduce unnecessary public exposure.

## Supporting Azure Services

The architecture also includes supporting services for:

- Identity management
- Access control
- Secrets management
- Network security
- Monitoring
- Logging
- Application observability
- Backup
- Disaster recovery
- Cost management

Key services include:

- Microsoft Entra ID
- Azure RBAC
- Managed Identity
- Azure Key Vault
- Azure Monitor
- Log Analytics
- Application Insights
- Azure Backup
- Azure Cost Management

## Project Objectives

The main objectives of the project are:

- Understand Azure 3-tier architecture
- Design a secure cloud network
- Apply network segmentation
- Protect public application traffic
- Prevent unnecessary database exposure
- Apply identity and access management
- Design monitoring and logging
- Plan for high availability
- Understand backup and disaster recovery
- Identify cloud cost optimization opportunities
- Practice real-world cloud troubleshooting
- Document technical design decisions

## Cloud Support Perspective

The project also focuses on how a Cloud Support Engineer would investigate issues across different layers.

For example, when an application is unavailable, troubleshooting should not immediately assume that the application itself is the problem.

The investigation can move through:

```text
User
  |
  v
Application Gateway / WAF
  |
  v
Web Tier
  |
  v
Application Tier
  |
  v
Private Network Connectivity
  |
  v
Database
  |
  v
Logs / Metrics / Monitoring
