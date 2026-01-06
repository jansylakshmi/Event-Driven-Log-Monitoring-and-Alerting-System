📊 Event-Driven Log Monitoring & Alerting System

AWS | Cloud | DevOps Project

🎯 Project Objective

Designed and implemented an event-driven monitoring system that collects application logs, detects critical events in real time, sends automated alerts, and scales dynamically during traffic spikes—while ensuring security and cost optimization.

🏗️ Architecture Summary

A highly available, secure, and scalable AWS architecture where logs generated on EC2 instances are streamed to CloudWatch, analyzed using metric filters, and trigger alerts, serverless processing, and automated scaling actions.

🧩 AWS Services & Responsibilities
🔹 EC2 – Application & Log Generation

Hosts log-generating applications

Deployed in private subnets for security

Generates:

Application logs

Access logs

System logs

🔹 IAM – Identity & Access Management

IAM roles attached to EC2 allow:

Writing logs to CloudWatch Logs

Uploading archived logs to S3

Implements least-privilege access

No hard-coded credentials

🔹 VPC – Secure Network Architecture

Public Subnet

Bastion Host (secure SSH access)

Application Load Balancer (ELB)

Private Subnets

Application EC2 instances

NAT Gateway

Enables outbound internet access for private EC2 without exposure

🔹 CloudWatch – Logging & Monitoring

Streams logs from EC2 into Log Groups

Metric Filters detect patterns such as:

ERROR

FAILED LOGIN

HTTP 5xx

Triggers alarms automatically

🔹 SNS – Alerting & Notifications

CloudWatch alarms publish messages to SNS topics

Notifications sent via:

Email

SMS

Slack / third-party tools (webhooks)

🔹 SQS – Log Event Queue

Buffers log events from CloudWatch

Decouples log ingestion from processing

Prevents message loss during traffic spikes

🔹 AWS Lambda – Event-Driven Processing

Triggered by messages from SQS

Performs:

Log parsing

Event enrichment

Alerting or remediation actions

Fully serverless (no infrastructure management)

🔹 S3 – Log Archival Storage

Archives logs from CloudWatch

Logs organized by:

Date

Application

Severity level

🔹 CloudTrail – Auditing & Compliance

Tracks all API activity related to:

IAM changes

EC2 lifecycle events

S3 access

Supports security audits and compliance requirements

🔹 Secrets Manager – Secure Secrets Storage

Stores sensitive data such as:

Slack tokens

PagerDuty keys

External API credentials

Automatic secret rotation enabled

🔹 Systems Manager – Automation & Maintenance

Used for:

EC2 patch management

Log cleanup

Running maintenance scripts

Access without SSH (Session Manager)

🔹 ELB – Load Balancing

Distributes incoming traffic across EC2 instances

Prevents log overload on a single server

Improves availability and fault tolerance

🔹 Auto Scaling – Dynamic Scalability

Automatically scales EC2 based on:

CPU utilization

Log volume

Request count

Maintains performance during peak traffic

🔹 Cost Optimization Strategy

Older logs transitioned automatically:

S3 → S3 Glacier

Lifecycle policies reduce long-term storage cost

🔄 End-to-End Workflow

User requests reach ELB

ELB forwards traffic to EC2 instances

Applications generate logs

Logs stream to CloudWatch

Metric filters detect critical patterns

Alerts sent via SNS

Log events queued in SQS

Lambda processes log events

Logs archived to S3 → Glacier

Auto Scaling adjusts EC2 capacity
