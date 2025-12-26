# User Interface

This directory contains the Gradio interface components for the Test Environment Manager Agent.

## Components

- **Environment Template Selector** - Choose from predefined environment templates
- **Infrastructure Configuration Form** - Configure compute, database, and network settings
- **Real-time Provisioning Progress Bar** - Track environment creation progress
- **Environment List** - View all environments with status indicators
- **Cost Dashboard** - Monitor costs and projections
- **Health Monitoring Panel** - Real-time health metrics and alerts
- **Schedule Configuration** - Set up auto-shutdown/start times
- **Quick Action Buttons** - Start, stop, delete, clone environments

## Structure

```
ui/
├── app.py                    # Main Gradio application
├── components/               # Individual UI components
│   ├── environment_form.py   # Environment creation form
│   ├── environment_list.py   # Environment listing and management
│   ├── cost_dashboard.py     # Cost analysis visualization
│   ├── health_panel.py       # Health monitoring display
│   └── schedule_config.py    # Scheduling interface
├── utils/                    # Helper functions
│   ├── api_client.py         # Backend API integration
│   └── formatters.py         # Data formatting utilities
├── static/                   # Static assets (CSS, images)
└── requirements.txt          # Python dependencies
```

## Technologies

- **Framework**: Gradio
- **Visualization**: Plotly (for cost charts)
- **API Integration**: HTTP client for backend communication

## Usage

```bash
pip install -r requirements.txt
python app.py
```

Access the interface at `http://localhost:7860`
