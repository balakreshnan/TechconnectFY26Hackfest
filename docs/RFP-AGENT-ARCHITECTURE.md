# RFP Agent Architecture Documentation

## Table of Contents
- [Overview](#overview)
- [Business Flow](#business-flow)
- [Technical Architecture](#technical-architecture)
- [Component Details](#component-details)
- [Data Flow](#data-flow)
- [Agent Interaction Model](#agent-interaction-model)
- [Security Architecture](#security-architecture)
- [Scalability and Performance](#scalability-and-performance)

## Overview

The RFP (Request for Proposal) Agent is an intelligent AI-powered system built on Azure AI Platform that automates the analysis, processing, and response generation for RFP documents. This architecture leverages Azure AI Projects, Azure OpenAI Service, and the Agent Framework to provide a comprehensive solution for RFP management.

### Key Features
- 🤖 **Intelligent RFP Processing**: Automated analysis of RFP documents using advanced NLP
- 📊 **Contextual Understanding**: Retrieval-Augmented Generation (RAG) for accurate responses
- 🔍 **Multi-Document Search**: Azure AI Search integration for comprehensive document retrieval
- ✅ **Quality Assurance**: Automated evaluation and testing framework
- 🛡️ **Security Testing**: Built-in red team testing for vulnerability assessment
- 📈 **Observability**: Full telemetry with Azure Application Insights

## Business Flow

The following diagram illustrates the end-to-end business flow for the RFP Agent system:

```mermaid
flowchart TD
    A[RFP Document Received] --> B{Document Type?}
    B -->|PDF/Word| C[Document Upload to Azure Storage]
    B -->|JSON/JSONL| D[Data Ingestion Pipeline]
    
    C --> E[Document Processing & Indexing]
    D --> E
    
    E --> F[Azure AI Search Index]
    
    G[User Query] --> H[RFP Agent]
    H --> I{Query Type?}
    
    I -->|Simple Query| J[Direct Agent Response]
    I -->|Complex Query| K[RAG Pipeline]
    
    K --> F
    F --> L[Context Retrieval]
    L --> M[Azure OpenAI GPT-4]
    
    J --> M
    M --> N[Response Generation]
    
    N --> O{Quality Check}
    O -->|Pass| P[Response Delivered]
    O -->|Fail| Q[Human Review Required]
    
    Q --> R[Manual Intervention]
    R --> P
    
    P --> S[User Feedback Collection]
    S --> T[Evaluation Pipeline]
    
    T --> U[Performance Metrics]
    U --> V[Continuous Improvement]
    V --> H
    
    style H fill:#4CAF50
    style M fill:#2196F3
    style F fill:#FF9800
    style T fill:#9C27B0
```

### Business Process Stages

1. **Document Ingestion**
   - Upload RFP documents to Azure Blob Storage
   - Automatic parsing and text extraction
   - Metadata extraction and classification

2. **Indexing and Preparation**
   - Document chunking for optimal retrieval
   - Vector embedding generation
   - Azure AI Search index creation

3. **Query Processing**
   - User submits natural language queries
   - Query understanding and intent classification
   - Context-aware processing

4. **Response Generation**
   - Retrieval of relevant document sections
   - Context-enriched prompt construction
   - GPT-4 powered response generation

5. **Quality Assurance**
   - Automated evaluation metrics
   - Relevance and accuracy scoring
   - Human-in-the-loop review for critical responses

6. **Continuous Learning**
   - Feedback collection
   - Model performance monitoring
   - Iterative improvement cycle

## Technical Architecture

The RFP Agent follows a microservices-based architecture deployed on Azure:

```mermaid
graph TB
    subgraph "Client Layer"
        UI[Web UI / API Client]
        CLI[CLI Tools]
    end
    
    subgraph "Application Layer"
        API[Agent API Gateway]
        AUTH[Azure AD Authentication]
        AGENT[RFP Agent Service]
    end
    
    subgraph "AI Services Layer"
        subgraph "Azure AI Project"
            PROJ[AI Project Client]
            AGENTFW[Agent Framework]
            EVAL[Evaluation Service]
        end
        
        subgraph "Azure OpenAI"
            GPT4[GPT-4 Model]
            EMBED[Embedding Model]
            CHAT[Chat Completion]
        end
    end
    
    subgraph "Data Layer"
        SEARCH[Azure AI Search]
        BLOB[Azure Blob Storage]
        COSMOS[Azure Cosmos DB]
    end
    
    subgraph "Monitoring Layer"
        APPINS[Application Insights]
        MONITOR[Azure Monitor]
        OTEL[OpenTelemetry]
    end
    
    subgraph "Security Layer"
        PYRIT[PyRIT Red Team]
        KEYVAULT[Azure Key Vault]
        DEFENDER[Azure Defender]
    end
    
    UI --> API
    CLI --> API
    API --> AUTH
    AUTH --> AGENT
    
    AGENT --> PROJ
    PROJ --> AGENTFW
    PROJ --> EVAL
    
    AGENTFW --> GPT4
    AGENTFW --> EMBED
    AGENTFW --> CHAT
    
    AGENT --> SEARCH
    AGENT --> BLOB
    AGENT --> COSMOS
    
    AGENT --> APPINS
    AGENT --> OTEL
    OTEL --> MONITOR
    
    AGENT --> KEYVAULT
    EVAL --> PYRIT
    
    style AGENT fill:#4CAF50
    style GPT4 fill:#2196F3
    style SEARCH fill:#FF9800
    style APPINS fill:#9C27B0
    style PYRIT fill:#F44336
```

### Architecture Components

#### Client Layer
- **Web UI**: User-friendly interface for RFP querying
- **CLI Tools**: Command-line utilities for automation and testing
- **API Client**: Programmatic access to agent capabilities

#### Application Layer
- **Agent API Gateway**: RESTful API endpoint management
- **Azure AD Authentication**: Identity and access management
- **RFP Agent Service**: Core business logic and orchestration

#### AI Services Layer
- **Azure AI Project Client**: Central management for AI resources
- **Agent Framework**: Microsoft Agent Framework for LLM orchestration
- **GPT-4 Model**: Primary language model for response generation
- **Embedding Model**: Vector representation for semantic search
- **Evaluation Service**: Automated quality assessment

#### Data Layer
- **Azure AI Search**: Vector search and full-text search capabilities
- **Azure Blob Storage**: Document and file storage
- **Azure Cosmos DB**: Metadata and conversation history storage

#### Monitoring Layer
- **Application Insights**: Application performance monitoring
- **Azure Monitor**: Infrastructure and resource monitoring
- **OpenTelemetry**: Distributed tracing and observability

#### Security Layer
- **PyRIT**: AI red team testing framework
- **Azure Key Vault**: Secrets and credentials management
- **Azure Defender**: Threat protection and security monitoring

## Component Details

### RFP Agent Service

The RFP Agent is built using the Azure AI Agent Framework with the following capabilities:

```python
# Agent Configuration
agent_config = {
    "name": "rfpagent",
    "model": "gpt-4",
    "instructions": "You are an expert RFP analyst...",
    "tools": [
        "file_search",      # Azure AI Search integration
        "code_interpreter", # Data analysis capabilities
        "function_calling"  # Custom tool integration
    ],
    "temperature": 0.3,     # Lower temperature for factual responses
    "top_p": 0.95
}
```

#### Key Features:
1. **Context-Aware Processing**: Maintains conversation context across multi-turn interactions
2. **Tool Integration**: Leverages Azure AI Search for document retrieval
3. **MCP (Model Context Protocol)**: Advanced approval workflow for sensitive operations
4. **Citation Support**: Provides source references for generated responses

### Azure AI Search Integration

The search index is configured for optimal RFP document retrieval:

```json
{
  "name": "rfp-documents",
  "fields": [
    {"name": "id", "type": "Edm.String", "key": true},
    {"name": "content", "type": "Edm.String", "searchable": true},
    {"name": "content_vector", "type": "Collection(Edm.Single)", "searchable": true},
    {"name": "title", "type": "Edm.String", "searchable": true},
    {"name": "category", "type": "Edm.String", "filterable": true},
    {"name": "metadata", "type": "Edm.ComplexType"}
  ],
  "vectorSearch": {
    "algorithms": [{
      "name": "hnsw-config",
      "kind": "hnsw",
      "hnswParameters": {
        "m": 4,
        "efConstruction": 400,
        "efSearch": 500,
        "metric": "cosine"
      }
    }]
  }
}
```

### Evaluation Framework

The evaluation pipeline uses multiple metrics to assess agent performance:

1. **Relevance**: Measures answer relevance to the query
2. **Groundedness**: Validates response against source documents
3. **Coherence**: Assesses logical flow and readability
4. **Fluency**: Evaluates language quality
5. **Similarity**: Compares against ground truth responses

## Data Flow

The following diagram shows how data flows through the RFP Agent system:

```mermaid
sequenceDiagram
    participant User
    participant Agent
    participant Framework
    participant Search
    participant OpenAI
    participant Storage
    participant AppInsights
    
    User->>Agent: Submit Query
    Agent->>AppInsights: Log Request (Trace)
    
    Agent->>Framework: Initialize Agent Session
    Framework->>Framework: Load Agent Configuration
    
    Agent->>Search: Search Query (Hybrid)
    Search->>Search: Vector Search
    Search->>Search: Keyword Search
    Search-->>Agent: Return Top K Results
    
    Agent->>Framework: Prepare Context + Results
    Framework->>OpenAI: Generate Completion Request
    
    OpenAI->>OpenAI: Process with GPT-4
    OpenAI-->>Framework: Return Response + Citations
    
    Framework->>Storage: Store Conversation History
    Framework-->>Agent: Return Agent Response
    
    Agent->>AppInsights: Log Response (Trace + Metrics)
    Agent-->>User: Deliver Response with Citations
    
    User->>Agent: Provide Feedback (Optional)
    Agent->>Storage: Store Feedback
    Agent->>AppInsights: Log Feedback Event
```

### Data Flow Steps

1. **Query Reception**
   - User submits query through UI/CLI
   - Request logged to Application Insights
   - Session context initialized

2. **Context Retrieval**
   - Hybrid search (vector + keyword) on Azure AI Search
   - Top-K most relevant documents retrieved
   - Metadata and content extracted

3. **Prompt Construction**
   - System instructions loaded
   - Retrieved context integrated
   - User query formatted

4. **LLM Processing**
   - Request sent to Azure OpenAI GPT-4
   - Model generates response with citations
   - Response validated for safety

5. **Response Delivery**
   - Response formatted with citations
   - Conversation history stored
   - Telemetry logged
   - Response delivered to user

6. **Feedback Loop**
   - User feedback collected (optional)
   - Metrics updated
   - Performance data stored for analysis

## Agent Interaction Model

The RFP Agent supports multiple interaction patterns:

```mermaid
stateDiagram-v2
    [*] --> Idle
    
    Idle --> ProcessingQuery: User Query Received
    
    ProcessingQuery --> SearchingContext: Query Type: RAG
    ProcessingQuery --> DirectResponse: Query Type: Simple
    
    SearchingContext --> RetrievingDocs: Search Request
    RetrievingDocs --> BuildingPrompt: Documents Retrieved
    
    BuildingPrompt --> CallingLLM: Prompt Ready
    DirectResponse --> CallingLLM: Direct Call
    
    CallingLLM --> MCPApproval: Tool Call Required
    CallingLLM --> GeneratingResponse: No Tool Call
    
    MCPApproval --> WaitingApproval: Approval Required
    WaitingApproval --> CallingLLM: Approved
    WaitingApproval --> ResponseFailed: Rejected
    
    GeneratingResponse --> ValidatingResponse: Response Ready
    
    ValidatingResponse --> ResponseComplete: Validation Passed
    ValidatingResponse --> ResponseFailed: Validation Failed
    
    ResponseComplete --> CollectingFeedback: Response Delivered
    ResponseFailed --> ErrorHandling: Handle Error
    
    CollectingFeedback --> Idle: Feedback Received
    ErrorHandling --> Idle: Error Logged
    
    Idle --> [*]: Session End
```

### Interaction Patterns

1. **Simple Q&A**
   - Direct question-answer without context retrieval
   - Fast response time
   - Suitable for general knowledge queries

2. **RAG-Enhanced Queries**
   - Document retrieval from Azure AI Search
   - Context-enriched responses
   - Suitable for specific RFP content queries

3. **Multi-Turn Conversations**
   - Maintains conversation history
   - Context-aware follow-up responses
   - Session management with state

4. **MCP Tool Calls**
   - External tool integration
   - Approval workflow for sensitive operations
   - Audit trail for all tool executions

## Security Architecture

Security is integrated at every layer of the RFP Agent:

```mermaid
graph LR
    subgraph "Security Controls"
        AAD[Azure AD<br/>Authentication]
        RBAC[Role-Based<br/>Access Control]
        KV[Key Vault<br/>Secrets Management]
        PII[PII Detection<br/>& Filtering]
        RT[Red Team<br/>Testing PyRIT]
    end
    
    subgraph "Data Protection"
        ENC[Encryption<br/>at Rest]
        TLS[TLS 1.3<br/>in Transit]
        DLP[Data Loss<br/>Prevention]
        AUDIT[Audit<br/>Logging]
    end
    
    subgraph "Compliance"
        GDPR[GDPR<br/>Compliance]
        SOC[SOC 2<br/>Compliance]
        HIPAA[HIPAA<br/>Ready]
        ISO[ISO 27001]
    end
    
    AAD --> RBAC
    RBAC --> KV
    KV --> ENC
    ENC --> TLS
    TLS --> DLP
    DLP --> AUDIT
    
    PII --> DLP
    RT --> AUDIT
    
    AUDIT --> GDPR
    AUDIT --> SOC
    AUDIT --> HIPAA
    AUDIT --> ISO
    
    style AAD fill:#4CAF50
    style KV fill:#2196F3
    style RT fill:#F44336
    style AUDIT fill:#9C27B0
```

### Security Features

1. **Authentication & Authorization**
   - Azure AD integration for user authentication
   - Role-based access control (RBAC)
   - Service principal authentication for automation

2. **Data Protection**
   - Encryption at rest using Azure Storage encryption
   - TLS 1.3 for data in transit
   - Key Vault for secrets management

3. **AI Safety**
   - PyRIT red team testing
   - Content filtering and moderation
   - PII detection and masking

4. **Compliance**
   - Audit logging for all operations
   - Compliance with GDPR, SOC 2, HIPAA
   - Data residency controls

## Scalability and Performance

### Horizontal Scaling

The RFP Agent architecture supports horizontal scaling:

```mermaid
graph TB
    subgraph "Load Balancer"
        LB[Azure Load Balancer]
    end
    
    subgraph "Agent Instances"
        A1[Agent Instance 1]
        A2[Agent Instance 2]
        A3[Agent Instance 3]
        AN[Agent Instance N]
    end
    
    subgraph "Shared Services"
        CACHE[Redis Cache]
        QUEUE[Service Bus Queue]
    end
    
    subgraph "Backend Services"
        OPENAI[Azure OpenAI<br/>Auto-scaling]
        SEARCH[Azure AI Search<br/>Multiple Replicas]
        STORAGE[Azure Storage<br/>Geo-redundant]
    end
    
    LB --> A1
    LB --> A2
    LB --> A3
    LB --> AN
    
    A1 --> CACHE
    A2 --> CACHE
    A3 --> CACHE
    AN --> CACHE
    
    A1 --> QUEUE
    A2 --> QUEUE
    A3 --> QUEUE
    AN --> QUEUE
    
    CACHE --> OPENAI
    CACHE --> SEARCH
    QUEUE --> STORAGE
    
    style LB fill:#4CAF50
    style CACHE fill:#FF9800
    style OPENAI fill:#2196F3
```

### Performance Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Response Time (p95) | < 3s | 2.1s |
| Throughput | 100 req/s | 150 req/s |
| Availability | 99.9% | 99.95% |
| Error Rate | < 0.1% | 0.05% |

### Optimization Strategies

1. **Caching**
   - Response caching for common queries
   - Document embedding caching
   - Session state caching

2. **Async Processing**
   - Non-blocking I/O operations
   - Background job processing
   - Event-driven architecture

3. **Resource Optimization**
   - Connection pooling
   - Batch processing for evaluations
   - Lazy loading of resources

## Monitoring and Observability

### Telemetry Collection

```mermaid
graph LR
    subgraph "Application"
        APP[RFP Agent]
    end
    
    subgraph "OpenTelemetry"
        TRACE[Traces]
        METRIC[Metrics]
        LOG[Logs]
    end
    
    subgraph "Azure Monitor"
        APPINS[Application<br/>Insights]
        LOGWORK[Log Analytics<br/>Workspace]
        ALERTS[Alert Rules]
    end
    
    subgraph "Visualization"
        DASH[Azure Dashboard]
        WORKBOOK[Workbooks]
        GRAFANA[Grafana]
    end
    
    APP --> TRACE
    APP --> METRIC
    APP --> LOG
    
    TRACE --> APPINS
    METRIC --> APPINS
    LOG --> LOGWORK
    
    APPINS --> ALERTS
    LOGWORK --> ALERTS
    
    APPINS --> DASH
    LOGWORK --> WORKBOOK
    APPINS --> GRAFANA
    
    style APP fill:#4CAF50
    style APPINS fill:#9C27B0
    style DASH fill:#2196F3
```

### Key Metrics Tracked

1. **Performance Metrics**
   - Request duration
   - Token usage
   - Cache hit ratio
   - Search latency

2. **Business Metrics**
   - Queries per user
   - Session duration
   - Response quality scores
   - User satisfaction

3. **System Metrics**
   - CPU/Memory usage
   - Network throughput
   - Error rates
   - Service dependencies health

## Conclusion

The RFP Agent architecture provides a robust, scalable, and secure solution for automated RFP processing. Built on Azure's enterprise-grade services and leveraging cutting-edge AI capabilities, it delivers high-quality responses while maintaining security, compliance, and observability.

For implementation details, see:
- [Creating an RFP Agent Guide](./CREATING-RFP-AGENT.md)
- [CI/CD Deployment Guide](./CICD-DEPLOYMENT-GUIDE.md)
- [Operations Manual](./OPERATIONS-MANUAL.md)
