# Application Configuration

This directory contains configuration files and environment variable templates for the Test Environment Manager Agent application.

## Files

- `config.yaml` - Main application configuration
- `.env.example` - Environment variable template
- `environments/` - Environment-specific configurations (dev, staging, prod)

## Configuration Categories

### AWS Configuration
- Region settings
- Bedrock Agent configuration
- Service endpoints
- Credential profiles

### Application Settings
- API server configuration
- UI server settings
- Logging levels
- Feature flags

### Database Configuration
- DynamoDB table names
- OpenSearch endpoint
- Connection settings

### Cost Management
- Cost thresholds
- Alert configurations
- Optimization rules

### Monitoring
- CloudWatch settings
- Health check intervals
- Metrics collection

## Usage

1. Copy `.env.example` to `.env`
2. Update configuration values for your environment
3. Never commit `.env` files to version control
