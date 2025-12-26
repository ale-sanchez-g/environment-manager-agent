# Environment Manager Agent

**Primary Goal:** Provision, configure, monitor, and teardown test environments on-demand while optimizing costs and ensuring environment consistency.

## Overview

The Test Environment Manager Agent is an AWS Bedrock-powered AI agent that manages the complete lifecycle of test environments. It handles provisioning, configuration, monitoring, cost optimization, and cleanup of cloud-based test environments.

**Who It Helps:** QA Engineers, DevOps Teams, Test Automation Engineers, Development Teams

## Project Structure

### 📋 Aidlc-plan/
AI Development Lifecycle planning documents and agent specifications.
- Complete agent design and requirements
- Input/Output schemas
- System prompts and behavior guidelines
- Tool integration specifications
- Implementation checklist

[View Details](Aidlc-plan/README.md)

### 💻 Application/
Application code including APIs, Lambda functions, and UI components.

- **api/** - FastAPI endpoints for environment management
- **lambda_functions/** - AWS Lambda functions for Bedrock Agent actions
- **ui/** - Gradio interface for user interactions
- **config/** - Application configuration files

[View Details](Application/README.md)

### 🏗️ Infrastructure/
Infrastructure as Code configurations for AWS deployment.

- **terraform/** - Terraform modules for Bedrock Agent and AWS resources
- **cloudformation/** - CloudFormation templates for test environments
- **docs/** - Infrastructure documentation and guides

[View Details](Infrastructure/README.md)

## Key Features

- **Environment Provisioning** - Create test environments from templates
- **Cost Optimization** - Auto-shutdown scheduling and right-sizing recommendations
- **Health Monitoring** - Continuous health checks and status reporting
- **Environment Cloning** - Duplicate existing environments quickly
- **Cost Analysis** - Real-time cost tracking and projections
- **Automated Cleanup** - Scheduled teardown to prevent cost overruns

## Technologies

- **AI/ML**: AWS Bedrock (Claude 3 Sonnet)
- **API**: FastAPI (Python)
- **UI**: Gradio
- **Infrastructure**: Terraform, CloudFormation
- **Cloud**: AWS (Lambda, DynamoDB, EventBridge, CloudWatch, OpenSearch)

## Getting Started

1. Review the [agent specification](Aidlc-plan/environment-agent.md)
2. Deploy infrastructure using [Terraform modules](Infrastructure/terraform/)
3. Configure and deploy [Lambda functions](Application/lambda_functions/)
4. Set up the [API server](Application/api/) and [UI](Application/ui/)

## Documentation

- [Infrastructure Documentation](Infrastructure/docs/README.md)
- [Deployment Guide](Infrastructure/terraform/README.md)
- [Agent Specification](Aidlc-plan/environment-agent.md)

## License

See [LICENSE](LICENSE) file for details.
