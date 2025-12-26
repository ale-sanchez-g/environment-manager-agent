# Lambda Functions

This directory contains AWS Lambda function implementations for the environment management actions.

## Functions

### Core Functions
- **provision_environment** - Create new test environments using CloudFormation/Terraform
- **update_environment** - Modify existing environment configuration
- **delete_environment** - Clean up and terminate environments
- **clone_environment** - Duplicate existing environment with snapshot
- **get_environment_status** - Retrieve current status and health metrics
- **calculate_costs** - Estimate and track environment costs using Cost Explorer
- **schedule_environment** - Set up auto-start/stop schedules with EventBridge
- **health_check** - Perform health checks on environment components

## Structure

```
lambda_functions/
├── provision_environment/
│   ├── handler.py
│   └── requirements.txt
├── update_environment/
│   ├── handler.py
│   └── requirements.txt
├── delete_environment/
│   ├── handler.py
│   └── requirements.txt
├── clone_environment/
│   ├── handler.py
│   └── requirements.txt
├── get_environment_status/
│   ├── handler.py
│   └── requirements.txt
├── calculate_costs/
│   ├── handler.py
│   └── requirements.txt
├── schedule_environment/
│   ├── handler.py
│   └── requirements.txt
├── health_check/
│   ├── handler.py
│   └── requirements.txt
├── shared/              # Shared utilities and helpers
│   ├── aws_clients.py
│   ├── dynamodb_helper.py
│   ├── cost_calculator.py
│   └── validators.py
└── layers/              # Lambda layers for common dependencies
    └── boto3_layer/
```

## Runtime

- Python 3.11
- AWS SDK (boto3)
- AWS Bedrock Agent integration

## Permissions Required

- CloudFormation stack operations
- EC2, RDS, ECS management
- VPC and networking operations
- Cost Explorer access
- Secrets Manager access
- DynamoDB read/write
- EventBridge rule management
