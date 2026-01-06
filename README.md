📊 Project: Event-Driven Log Monitoring & Alerting System

AWS | Cloud | DevOps Project

🎯 Project Goal

Design and implement an event-driven monitoring system that:

Collects application logs in real time

Detects critical events automatically

Sends alerts via email, SMS, or Slack

Scales EC2 instances dynamically during traffic spikes

Optimizes storage costs by archiving old logs

🏗️ Architecture Overview

A highly available, secure, and scalable AWS architecture where logs generated on EC2 instances are streamed to CloudWatch, analyzed with metric filters, and trigger alerts and automated actions.

Architecture Components:

EC2 → Log-generating application servers

ELB → Distributes traffic across EC2

CloudWatch → Collects and monitors logs

SNS → Sends alerts

SQS → Queues log events

Lambda → Processes events serverlessly

S3 & Glacier → Archives logs for cost optimization

🔧 AWS Services & Responsibilities
🔹 EC2 – Application & Log Generation

Runs log-generating applications

Deployed in private subnets

Logs include application errors, access logs, and system logs

🔹 IAM – Secure Access Control

Roles attached to EC2 allow:

Writing logs to CloudWatch

Uploading logs to S3

Least privilege policy; no hard-coded credentials

🔹 VPC – Network Security

Public Subnet: Bastion host & ELB

Private Subnets: Application EC2 instances

NAT Gateway: Outbound internet access without exposure

🔹 CloudWatch – Logging & Monitoring

Streams EC2 logs to Log Groups

Metric filters detect patterns like: ERROR, FAILED LOGIN, HTTP 5xx

Triggers alarms automatically

🔹 SNS – Alerting

CloudWatch alarms publish messages to SNS topics

Notifications via: Email, SMS, Slack / Webhooks

🔹 SQS – Log Event Queue

Buffers log events from CloudWatch

Decouples ingestion from processing

Prevents data loss during spikes

🔹 Lambda – Event-Driven Processing

Triggered by SQS messages

Performs log parsing, enrichment, and automated alerting

Fully serverless, no infrastructure management

🔹 S3 – Log Archival

Archives logs from CloudWatch

Organized by date, application, and severity

🔹 CloudTrail – Auditing

Tracks API activity for: IAM, EC2, S3

Enables security auditing and compliance

🔹 Secrets Manager – Credential Storage

Stores API keys and tokens (Slack, PagerDuty, etc.)

Automatic secret rotation

🔹 Systems Manager – Automation

Automates EC2 patching and log cleanup

Runs scripts without SSH access

🔹 ELB – Load Balancing

Distributes traffic across EC2 instances

Prevents overload and improves fault tolerance

🔹 Auto Scaling – Dynamic Scalability

Adjusts EC2 instance count based on CPU, request volume, or log load

🔹 Cost Optimization

Old logs moved from S3 → Glacier automatically

Reduces long-term storage cost using lifecycle policies

🔄 End-to-End Workflow

User request → ELB

ELB forwards request → EC2

EC2 generates logs

Logs → CloudWatch

Metric filters detect errors

Alerts sent via SNS

Logs queued in SQS

Lambda processes log events

Logs archived → S3 → Glacier

Auto Scaling adjusts EC2 capacity
