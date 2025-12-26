# Agent 2: Test Environment Manager Agent

## Step 1: Define Role and Goal

**Agent Role:** Test Environment Lifecycle Manager

**Primary Goal:** Provision, configure, monitor, and teardown test environments on-demand while optimizing costs and ensuring environment consistency.

**Who It Helps:** QA Engineers, DevOps Teams, Test Automation Engineers, Development Teams

**Output Type:** 
- Environment provisioning status and details
- Configuration reports
- Cost analysis and optimization recommendations
- Environment health metrics

---

## Step 2: Structured Input & Output Schema

### Input Schema (JSON)
```json
{
  "action": "string (create|update|delete|clone|snapshot|restore)",
  "environment_name": "string",
  "environment_type": "string (dev|qa|staging|perf|security)",
  "infrastructure": {
    "compute": {
      "type": "string (ec2|ecs|eks|lambda)",
      "size": "string (small|medium|large|xlarge)",
      "instance_count": "integer"
    },
    "database": {
      "engine": "string (postgres|mysql|mongodb|redis)",
      "version": "string",
      "size": "string"
    },
    "network": {
      "vpc_id": "string (optional)",
      "subnet_type": "string (public|private)",
      "security_group_rules": ["array"]
    }
  },
  "configuration": {
    "application_version": "string",
    "config_files": ["array of S3 paths"],
    "environment_variables": "object",
    "seed_data": "boolean"
  },
  "scheduling": {
    "auto_shutdown": "boolean",
    "shutdown_time": "string (cron expression)",
    "auto_start": "string (cron expression)"
  },
  "tags": "object"
}
```

### Output Schema (JSON)
```json
{
  "environment_id": "uuid",
  "status": "string (provisioning|ready|updating|failed|terminated)",
  "endpoints": {
    "application_url": "string",
    "database_endpoint": "string",
    "api_endpoint": "string"
  },
  "credentials": {
    "database_secret_arn": "string",
    "api_key_secret_arn": "string"
  },
  "infrastructure_details": {
    "vpc_id": "string",
    "subnet_ids": ["array"],
    "instance_ids": ["array"],
    "load_balancer_dns": "string"
  },
  "cost_estimate": {
    "hourly_cost": "float",
    "daily_cost": "float",
    "monthly_projection": "float"
  },
  "health_status": {
    "overall": "string (healthy|degraded|unhealthy)",
    "checks": ["array of health check results"]
  },
  "provisioning_time_seconds": "integer",
  "errors": ["array"]
}
```

---

## Step 3: System Prompt for Behavior

### Core Agent Prompt
```
You are a Test Environment Manager Agent responsible for the complete lifecycle management of test environments in AWS.

Your responsibilities:
1. Provision test environments based on specified requirements
2. Configure applications and services with appropriate settings
3. Monitor environment health and performance
4. Optimize costs by implementing auto-shutdown schedules
5. Provide environment cloning and snapshot capabilities
6. Ensure environment consistency and reproducibility
7. Clean up resources to prevent cost overruns

Behavioral Guidelines:
- Always validate infrastructure requirements before provisioning
- Implement cost-saving measures (auto-shutdown, right-sizing)
- Tag all resources for proper tracking and billing
- Provide clear status updates during long-running operations
- Warn users about cost implications of large environments
- Suggest optimizations when detecting inefficiencies
- Ensure security best practices (private subnets, security groups)
- Maintain environment isolation to prevent cross-contamination

Decision-Making Process:
- Evaluate if existing environments can be reused before creating new ones
- Choose appropriate instance types based on workload requirements
- Recommend spot instances for non-critical test environments
- Suggest environment sharing when multiple teams have similar needs

Communication Style:
- Provide clear progress updates during provisioning
- Explain cost implications in simple terms
- Offer alternatives when resource limits are reached
- Give actionable recommendations for optimization
```

---

## Step 4: Reasoning and Tool Use

### Available Tools:

1. **AWS CloudFormation Client** - Infrastructure as Code deployment
2. **AWS EC2 Client** - Compute resource management
3. **AWS RDS Client** - Database provisioning
4. **AWS ECS/EKS Client** - Container orchestration
5. **AWS Secrets Manager** - Credential management
6. **AWS Cost Explorer** - Cost analysis
7. **AWS CloudWatch** - Monitoring and health checks
8. **AWS EventBridge** - Scheduling auto-shutdown/start
9. **Terraform State Manager** - Infrastructure state tracking

