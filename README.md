# AWS Cloud Security Project – IAM Policy Enforcement Lab

## Overview
This hands-on lab demonstrates the implementation of AWS cloud security controls, focusing on Identity and Access Management (IAM), monitoring, logging, and access restriction testing.  

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

## Sample IAM Policy (Audit Instance)

The following IAM policy restricts full EC2 actions to resources tagged as Audit while allowing general Describe operations on all instances. Tag creation and deletion are explicitly denied.

<pre>
```json
{
"Version": "2012-10-17",
"Statement": [
{
"Effect": "Allow",
"Action": "ec2:*",
"Resource": "*",
"Condition": {
"StringEquals": {
"ec2:ResourceTag/Env": "Audit"
}
}
},
{
"Effect": "Allow",
"Action": "ec2:Describe*",
"Resource": "*"
},
{
"Effect": "Deny",
"Action": [
"ec2:DeleteTags",
"ec2:CreateTags"
],
"Resource": "*"
}
]
}
```
</pre>



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

- [AWS console interface](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/0-AWS_console_interface.png)
- [EC2 instances deployed](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/3-EC2_instances_deployed.png)
- [IAM policy configuration](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/4-IAM_policy_audit_config.png)
- [Account alias setup](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/5-acct_Alias.png)
- [IAM users and groups](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/6-IAM_users.png)
- [EC2 instance Cloudwatch Alarm](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/7-EC2_instance_Cloudwatch_Alarm.png)
- [Access denied test results](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/8-IAM_Permission_Denied.png)
- [Access denied IAMListGroups](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/9_AccessDenied_IAM_ListGroups.png)
- [Permission validation logs](https://github.com/Yem-Tech/AWS-IAM-Cloud-Security-Project/blob/main/Screenshots/9_Permission_validation_logs.png)
  

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
Olayemi K. Owoeye
Cybersecurity Analyst
