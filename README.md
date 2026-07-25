# Automation Workflow Builder





An intelligent workflow orchestration system that leverages AI to generate dynamic configuration files for DevOps automation.




## Overview
This project is a no-code automation workflow built with **n8n** that integrates with **Google Gemini AI** to generate infrastructure configuration files on demand. It automates the creation of:


- **YAML Configuration** (spec.yaml) - Kubernetes-ready YAML with kebab-case formatting
- **EJS Templates** (template.ejs) - Templated HTML/configuration files
- **Python Pickle Files** - Serialized Python dictionary configurations
- **Git Branch Names** - Automated branch naming for DevOps workflows
## Workflow Architecture
### Components

1. **Webhook Trigger** (`/generate-config`)
   - Entry point for configuration generation requests
   - Accepts POST requests with input parameters


2. **Prompt Builder**
   - Creates an optimized prompt for the AI model
   - Instructs Gemini AI to generate YAML, EJS, and Python configs

3. **Gemini API Integration**
   - Calls Google's Gemini API to generate configurations
   - Returns structured JSON with all required outputs

4. **Python Processing Engine**
   - Processes Gemini's response
   - Handles Markdown cleanup and JSON parsing
   - Serializes Python dictionaries to base64-encoded pickle files


## API Endpoint

### Generate Configuration

**Endpoint:** `POST /generate-config`

**Request Body:**
```json
{
  "requested_type": "kubernetes",
  "environment": "production",
  "service_name": "my-service"
}
```

**Response:**
```json
{
  "json": {
    "branch": "feat/ops-config-...",
    "yaml": "apiVersion: v1\nkind: ConfigMap\n...",
    "ejs": "<h1>Order for <%= client_id %></h1>"
  },
  "binary": {
    "pkl_file": {
      "data": "base64_encoded_pickle_data",
      "mimeType": "application/octet-stream",
      "fileName": "vendor_config.pkl"
    }
  }
}
```

## Configuration Files

### WorkflowConfig.json
Contains the complete n8n workflow definition with all nodes and connections for the automation pipeline.

## Key Features

✅ **AI-Powered Generation** - Uses Gemini AI for intelligent configuration creation  
✅ **Multi-Format Output** - Generates YAML, EJS, and Python configs in one request  
✅ **Automated Serialization** - Handles pickle file encoding automatically  
✅ **DevOps Ready** - Produces Kubernetes-compatible configurations  
✅ **No-Code Workflow** - Built entirely in n8n, no coding required  

## Setup & Deployment

1. Import `WorkflowConfig.json` into your n8n instance
2. Configure Gemini API credentials
3. Deploy and trigger via webhook endpoint
4. Receive generated configs in structured JSON format

## Technology Stack

- **n8n** - Workflow automation platform
- **Google Gemini API** - AI-powered configuration generation
- **Python** - Pickle serialization and data processing
- **JSON/YAML/EJS** - Configuration formats

## Use Cases

- Automated infrastructure setup
- Dynamic configuration generation
- Multi-environment deployment management
- Infrastructure-as-Code (IaC) automation
- CI/CD pipeline orchestration

## License

MIT
