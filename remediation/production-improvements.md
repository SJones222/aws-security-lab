# Production Improvements

This project focused on building a secure baseline and then introducing controlled misconfigurations to simulate real-world cloud security incidents. If this environment were extended toward production, the following improvements would be recommended.

## S3 Public Exposure Controls

- Enforce S3 Block Public Access at the account level
- Implement automated alerts for bucket policy changes
- Use service control policies (SCPs) to restrict unsafe storage configurations
- Perform regular compliance reviews using AWS Config rules

## IAM Hardening

- Enforce least-privilege policies through design and review
- Use IAM Access Analyzer to identify risky access paths
- Implement permission boundaries where appropriate
- Periodically review all roles for unnecessary permissions

## Network Security Hardening

- Enforce restricted SSH access policies
- Use bastion hosts or more controlled access methods instead of broad direct access
- Implement automated alerts for security group changes
- Conduct regular network configuration audits

## Monitoring Improvements

- Expand CloudWatch from basic metrics visibility into alerting where useful
- Strengthen review procedures for CloudTrail activity across regions
- Consider enabling additional managed detection services, such as GuardDuty, where account capabilities permit

## Governance Improvements

- Establish recurring review of compliance findings
- Validate that audit logs remain isolated from application data
- Continue documenting baseline state before testing or operational changes
