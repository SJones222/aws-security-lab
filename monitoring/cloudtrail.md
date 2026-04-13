# CloudTrail

## Purpose

CloudTrail was enabled to provide management event logging for the environment. It supports auditability by recording who made changes, what actions were taken, and when those actions occurred.

## Configuration

- **Trail name:** `aws-sec-lab-trail`
- **Event category:** Management events
- **Storage location:** Dedicated S3 log bucket
- **Log separation:** Audit logs stored separately from application/test data

This separation of concerns helps protect audit evidence from accidental exposure during testing scenarios.

## Baseline Evidence

![CloudTrail baseline](../evidence/screenshots/baseline/cloudtrail.png)

## Use in Security Tests

CloudTrail was used to capture change events associated with all three scenarios in this project:

- **S3 Public Exposure** - policy change activity
- **IAM Over-Permission** - policy attachment activity
- **Open Port Exposure** - security group ingress rule changes

## Important IAM Logging Note

IAM is a global service, so identity-related events were recorded in `us-east-1` rather than the primary deployment region. This highlights the importance of reviewing CloudTrail logs across regions when investigating identity-based activity.
