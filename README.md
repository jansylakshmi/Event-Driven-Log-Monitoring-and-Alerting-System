📊 Project 2: Event-Driven Log Monitoring & Alerting System
🎯 Project Goal

Design and implement an event-driven monitoring system that collects application logs, detects critical events in real time, sends alerts automatically, and scales dynamically during traffic spikes—while keeping costs optimized.

🏗️ High-Level Architecture Overview

This project uses a highly available, secure, and scalable AWS architecture where application logs generated on EC2 instances are streamed to CloudWatch, analyzed for patterns, and trigger alerts and automated actions.

🔧 AWS Services & Their Roles
1️⃣ EC2 – Application & Log Generation

EC2 instances host applications that continuously generate logs.

Instances run in private subnets for security.

Logs include application errors, access logs, and system logs.

2️⃣ IAM – Secure Access Control

IAM roles attached to EC2 allow:

Writing logs to CloudWatch Logs

Uploading archived logs to S3

No hard-coded credentials (follows least privilege principle).

3️⃣ VPC – Secure Network Design

Public Subnet

Bastion host for secure SSH access

Load Balancer (ELB)

Private Subnets

Application EC2 instances

NAT Gateway enables outbound internet access without exposing EC2.

4️⃣ CloudWatch – Log Streaming & Monitoring

EC2 streams logs to CloudWatch Log Groups.

Metric Filters detect patterns such as:

ERROR

FAILED LOGIN

HTTP 5xx

Metrics trigger alarms automatically.

5️⃣ SNS – Real-Time Alerts

CloudWatch alarms publish notifications to SNS topics.

Alerts are sent via:

Email

SMS

Slack / third-party tools (via webhook)

6️⃣ SQS – Reliable Log Processing

CloudWatch events push messages to SQS queues.

Decouples log ingestion from processing.

Prevents data loss during traffic spikes.

7️⃣ AWS Lambda – Event-Driven Processing

Lambda functions process messages from SQS:

Parse logs

Enrich events

Trigger alerts or remediation steps

Serverless → no infrastructure management.

8️⃣ S3 – Log Archival Storage

Logs are archived from CloudWatch to S3 buckets.

Organized by:

Date

Application

Severity level

9️⃣ CloudTrail – Audit & Compliance

Tracks all API activity related to:

IAM changes

EC2 lifecycle actions

S3 access

Enables security auditing and compliance.

🔐 1️⃣0️⃣ Secrets Manager – Secure Credential Storage

Stores API keys and tokens for:

Slack

PagerDuty

External monitoring tools

Secrets are rotated automatically.

⚙️ 1️⃣1️⃣ Systems Manager – Automation & Maintenance

Used to:

Patch EC2 instances

Clean old log files

Run maintenance scripts

No SSH required (Session Manager).

⚖️ 1️⃣2️⃣ ELB – Load Distribution

Elastic Load Balancer distributes incoming traffic across EC2.

Prevents log overload on a single instance.

Improves fault tolerance.

📈 1️⃣3️⃣ Auto Scaling – Dynamic Scalability

EC2 instances scale automatically based on:

CPU usage

Log volume

Request count

Ensures performance during high-traffic events.

💰 1️⃣4️⃣ Cost Optimization Strategy

Old logs are transitioned:

S3 → S3 Glacier

Reduces long-term storage cost.

Lifecycle policies automate archival.

🔄 End-to-End Flow

Users send requests → ELB

EC2 processes requests → generates logs

Logs stream to CloudWatch

Metric filters detect errors

Alerts sent via SNS

Logs queued in SQS

Lambda processes log events

Logs archived to S3 → Glacier

Auto Scaling adjusts EC2 capacity

⭐ Key Benefits

Real-time alerting

Event-driven & serverless

Highly scalable

Secure & compliant

Cost-optimized
