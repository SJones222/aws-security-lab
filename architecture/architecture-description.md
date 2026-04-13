# Architecture Description

## Overview

This AWS environment was designed as a small, secure baseline for testing and documenting cloud security incidents. The architecture emphasizes least privilege, network segmentation, auditability, and separation of concerns.

## Design Principles

The environment was guided by the following security principles:

- **Least privilege access** through narrowly scoped IAM permissions
- **Network segmentation** through public and private subnets
- **Separation of concerns** by storing application data separately from audit logs
- **Auditability** through CloudTrail and AWS Config

## High-Level Architecture

The environment consists of:

- A **VPC** with a defined private address range
- A **public subnet** containing an EC2 instance used for controlled testing
- A **private subnet** reserved for segmented internal workloads
- An **S3 bucket** used for storage testing
- A dedicated **CloudTrail log bucket**
- An **IAM role** attached to the EC2 instance
- **AWS Config** and **CloudWatch** for monitoring support

## VPC and Subnets

A VPC was configured to isolate cloud resources and control network traffic within a defined private address range.

- **VPC CIDR:** `10.0.0.0/16`
- **Public subnet CIDR:** `10.0.1.0/24`
- **Private subnet CIDR:** `10.0.2.0/24`

The public subnet contains the EC2 instance used for security testing. The private subnet currently has no deployed resources, but it was included to demonstrate segmentation and reflect how production-oriented workloads would normally be isolated.

## Internet Connectivity

The public subnet uses a route table with:

- `0.0.0.0/0 -> Internet Gateway`
- `10.0.0.0/16 -> Local`

This allows the EC2 instance to reach the internet while preserving internal communication inside the VPC.

## EC2 Placement

The EC2 instance was intentionally placed in the public subnet to support controlled exposure scenarios such as:

- Open port testing
- Public access validation
- Observable activity for CloudTrail and AWS Config

In a production environment, sensitive workloads would typically be placed in private subnets and shielded from direct internet access.

## S3 Placement

The S3 bucket exists as a **regional AWS service** and is **not deployed inside the VPC or either subnet**. Access to S3 is controlled through IAM policies and bucket permissions rather than network placement.

This distinction is important because it separates network-level controls from service-level access controls.

## Separation of Concerns

Application/test storage and CloudTrail audit log storage were kept in separate S3 buckets. This reduces risk, improves control clarity, and prevents a storage misconfiguration affecting one bucket from also exposing audit evidence stored in another.

## Monitoring and Audit Support

The environment was instrumented with:

- **CloudTrail** for management event logging
- **AWS Config** for resource recording and compliance checks
- **CloudWatch** for metrics visibility

These services support detection, investigation, and documentation of the misconfiguration scenarios included in the project.
