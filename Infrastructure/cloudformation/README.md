# CloudFormation Templates

This directory contains CloudFormation templates for provisioning various test environment types.

## Template Categories

### Environment Types
- `dev-environment.yaml` - Development environment template
- `qa-environment.yaml` - QA testing environment template
- `staging-environment.yaml` - Staging environment template
- `performance-environment.yaml` - Performance testing environment template
- `security-environment.yaml` - Security testing environment template

### Infrastructure Components

#### Compute Templates
- `compute/ec2-autoscaling.yaml` - EC2 with auto-scaling groups
- `compute/ecs-cluster.yaml` - ECS cluster configuration
- `compute/eks-cluster.yaml` - EKS cluster configuration
- `compute/lambda-app.yaml` - Serverless Lambda application

#### Database Templates
- `database/postgresql-rds.yaml` - PostgreSQL RDS instance
- `database/mysql-rds.yaml` - MySQL RDS instance
- `database/mongodb-documentdb.yaml` - DocumentDB cluster
- `database/redis-elasticache.yaml` - ElastiCache Redis cluster

#### Network Templates
- `network/vpc-with-subnets.yaml` - VPC with public/private subnets
- `network/security-groups.yaml` - Security group configurations
- `network/load-balancer.yaml` - Application Load Balancer

## Structure

```
cloudformation/
├── environments/
│   ├── dev-environment.yaml
│   ├── qa-environment.yaml
│   ├── staging-environment.yaml
│   ├── performance-environment.yaml
│   └── security-environment.yaml
├── components/
│   ├── compute/
│   │   ├── ec2-autoscaling.yaml
│   │   ├── ecs-cluster.yaml
│   │   ├── eks-cluster.yaml
│   │   └── lambda-app.yaml
│   ├── database/
│   │   ├── postgresql-rds.yaml
│   │   ├── mysql-rds.yaml
│   │   ├── mongodb-documentdb.yaml
│   │   └── redis-elasticache.yaml
│   └── network/
│       ├── vpc-with-subnets.yaml
│       ├── security-groups.yaml
│       └── load-balancer.yaml
├── nested/                      # Nested stack templates
└── parameters/                  # Parameter files
    ├── dev-params.json
    ├── qa-params.json
    └── staging-params.json
```

## Features

- **Parameterized Templates** - Flexible configuration options
- **Nested Stacks** - Modular, reusable components
- **Resource Tags** - Automatic tagging for cost tracking
- **Security Best Practices** - Private subnets, security groups
- **Cost Optimization** - Right-sized instances, auto-scaling

## Usage

### Deploy a Complete Environment

```bash
aws cloudformation create-stack \
  --stack-name my-qa-environment \
  --template-body file://environments/qa-environment.yaml \
  --parameters file://parameters/qa-params.json \
  --capabilities CAPABILITY_IAM
```

### Deploy Individual Components

```bash
aws cloudformation create-stack \
  --stack-name my-database \
  --template-body file://components/database/postgresql-rds.yaml \
  --parameters ParameterKey=DBInstanceClass,ParameterValue=db.t3.medium
```

## Template Standards

- All templates include comprehensive parameter validation
- Outputs include essential endpoint and resource information
- Resources are tagged with environment, cost-center, and project
- Templates follow AWS Well-Architected Framework principles
