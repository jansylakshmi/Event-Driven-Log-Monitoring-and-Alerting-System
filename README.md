<div align="center">
🏆 EVENT-DRIVEN LOG MONITORING & ALERTING SYSTEM

AWS | Cloud | DevOps Project

</div>
🎯 Project Goal

Design and implement an event-driven monitoring system that:

Collects application logs in real time

Detects critical events automatically

Sends alerts via Email, SMS, or Slack

Dynamically scales EC2 instances during traffic spikes

Optimizes storage costs by archiving old logs

🏗️ Architecture Overview

A highly available, secure, and scalable AWS architecture where EC2 logs are streamed to CloudWatch, analyzed with metric filters, and trigger alerts and automated actions.

Components:

EC2 → Log-generating application servers

ELB → Distributes traffic across EC2

CloudWatch → Collects and monitors logs

SNS → Sends alerts

SQS → Queues log events

Lambda → Processes events serverlessly

S3 & Glacier → Archives logs for cost optimization

🔧 AWS Services & Responsibilities
🔹 EC2 – Application & Log Generation

Runs log-generating applications in private subnets

Generates application, access, and system logs

🔹 IAM – Secure Access Control

Allows EC2 to:

Write logs to CloudWatch

Upload logs to S3

Implements least-privilege access, no hard-coded credentials

🔹 VPC – Network Security

Public Subnet: Bastion host & ELB

Private Subnets: EC2 application servers

NAT Gateway: Outbound internet access for private EC2

🔹 CloudWatch – Logging & Monitoring

Streams logs from EC2 to Log Groups

Metric filters detect patterns: ERROR, FAILED LOGIN, HTTP 5xx

Triggers alarms automatically

🔹 SNS – Alerts & Notifications

Sends notifications for CloudWatch alarms

Supports Email, SMS, Slack/webhooks

🔹 SQS – Event Queue

Buffers log events

Decouples ingestion from processing

Prevents data loss during spikes

🔹 Lambda – Event-Driven Processing

Processes messages from SQS

Parses logs, enriches events, triggers alerts

Fully serverless

🔹 S3 & Glacier – Log Archival

Archives logs organized by date, application, severity

Glacier used for long-term storage cost optimization

🔹 CloudTrail – Auditing

Tracks API activity: IAM, EC2, S3

Enables security compliance

🔹 Secrets Manager – Credential Storage

Stores API keys (Slack, PagerDuty, external integrations)

Automatic rotation enabled

🔹 Systems Manager – Automation

Automates EC2 patching and log cleanup

Executes scripts without SSH

🔹 ELB – Load Balancing

Distributes traffic evenly across EC2 instances

Prevents overload and ensures high availability

🔹 Auto Scaling – Dynamic Scalability

Adjusts EC2 instance count based on CPU, requests, or log volume

🔄 End-to-End Workflow

User request → ELB

ELB forwards request → EC2

EC2 generates logs

Logs → CloudWatch

Metric filters detect critical patterns

Alerts sent via SNS

Logs queued in SQS

Lambda processes log events

Logs archived → S3 → Glacier

Auto Scaling adjusts EC2 capacity
