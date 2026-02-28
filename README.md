# AWS Cloud Security Project – IAM Policy Enforcement Lab

## Overview
This project demonstrates hands-on implementation of cloud security controls within :contentReference[oaicite:0]{index=0}, focusing on Identity and Access Management (IAM), monitoring, logging, and access restriction testing.  

The objective was to design and validate a least-privilege access model that restricts specific actions on designated EC2 instances while allowing permitted operations on others.

---

## Project Objectives
- Implement least-privilege IAM policies  
- Configure monitoring and logging services  
- Restrict unauthorized resource actions  
- Validate access controls through testing  
- Strengthen cloud security posture  

---

## Environment Components Configured

### Identity & Access Security
- Created IAM users and groups  
- Configured administrator account with MFA  
- Assigned users to permission-based groups  
- Tested real access scenarios and restrictions  

### Compute Infrastructure
- Launched EC2 instances:
  - HyperTechai-Audit-Ashafa (Audit Server)
  - HyperTechai-Sales-Bryan (Sales Server)
- Applied instance tagging strategy for access control logic  

### Monitoring & Alerting
- Configured CloudTrail logging
- Set up SNS notification system
- Created EventBridge rule for automated event monitoring

### Account Configuration
- Configured account alias for simplified login access  

---

## Tagging Strategy
| Instance | Tag Key | Tag Value |
|--------|--------|-----------|
|HyperTechai-Audit-Ashafa | Environment | Audit |
|HyperTechai-Sales-Bryan | Environment | Sales |

Tags were used to control policy logic and enforce targeted permissions.

---

## IAM Policy Implementation
A custom JSON IAM policy was created to:

- Deny start/stop actions on the **HyperTechai-Audit-Ashafa** instance  
- Allow start/stop actions on the **HyperTechai-Sales-Bryan** instance  

This demonstrates real-world access segmentation using resource-level permissions.

---

## Access Testing Results

| Action | Expected | Result |
|------|---------|-------|
Stop HyperTechai-Audit-Ashafa Instance | Denied | Access denied |
Start HyperTechai-Audit-Ashafa Instance | Denied | Access denied |
Stop HyperTechai-Sales-Bryan Instance | Allowed | Success |
Start HyperTechai-Sales-Bryan Instance | Allowed | Success |

Additional permission tests confirmed access denial for restricted API calls including:

- `iam:GetAccountSummary`
- `iam:ListMFADevices`
- `iam:ListAccountAliases`
- Unauthorized compute optimization actions
- Service Catalog access attempts

---

## Screenshots Included
This repository contains evidence screenshots of:

- AWS console interface
- EC2 instances deployed
- IAM policy configuration
- Account alias setup
- IAM users and groups
- EC2 instance Cloudwatch Alarm
- Access denied test results
- Access denied IAMListGroups
- Permission validation logs
  

---

## Security Concepts Demonstrated
- Principle of Least Privilege
- Role-Based Access Control
- Cloud Logging & Monitoring
- Identity Federation Preparation
- Resource-Level Permissions
- Security Validation Testing

---

## Project Workflow Summary
1. Created cloud account and secured root access with MFA  
2. Created admin IAM user and enabled MFA  
3. Created IAM group and users  
4. Built EC2 infrastructure  
5. Applied tagging structure  
6. Created custom IAM policy  
7. Configured CloudTrail, SNS, and EventBridge  
8. Tested user access permissions and restrictions  

---

## Key Skills Demonstrated
- Cloud Security Implementation
- IAM Policy Design
- JSON Policy Writing
- Access Control Testing
- AWS Monitoring Tools
- Security Validation Procedures

---

## Purpose
This lab simulates real-world cloud security engineering tasks and demonstrates practical knowledge of designing, enforcing, and validating access control policies in enterprise cloud environments.

---

## Author
Cybersecurity & Cloud Security Enthusiast  
Hands-on lab portfolio demonstrating practical infrastructure security skills.