### Reasoning Framework: ReAct (Reasoning + Action)

```
Example thought process:

Thought: User wants to create a QA environment with PostgreSQL database
Action: Check if similar environments exist that could be cloned
Observation: Found staging environment with similar configuration

Thought: Cloning would be faster and cheaper than provisioning from scratch
Action: Propose cloning option to user
Observation: User approves cloning approach

Thought: Need to provision compute, database, and networking
Action: Validate VPC and subnet availability
Observation: VPC has sufficient IP addresses

Thought: Database size specified as 'large' which seems oversized for QA
Action: Check historical usage patterns from similar environments
Observation: Medium size sufficient for 90% of QA workloads

Thought: Should recommend cost optimization
Action: Suggest medium size with auto-scaling if needed
Observation: User accepts recommendation

Action: Begin provisioning infrastructure via CloudFormation
Observation: Stack creation in progress

Action: Monitor provisioning status
Observation: Resources created successfully

Action: Configure application settings
Observation: Configuration applied

Action: Run health checks
Observation: All checks passing

Action: Calculate cost estimate
Observation: Daily cost: $48.50

Action: Return environment details to user
```

---

## Step 5: Multi-Agent Logic (Not Required)

This agent operates independently but coordinates with:
- Synthetic Data Agent (for seeding test data)
- Test Execution Agent (to notify when environments are ready)
- Master QE Agent (for orchestration)

---

## Step 6: Memory and Context (RAG)

### Memory Requirements:

**Short-term Memory:**
- Current provisioning operations in progress
- User preferences for current session
- Temporary credentials and secrets
- Real-time cost tracking

**Long-term Memory (Vector Store):**
- Historical environment configurations
- Cost optimization patterns
- Common troubleshooting solutions
- Infrastructure templates by use case
- Performance benchmarks for different configurations
- User team preferences and patterns

**Conversation Memory:**
- Track user's environment creation history
- Remember preferred configurations
- Recall previous optimization recommendations

**Tools:** 
- LangChain Memory for conversation tracking
- Amazon OpenSearch for infrastructure templates and patterns
- DynamoDB for environment state and history
- S3 for CloudFormation templates and configuration files

---

## Step 7: Voice/Vision Capabilities

Not required for this agent.

---

## Step 8: Output Formatting

**Markdown Report Example:**
```markdown
# Environment Provisioning Report

## Environment: qa-payment-service-01

**Status:** ✅ Ready
**Provisioning Time:** 8m 23s
**Environment Type:** QA

### Access Details
- **Application URL:** https://qa-payment-01.test.example.com
- **Database Endpoint:** qa-payment-db.xxxxx.us-east-1.rds.amazonaws.com
- **API Endpoint:** https://api-qa-payment-01.test.example.com

### Infrastructure Components
- **VPC:** vpc-0a1b2c3d4e5f (test-environments-vpc)
- **Compute:** 2x t3.medium EC2 instances
- **Database:** PostgreSQL 14.7, db.t3.medium
- **Load Balancer:** alb-qa-payment-01

### Cost Estimate
- **Hourly:** $2.15
- **Daily:** $51.60
- **Monthly (projected):** $1,548.00

💡 **Cost Optimization Tip:** This environment will auto-shutdown at 7 PM EST and restart at 7 AM EST, saving approximately $720/month.

### Health Status
✅ Application: Healthy (HTTP 200)
✅ Database: Healthy (connection successful)
✅ API: Healthy (all endpoints responding)

### Credentials
Database credentials stored in AWS Secrets Manager:
- Secret ARN: arn:aws:secretsmanager:us-east-1:123456789:secret:qa-payment-db-creds

### Next Steps
1. Environment is ready for testing
2. Seed data can be loaded using the Synthetic Data Agent
3. Run smoke tests to verify functionality
```

---

## Step 9: UI Integration

**FastAPI Endpoints:**
```python
POST /api/v1/environments/create
GET /api/v1/environments/{environment_id}
PUT /api/v1/environments/{environment_id}
DELETE /api/v1/environments/{environment_id}
POST /api/v1/environments/{environment_id}/clone
POST /api/v1/environments/{environment_id}/snapshot
GET /api/v1/environments/list
GET /api/v1/environments/{environment_id}/health
GET /api/v1/environments/{environment_id}/costs
POST /api/v1/environments/{environment_id}/schedule
```

**Gradio Interface Components:**
- Environment template selector
- Infrastructure configuration form
- Real-time provisioning progress bar
- Environment list with status indicators
- Cost dashboard
- Health monitoring panel
- Schedule configuration
- Quick action buttons (start, stop, delete)

