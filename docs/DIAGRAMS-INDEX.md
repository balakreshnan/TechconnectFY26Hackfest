# Diagrams Index

This document provides a comprehensive index of all diagrams used in the RFP Agent documentation. All diagrams are created using Mermaid and can be viewed directly in GitHub or any Markdown viewer with Mermaid support.

## Table of Contents
- [Architecture Diagrams](#architecture-diagrams)
- [Process Flow Diagrams](#process-flow-diagrams)
- [CI/CD Diagrams](#cicd-diagrams)
- [Deployment Diagrams](#deployment-diagrams)
- [Monitoring Diagrams](#monitoring-diagrams)

## Architecture Diagrams

### 1. High-Level System Architecture
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#technical-architecture)

Shows the complete technical architecture including:
- Client Layer (Web UI, CLI)
- Application Layer (API Gateway, Agent Service)
- AI Services Layer (Azure AI Project, OpenAI)
- Data Layer (Search, Storage, Database)
- Monitoring Layer (Application Insights)
- Security Layer (PyRIT, Key Vault)

**Use Case**: Understanding overall system design and component relationships

### 2. Component Interaction Model
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#component-details)

Details how different components interact during agent execution.

**Use Case**: Debugging integration issues, understanding data flow

### 3. Security Architecture
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#security-architecture)

Illustrates security controls, data protection, and compliance features.

**Use Case**: Security audits, compliance verification

## Process Flow Diagrams

### 1. Business Flow - End-to-End RFP Processing
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#business-flow)

Shows the complete business process from document receipt to response delivery:
- Document ingestion (PDF/Word/JSON)
- Document processing and indexing
- User query handling
- RAG pipeline execution
- Quality checks
- Response delivery
- Feedback collection

**Use Case**: Business stakeholders understanding the workflow

### 2. Data Flow Sequence
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#data-flow)

Detailed sequence diagram showing:
- User query submission
- Search execution (vector + keyword)
- Context retrieval
- LLM processing
- Response generation with citations
- Telemetry logging

**Use Case**: Understanding request/response lifecycle, optimizing performance

### 3. Agent Interaction State Machine
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#agent-interaction-model)

State diagram showing different interaction patterns:
- Simple Q&A
- RAG-enhanced queries
- Multi-turn conversations
- MCP tool calls with approval workflow

**Use Case**: Understanding agent behavior, implementing new features

## CI/CD Diagrams

### 1. Complete CI/CD Pipeline
**Location**: [CICD-DEPLOYMENT-GUIDE.md](./CICD-DEPLOYMENT-GUIDE.md#cicd-architecture)

Comprehensive pipeline showing:
- CI stages (build, test, evaluation, security)
- Quality gates (test pass rate, evaluation scores)
- CD stages (dev, staging, production)
- Deployment strategies
- Monitoring integration

**Use Case**: Setting up CI/CD, understanding automation flow

### 2. GitFlow Branch Strategy
**Location**: [CICD-DEPLOYMENT-GUIDE.md](./CICD-DEPLOYMENT-GUIDE.md#12-branch-strategy)

Git branching model showing:
- Main and develop branches
- Feature branch workflow
- Release branch process
- Hotfix workflow

**Use Case**: Team collaboration, release management

### 3. Workflow Trigger and Execution
**Location**: [QUICK-REFERENCE.md](./QUICK-REFERENCE.md#3-cicd-pipeline-flow)

Simplified view of CI/CD execution flow.

**Use Case**: Quick reference for developers

## Deployment Diagrams

### 1. Blue-Green Deployment Strategy
**Location**: [CICD-DEPLOYMENT-GUIDE.md](./CICD-DEPLOYMENT-GUIDE.md#61-blue-green-deployment)

Shows:
- Current production environment (blue)
- New version environment (green)
- Traffic switching mechanism
- Validation and rollback process

**Use Case**: Zero-downtime deployments, production updates

### 2. Canary Deployment Strategy
**Location**: [CICD-DEPLOYMENT-GUIDE.md](./CICD-DEPLOYMENT-GUIDE.md#62-canary-deployment)

Illustrates:
- Gradual traffic routing (5% → 25% → 50% → 100%)
- Monitoring at each stage
- Automatic rollback on failure

**Use Case**: Risk mitigation, gradual rollout

### 3. Horizontal Scaling Architecture
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#scalability-and-performance)

Shows:
- Load balancer
- Multiple agent instances
- Shared services (Redis, Service Bus)
- Backend service scaling

**Use Case**: Capacity planning, performance optimization

## Monitoring Diagrams

### 1. Telemetry Collection Flow
**Location**: [RFP-AGENT-ARCHITECTURE.md](./RFP-AGENT-ARCHITECTURE.md#monitoring-and-observability)

Shows how telemetry flows from:
- Application (traces, metrics, logs)
- OpenTelemetry collection
- Azure Monitor ingestion
- Visualization (dashboards, workbooks)

**Use Case**: Setting up monitoring, debugging issues

### 2. Key Metrics Dashboard
**Location**: [QUICK-REFERENCE.md](./QUICK-REFERENCE.md#monitoring-dashboards)

Visual representation of critical metrics:
- Performance metrics (response time, token usage)
- Quality metrics (evaluation scores)
- Reliability metrics (error rate, availability)

**Use Case**: Operations, SLA monitoring

## Workflow Diagrams

### 1. Document Processing Workflow
**Location**: [QUICK-REFERENCE.md](./QUICK-REFERENCE.md#1-document-processing-flow)

Sequence diagram for document upload and indexing:
- Upload to storage
- Automatic indexing
- Embedding generation
- Agent readiness

**Use Case**: Document management, troubleshooting indexing issues

### 2. Query and Response Workflow
**Location**: [QUICK-REFERENCE.md](./QUICK-REFERENCE.md#2-query--response-flow)

Sequence diagram for user query handling:
- Query submission
- Document search
- Context retrieval
- Response generation
- Logging and delivery

**Use Case**: Understanding query processing, performance tuning

### 3. Agent Creation Workflow
**Location**: [CREATING-RFP-AGENT.md](./CREATING-RFP-AGENT.md#architecture-overview)

Step-by-step flow for creating a new agent:
- Azure environment setup
- AI Project creation
- OpenAI model deployment
- Search configuration
- Agent configuration
- Testing and deployment

**Use Case**: New agent setup, onboarding

## Quick Reference Diagrams

### System Overview
**Location**: [QUICK-REFERENCE.md](./QUICK-REFERENCE.md#system-overview-diagram)

Simplified architecture showing main components and their relationships.

**Use Case**: Quick understanding, presentations

## How to Use These Diagrams

### Viewing in GitHub
All diagrams are written in Mermaid syntax and render automatically in GitHub. Simply navigate to the document and scroll to the diagram section.

### Exporting Diagrams
You can export diagrams in various formats:

1. **As PNG/SVG**: Use [Mermaid Live Editor](https://mermaid.live/)
   - Copy the diagram code
   - Paste into the editor
   - Export as PNG or SVG

2. **In Documentation Tools**: Most modern documentation tools support Mermaid:
   - GitBook
   - Docusaurus
   - VuePress
   - MkDocs (with plugin)

3. **In Presentations**: Use Mermaid plugins for:
   - VS Code (with Mermaid Preview extension)
   - Obsidian
   - Notion

### Editing Diagrams
To modify diagrams:
1. Locate the diagram source in the markdown file
2. Edit the Mermaid code within the code fence
3. Preview changes using GitHub or Mermaid Live Editor
4. Submit changes via pull request

## Diagram Conventions

### Colors
- 🟢 **Green** (#4CAF50): Primary components (Agent, CI/CD)
- 🔵 **Blue** (#2196F3): Azure services (OpenAI, Search)
- 🟠 **Orange** (#FF9800): Data stores, decision points
- 🟣 **Purple** (#9C27B0): Monitoring, evaluation
- 🔴 **Red** (#F44336): Security, errors, rollback

### Shapes
- **Rectangle**: Services, components
- **Diamond**: Decision points, conditions
- **Circle**: Start/end points
- **Cylinder**: Databases, storage
- **Dotted lines**: Optional flows, async operations

### Flow Direction
- **LR**: Left to right (for simple flows)
- **TB**: Top to bottom (for hierarchical structures)
- **TD**: Top down (for workflows)

## Diagram Source Locations

| Diagram Type | Primary Location | Also See |
|-------------|------------------|----------|
| Architecture | RFP-AGENT-ARCHITECTURE.md | QUICK-REFERENCE.md |
| CI/CD Flows | CICD-DEPLOYMENT-GUIDE.md | QUICK-REFERENCE.md |
| Process Flows | RFP-AGENT-ARCHITECTURE.md | CREATING-RFP-AGENT.md |
| Deployment | CICD-DEPLOYMENT-GUIDE.md | - |
| Monitoring | RFP-AGENT-ARCHITECTURE.md | QUICK-REFERENCE.md |

## Contributing New Diagrams

When adding new diagrams:

1. **Choose appropriate diagram type**:
   - Flowchart: Process flows, business logic
   - Sequence: Interactions over time
   - State: State machines, lifecycle
   - Graph: Relationships, dependencies

2. **Follow conventions**:
   - Use consistent colors
   - Add meaningful labels
   - Include legends if needed

3. **Document the diagram**:
   - Add to this index
   - Explain use case
   - Provide context in the source document

4. **Test rendering**:
   - Verify on GitHub
   - Check in Mermaid Live Editor
   - Ensure mobile compatibility

## Additional Resources

- [Mermaid Documentation](https://mermaid.js.org/)
- [Mermaid Live Editor](https://mermaid.live/)
- [GitHub Mermaid Support](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/)
- [Diagram Best Practices](https://mermaid.js.org/intro/n00b-gettingStarted.html)

---

**Need a specific diagram?** Open an issue or contact the documentation team.
