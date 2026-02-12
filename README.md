# TechConnect FY26 Hackfest

A comprehensive AI Agent Testing & Evaluation Framework for Microsoft Azure AI, designed for automated agent deployment, execution, and safety evaluation.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [📚 Documentation](#-documentation)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [CI/CD with GitHub Actions](#cicd-with-github-actions)
- [Project Structure](#project-structure)
- [Modules Description](#modules-description)

## Overview

This framework provides a complete solution for testing and evaluating Azure AI agents with built-in support for:
- Agent execution and consumption
- Automated evaluation using Azure AI Evaluation
- Batch evaluation capabilities
- Red team testing for security and safety vulnerabilities

## Features

- 🤖 **Agent Execution**: Execute and consume existing Azure AI agents
- 📊 **Automated Evaluation**: Evaluate agent responses using OpenAI evaluation metrics
- 🔄 **Batch Processing**: Run evaluations on multiple data points efficiently
- 🛡️ **Red Team Testing**: Identify potential security and safety vulnerabilities using PyRIT
- ☁️ **Azure Integration**: Seamless integration with Azure AI Projects and Azure OpenAI
- 🔧 **CI/CD Ready**: GitHub Actions workflow for automated testing

## 📚 Documentation

Comprehensive guides and architecture documentation are available in the `docs/` directory:

### Getting Started
- **[RFP Agent Architecture](./docs/RFP-AGENT-ARCHITECTURE.md)** - Complete architecture overview with Mermaid diagrams including:
  - Business flow diagrams
  - Technical architecture
  - Data flow and agent interaction models
  - Security architecture
  - Scalability and performance considerations

### Development Guides
- **[Creating an RFP Agent](./docs/CREATING-RFP-AGENT.md)** - Step-by-step guide for building an RFP agent:
  - Azure environment setup
  - Document preparation and indexing
  - Agent creation and configuration
  - Testing and optimization
  - Best practices and troubleshooting

### Deployment
- **[CI/CD Deployment Guide](./docs/CICD-DEPLOYMENT-GUIDE.md)** - End-to-end CI/CD setup for agentic AI applications:
  - Multi-environment deployment (Dev/Staging/Production)
  - GitHub Actions workflows
  - Automated testing and evaluation
  - Security scanning with PyRIT
  - Blue-green and canary deployment strategies
  - Monitoring and observability setup

### Quick Links
```
docs/
├── RFP-AGENT-ARCHITECTURE.md      # Architecture & diagrams
├── CREATING-RFP-AGENT.md          # Agent development guide
└── CICD-DEPLOYMENT-GUIDE.md       # CI/CD setup & deployment
```

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.12** or higher
- **pip** (Python package manager)
- **Azure Account** with the following services set up:
  - Azure AI Projects
  - Azure OpenAI Service
  - Azure AI Search (optional, for search capabilities)
- **Git** for version control

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/balakreshnan/TechconnectFY26Hackfest.git
cd TechconnectFY26Hackfest
```

> **Note**: The repository URL uses 'TechconnectFY26Hackfest' (without spaces) for compatibility with URL standards.

### 2. Create a Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

The `requirements.txt` includes all necessary packages:
- Azure AI Framework components
- OpenAI client libraries
- PyRIT for red team testing
- Azure AI Evaluation
- Streamlit for UI components
- And other supporting libraries

## Configuration

### Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# Azure AI Project Configuration
AZURE_AI_PROJECT=your-project-name
AZURE_AI_PROJECT_ENDPOINT=https://your-endpoint.azure.com
AZURE_RESOURCE_GROUP=your-resource-group

# Azure OpenAI Configuration
AZURE_OPENAI_KEY=your-openai-key
AZURE_OPENAI_ENDPOINT=https://your-openai-endpoint.azure.com
AZURE_OPENAI_DEPLOYMENT=your-deployment-name
AZURE_OPENAI_CHAT_DEPLOYMENT_NAME=your-chat-deployment
AZURE_OPENAI_API_VERSION=2024-02-15-preview
AZURE_OPENAI_RESPONSES_DEPLOYMENT_NAME=your-responses-deployment

# Azure AI Model Configuration
AZURE_AI_MODEL_DEPLOYMENT_NAME=your-model-deployment

# Azure AI Search (Optional)
AZURE_AI_SEARCH_INDEX_NAME=your-search-index

# Agent Configuration
AGENT_NAME=your-agent-name
```

### Azure Credentials

Ensure you have the necessary Azure credentials configured for authentication:

```bash
az login
```

## Usage

### Running Individual Modules

#### 1. Agent Execution

Execute an existing Azure AI agent:

```bash
python exagent.py \
  --resource-group "your-resource-group" \
  --project "your-project-name" \
  --agent-name "your-agent-name"
```

#### 2. Agent Evaluation

Run evaluation on agent responses:

```bash
python agenteval.py \
  --resource-group "your-resource-group" \
  --project "your-project-name" \
  --agent-name "your-agent-name"
```

#### 3. Batch Evaluation

Run batch evaluation on multiple data points:

```bash
python batchevalagent.py \
  --resource-group "your-resource-group" \
  --project "your-project-name" \
  --agent-name "your-agent-name"
```

#### 4. Red Team Testing

Run security and safety tests:

```bash
python redteam.py \
  --resource-group "your-resource-group" \
  --project "your-project-name" \
  --agent-name "your-agent-name"
```

## CI/CD with GitHub Actions

This project includes a GitHub Actions workflow for automated testing and evaluation.

### Setting Up GitHub Actions

#### Step 1: Configure GitHub Secrets

Navigate to your repository settings and add the following secrets:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret** and add each of the following:

| Secret Name | Description |
|-------------|-------------|
| `AZURE_CREDENTIALS` | Azure service principal credentials (JSON format) |
| `AZURE_RESOURCE_GROUP` | Your Azure resource group name |
| `AZURE_AI_PROJECT` | Your Azure AI project name |
| `AZURE_AI_PROJECT_ENDPOINT` | Your Azure AI project endpoint URL |
| `AZURE_OPENAI_KEY` | Azure OpenAI service key |
| `AZURE_OPENAI_ENDPOINT` | Azure OpenAI endpoint URL |
| `AZURE_AI_MODEL_DEPLOYMENT_NAME` | Azure AI model deployment name |
| `AZURE_OPENAI_DEPLOYMENT` | Azure OpenAI deployment name |
| `AZURE_AI_SEARCH_INDEX_NAME` | Azure AI Search index name (optional) |
| `AZURE_OPENAI_CHAT_DEPLOYMENT_NAME` | Azure OpenAI chat deployment name |
| `AZURE_OPENAI_API_VERSION` | Azure OpenAI API version |
| `AZURE_OPENAI_RESPONSES_DEPLOYMENT_NAME` | Azure OpenAI responses deployment name |
| `AGENT_NAME` | Name of your AI agent |

#### Step 2: Create Azure Service Principal

To create the `AZURE_CREDENTIALS` secret, run:

```bash
az ad sp create-for-rbac \
  --name "github-actions-sp" \
  --role contributor \
  --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
  --sdk-auth
```

Copy the entire JSON output and use it as the value for `AZURE_CREDENTIALS`.

#### Step 3: Configure Environment

1. Go to **Settings** → **Environments**
2. Create a new environment named `dev`
3. Optionally, add protection rules and required reviewers

### Executing the CI/CD Pipeline

The workflow is triggered manually using `workflow_dispatch`:

#### Method 1: GitHub UI

1. Navigate to your repository on GitHub
2. Click on the **Actions** tab
3. Select **Agent Consumption - Single Environment** workflow from the left sidebar
4. Click **Run workflow** button
5. Select the branch (usually `main`)
6. Click the green **Run workflow** button

#### Method 2: GitHub CLI

```bash
# Install GitHub CLI if not already installed
# https://cli.github.com/

# Trigger the workflow
gh workflow run "Agent Consumption - Single Environment" --ref main
```

#### Method 3: REST API

```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/{owner}/{repo}/actions/workflows/agent-consumption-single-env.yml/dispatches \
  -d '{"ref":"main"}'
```

Replace `{owner}` with your GitHub username and `{repo}` with the repository name.

### Workflow Execution Steps

The CI/CD workflow performs the following steps automatically:

1. **Checkout Repository**: Clones the repository code
2. **Setup Python**: Installs Python 3.12
3. **Install Dependencies**: Installs all required Python packages from `requirements.txt`
4. **Azure Login**: Authenticates with Azure using service principal credentials
5. **Run Agent Execution Test**: Executes the agent using `exagent.py`
6. **Run Evaluation**: Evaluates agent responses using `agenteval.py`
7. **Run Batch Evaluation**: Performs batch evaluation using `batchevalagent.py`
8. **Run Red Team Tests**: Conducts security testing using `redteam.py`

### Monitoring Workflow Runs

1. Go to the **Actions** tab in your repository
2. Click on the workflow run you want to monitor
3. View logs for each step by clicking on the step name
4. Check for any errors or warnings in the execution logs

## Project Structure

```
TechconnectFY26Hackfest/
├── .github/
│   └── workflows/
│       └── agent-consumption-single-env.yml  # CI/CD workflow
├── evaldata/
│   ├── datarfp.jsonl                        # Evaluation dataset 1
│   └── datarfpagent.jsonl                   # Evaluation dataset 2
├── exagent.py                               # Agent execution module
├── agenteval.py                             # Agent evaluation module
├── batchevalagent.py                        # Batch evaluation module
├── redteam.py                               # Red team testing module
├── requirements.txt                         # Python dependencies
├── .gitignore                               # Git ignore rules
└── README.md                                # This file
```

## Modules Description

### exagent.py
Consumes and executes existing Azure AI agents. This module connects to your deployed agent and runs test queries.

**Key Features:**
- Azure AI Projects integration
- Agent consumption and execution
- Response collection and logging

### agenteval.py
Performs evaluation on agent responses using Azure AI Evaluation and OpenAI metrics.

**Key Features:**
- Automated evaluation metrics
- Response quality assessment
- Performance benchmarking

### batchevalagent.py
Runs batch evaluations on multiple data points efficiently.

**Key Features:**
- Bulk processing capabilities
- Parallel evaluation support
- Aggregated results reporting

### redteam.py
Conducts red team testing to identify potential security and safety vulnerabilities using PyRIT.

**Key Features:**
- Security vulnerability detection
- Safety compliance testing
- Adversarial testing scenarios
- Comprehensive reporting

## Contributing

We welcome contributions to improve this framework! Here's how you can contribute:

1. **Fork the repository** and create your feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following these guidelines:
   - Write clear, commented code
   - Follow existing code style and conventions
   - Test your changes thoroughly
   - Update documentation as needed

3. **Commit your changes** with descriptive messages:
   ```bash
   git commit -m "Add: brief description of your changes"
   ```

4. **Push to your fork** and submit a Pull Request:
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Pull Request Guidelines**:
   - Provide a clear description of the changes
   - Reference any related issues
   - Ensure all tests pass
   - Wait for review and address feedback

For major changes, please open an issue first to discuss what you would like to change.

## License

This project is part of the TechConnect FY26 Hackfest initiative.

## Support

For issues and questions, please open an issue in the GitHub repository.

---

**Built with ❤️ for TechConnect FY26 Hackfest**
