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

A highly available, secure, and scalable AWS architecture where application logs generated on EC2 instances are streamed to CloudWatch, analyzed with metric filters, and trigger alerts and automated actions.

Components:

EC2 → Hosts log-generating applications

ELB → Distributes traffic across EC2

CloudWatch → Collects and monitors logs

SNS → Sends alerts

SQS → Queues log events for processing

Lambda → Serverless processing of events

S3 & Glacier → Archives logs for cost optimization

🔧 AWS Services & Responsibilities
🔹 EC2 – Application & Log Generation

Runs log-generating applications in private subnets

Generates:

Application logs

Access logs

System logs

🔹 IAM – Secure Access Control

IAM roles attached to EC2 allow:

Writing logs to CloudWatch

Uploading logs to S3

Implements least-privilege access

No hard-coded credentials

🔹 VPC – Network Security

Public Subnet: Bastion host & ELB

Private Subnets: Application EC2 instances

NAT Gateway: Outbound internet access without exposure

🔹 CloudWatch – Logging & Monitoring

Streams EC2 logs to Log Groups

Metric filters detect patterns: ERROR, FAILED LOGIN, HTTP 5xx

Automatically triggers alarms

🔹 SNS – Alerts & Notifications

Sends notifications when CloudWatch alarms trigger

Supports: Email, SMS, Slack/webhooks

🔹 SQS – Event Queue

Buffers log events from CloudWatch

Decouples ingestion from processing

Prevents data loss during traffic spikes

🔹 Lambda – Event-Driven Processing

Triggered by SQS messages

Parses logs, enriches events, triggers alerts

Fully serverless

🔹 S3 & Glacier – Log Archival

Archives logs from CloudWatch

Organizes by date, application, severity

Glacier used for long-term cost optimization

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

Distributes traffic across EC2

Prevents overload and ensures fault tolerance

🔹 Auto Scaling – Dynamic Scalability

Adjusts EC2 instances based on CPU, requests, or log volume

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
