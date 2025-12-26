# Application

This folder contains all application code for the Test Environment Manager Agent.

## Structure

### `/api`
FastAPI endpoints for environment management:
- `POST /api/v1/environments/create` - Create new environment
- `GET /api/v1/environments/{environment_id}` - Get environment details
- `PUT /api/v1/environments/{environment_id}` - Update environment
- `DELETE /api/v1/environments/{environment_id}` - Delete environment
- `POST /api/v1/environments/{environment_id}/clone` - Clone environment
- `POST /api/v1/environments/{environment_id}/snapshot` - Create snapshot
- `GET /api/v1/environments/list` - List all environments
- `GET /api/v1/environments/{environment_id}/health` - Health check
- `GET /api/v1/environments/{environment_id}/costs` - Cost analysis
- `POST /api/v1/environments/{environment_id}/schedule` - Configure schedule

### `/lambda_functions`
AWS Lambda function implementations:
- `provision_environment` - Create new test environments using CloudFormation
- `update_environment` - Modify existing environment configuration
- `delete_environment` - Clean up and terminate environments
- `clone_environment` - Duplicate existing environment
- `get_environment_status` - Retrieve current status and health
- `calculate_costs` - Estimate and track environment costs
- `schedule_environment` - Set up auto-start/stop schedules
- `health_check` - Perform health checks on environment components

### `/ui`
Gradio interface components:
- Environment template selector
- Infrastructure configuration form
- Real-time provisioning progress bar
- Environment list with status indicators
- Cost dashboard
- Health monitoring panel
- Schedule configuration
- Quick action buttons (start, stop, delete)

### `/config`
Application configuration files and environment variables.

## Technologies

- **API Framework**: FastAPI
- **UI Framework**: Gradio
- **Runtime**: Python 3.11
- **AWS Services**: Lambda, Bedrock Agent
