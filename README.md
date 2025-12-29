AWS High-Availability Architecture: Multi-AZ Container Deployment
📌 Project Overview
This project implements a fault-tolerant, Multi-AZ (Availability Zone) web architecture on AWS. It demonstrates the migration of a monolithic application into a containerized environment using Amazon ECS (Fargate), ensuring high availability and automated scalability.

🏗️ Architecture Design
The infrastructure was designed following the AWS Well-Architected Framework, specifically focusing on the Reliability and Operational Excellence pillars.

Compute: Amazon ECS with Fargate launch type (Serverless, Multi-AZ).

Load Balancing: Application Load Balancer (ALB) distributing traffic across 3 Public Subnets.

Network: Custom VPC with Public and Private Subnets across multiple Availability Zones to prevent single points of failure.

Database: Amazon RDS (Multi-AZ) for managed, redundant data persistence.

CI/CD: Full automation using AWS CodePipeline, CodeBuild, and GitHub.

🚀 Key Engineering Features
1. Fault Tolerance & High Availability
The application is deployed across multiple AZs. If one AWS data center experiences an outage, the Application Load Balancer automatically redirects traffic to healthy containers in the remaining zones, maintaining a zero-downtime experience.

2. Automated CI/CD Pipeline
A robust "Source-to-Deploy" pipeline was established:

Commit: Changes pushed to the main branch trigger the pipeline.

Build: AWS CodeBuild creates a new Docker image and pushes it to Amazon ECR.

Deploy: ECS performs a Rolling Update, replacing old tasks with new ones only after successful Health Checks.

3. Monitoring & Observability
Integrated with Amazon CloudWatch to monitor:

CPU and Memory utilization per task.

ALB Request counts and 5XX error rates.

Alarms: Configured SNS notifications for any service disruptions.
