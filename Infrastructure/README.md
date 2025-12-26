# Infrastructure

This folder contains Infrastructure as Code (IaC) configurations for deploying the Test Environment Manager Agent.

## Structure

### `/terraform`
Terraform configurations for:
- AWS Bedrock Agent setup
- Lambda functions and layers
- DynamoDB tables (environment_registry, environment_history, cost_tracking)
- S3 buckets for templates and configurations
- EventBridge rules for scheduling
- CloudWatch Log Groups and alarms
- IAM roles and policies
- OpenSearch Serverless for knowledge base

### `/cloudformation`
CloudFormation templates for:
- Common environment types (dev, qa, staging, perf, security)
- VPC and networking configurations
- Compute resources (EC2, ECS, EKS)
- Database resources (RDS, DynamoDB, Redis)
- Load balancers and auto-scaling groups

### `/docs`
Infrastructure documentation:
- Deployment guides
- Architecture diagrams
- Security best practices
- Cost optimization strategies
- Troubleshooting guides

## AWS Resources

### Bedrock Agent Configuration
- Foundation Model: anthropic.claude-3-sonnet-20240229-v1:0
- Action Groups: environment-management-actions
- Knowledge Base: infrastructure-templates-kb

### Core Infrastructure
- Lambda Functions (Python 3.11 with boto3)
- DynamoDB tables for state tracking and history
- S3 buckets for templates and configurations
- EventBridge rules for auto-shutdown/start scheduling
- CloudWatch monitoring and alerting
- OpenSearch Serverless for vector store

## Deployment

Refer to individual README files in subdirectories for specific deployment instructions.
