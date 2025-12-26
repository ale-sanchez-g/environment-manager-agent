# Terraform Modules

This directory contains Terraform configurations for deploying the AWS Bedrock Agent and supporting infrastructure.

## Structure

```
terraform/
├── main.tf                      # Main Terraform configuration
├── variables.tf                 # Input variables
├── outputs.tf                   # Output values
├── providers.tf                 # Provider configuration
├── modules/
│   ├── bedrock_agent/          # Bedrock Agent configuration
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── lambda_functions/       # Lambda function deployment
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── dynamodb_tables/        # DynamoDB tables
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── s3_buckets/             # S3 buckets for templates
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── eventbridge/            # EventBridge rules
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── iam/                    # IAM roles and policies
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── opensearch/             # OpenSearch Serverless
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── cloudwatch/             # CloudWatch alarms
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── environments/
│   ├── dev.tfvars
│   ├── staging.tfvars
│   └── prod.tfvars
└── README.md
```

## Key Resources

### Bedrock Agent
- Agent Name: test-environment-manager-agent
- Foundation Model: anthropic.claude-3-sonnet-20240229-v1:0
- Action Groups: environment-management-actions
- Knowledge Base: infrastructure-templates-kb

### DynamoDB Tables
- `environment_registry` - Track all environments
- `environment_history` - Audit log of operations
- `cost_tracking` - Historical cost data

### Lambda Functions
- All 8 action group functions
- Python 3.11 runtime
- boto3 integration

### IAM Roles
- Bedrock Agent execution role
- Lambda execution roles
- EventBridge service role

## Deployment

```bash
# Initialize Terraform
terraform init

# Plan deployment
terraform plan -var-file="environments/dev.tfvars"

# Apply configuration
terraform apply -var-file="environments/dev.tfvars"
```

## Best Practices

- Use workspaces for environment separation
- Store state in S3 with DynamoDB locking
- Enable versioning on S3 buckets
- Tag all resources appropriately
- Implement cost allocation tags