---

## Step 10: Evaluation and Monitoring

**Key Metrics:**
- Environment provisioning success rate
- Average provisioning time by environment type
- Cost savings from auto-shutdown
- Environment uptime and availability
- Resource utilization rates
- Number of active environments
- Environment creation/deletion frequency

**CloudWatch Dashboards:**
- Real-time environment status
- Cost trends and projections
- Resource utilization heatmaps
- Health check results
- Provisioning operation metrics

**Alerts:**
- Environment provisioning failures
- Cost threshold exceeded
- Health check failures
- Resource limit warnings
- Long-running environments without activity

---

## AWS Bedrock Agent Configuration (Terraform)

### Prompt for VS Code AI Assistant:

```
Create a Terraform configuration for AWS Bedrock Agent that implements a Test Environment Manager Agent with the following requirements:

1. Agent Configuration:
   - Name: test-environment-manager-agent
   - Foundation Model: anthropic.claude-3-sonnet-20240229-v1:0
   - Role: Manage complete lifecycle of test environments

2. Action Groups:
   - Name: environment-management-actions
   - Lambda Functions:
     * provision_environment: Create new test environments using CloudFormation
     * update_environment: Modify existing environment configuration
     * delete_environment: Clean up and terminate environments
     * clone_environment: Duplicate existing environment
     * get_environment_status: Retrieve current status and health
     * calculate_costs: Estimate and track environment costs
     * schedule_environment: Set up auto-start/stop schedules
     * health_check: Perform health checks on environment components
   - API Schema: OpenAPI 3.0 spec defining environment management operations

3. Knowledge Base:
   - Name: infrastructure-templates-kb
   - Data Source: S3 bucket containing:
     * CloudFormation templates for common configurations
     * Environment sizing guidelines
     * Cost optimization best practices
     * Troubleshooting guides
   - Vector Store: OpenSearch Serverless

4. Infrastructure Components:
   - Lambda Functions (Python 3.11 with boto3)
   - S3 buckets for templates and configurations
   - DynamoDB tables:
     * environment_registry: Track all environments
     * environment_history: Audit log of operations
     * cost_tracking: Historical cost data
   - EventBridge rules for scheduling
   - CloudWatch Log Groups and alarms
   - IAM roles with permissions for:
     * CloudFormation stack operations
     * EC2, RDS, ECS management
     * VPC and networking operations
     * Cost Explorer access
     * Secrets Manager access

5. Lambda Function Requirements:
   - Provision environments using CloudFormation or Terraform
   - Implement cost estimation logic
   - Set up EventBridge rules for auto-shutdown
   - Configure health checks via CloudWatch
   - Tag all resources appropriately
   - Store environment metadata in DynamoDB
   - Integrate with AWS Cost Explorer API

6. Additional Features:
   - Environment state machine for lifecycle management
   - Cost alerting when thresholds exceeded
   - Automated resource tagging
   - Environment isolation via separate VPCs/subnets
   - Snapshot and backup capabilities

Please provide:
- Complete Terraform modules structure with separate files for:
  * Bedrock agent configuration
  * Lambda functions and layers
  * DynamoDB tables
  * S3 buckets and policies
  * EventBridge rules
  * IAM roles and policies
  * CloudWatch alarms
- Lambda function code templates for each action
- OpenAPI 3.0 schema for action groups
- CloudFormation templates for common environment types
- Variable definitions and outputs
- README with deployment instructions

Use AWS best practices for:
- Cost optimization
- Security (least privilege, encryption)
- Monitoring and alerting
- Error handling and retry logic
```

---

## Implementation Checklist

- [ ] Define infrastructure templates for common environment types
- [ ] Create CloudFormation/Terraform modules
- [ ] Implement Lambda functions for all actions
- [ ] Set up DynamoDB tables for state tracking
- [ ] Configure EventBridge for scheduling
- [ ] Create cost calculation logic
- [ ] Implement health check monitors
- [ ] Set up CloudWatch dashboards
- [ ] Configure auto-shutdown/start mechanisms
- [ ] Create environment cloning logic
- [ ] Implement snapshot/restore capabilities
- [ ] Set up cost alerting
- [ ] Add resource tagging automation
- [ ] Create API documentation
- [ ] Build example environment templates
- [ ] Test provisioning different environment types
- [ ] Verify cost calculations accuracy
- [ ] Validate cleanup procedures
