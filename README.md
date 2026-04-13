# AWS Security Lab

## Overview

This project demonstrates the design, implementation, and security analysis of an AWS cloud environment. It focuses on identifying, detecting, and remediating common cloud misconfigurations across key security domains.

The environment was intentionally designed with a secure baseline and then modified to simulate real-world security incidents.

---

## Architecture

The architecture consists of:

- A VPC with public and private subnets
- An EC2 instance deployed in the public subnet for controlled testing
- An S3 bucket used for storage testing (external to the VPC)
- IAM roles and policies enforcing least-privilege access
- CloudTrail logging to a dedicated S3 bucket
- AWS Config for compliance monitoring
- CloudWatch for metrics visibility

---

## Security Tests

This project includes the following security scenarios:

### 1. S3 Public Exposure
- Simulated a misconfiguration allowing public read access to an S3 bucket
- Evaluated risks such as unauthorized access and data exposure
- Detected using AWS Config and CloudTrail
- Remediated by restoring secure access settings

---

### 2. IAM Over-Permission
- Simulated an over-permissive IAM policy using wildcard access (`*`)
- Demonstrated risks including privilege escalation and full account compromise
- Detected via CloudTrail
- Highlighted limitations of AWS Config in identifying IAM over-permission issues
- Remediated by restoring least-privilege access

---

### 3. Open Port Exposure
- Simulated a security group misconfiguration exposing SSH (port 22) to the internet
- Demonstrated increased attack surface and risk of unauthorized access
- Detected using AWS Config (`restricted-ssh` rule) and CloudTrail
- Remediated by restricting access to a trusted IP

---

## Monitoring & Detection

The following AWS services were used for monitoring and detection:

- **CloudTrail** – Logged all management events for audit and traceability  
- **AWS Config** – Evaluated resource compliance and detected misconfigurations  
- **CloudWatch** – Provided metrics visibility for the environment  

> Note: IAM events were recorded in `us-east-1` due to IAM being a global service.

---

## Key Security Concepts Demonstrated

- Least privilege access (IAM)
- Network segmentation (public/private subnets)
- Separation of concerns (application data vs logging storage)
- Cloud misconfiguration risks
- Detection limitations in AWS-native tools
- Secure baseline → misconfiguration → detection → remediation workflow

---

---

## Evidence

Screenshots and logs are included to demonstrate:

- Baseline configuration
- Misconfigurations introduced
- Detection via AWS services
- Successful remediation

---

## Notes

Certain identifiers (e.g., account ID, IP address) have been partially redacted for security best practices.

---

## Conclusion

This project demonstrates how common AWS misconfigurations can lead to serious security risks and highlights the importance of:

- secure default configurations  
- continuous monitoring  
- proper access control  
- understanding the limitations of automated detection tools  
