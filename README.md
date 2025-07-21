# Agentic Motor Insurance Underwriting

[![CI/CD](https://github.com/lingak2311/agentic-motor-underwriting/actions/workflows/ci.yml/badge.svg)](https://github.com/lingak2311/agentic-motor-underwriting/actions/workflows/ci.yml)
[![Deploy](https://github.com/lingak2311/agentic-motor-underwriting/actions/workflows/deploy.yml/badge.svg)](https://github.com/lingak2311/agentic-motor-underwriting/actions/workflows/deploy.yml)

A production-ready agentic AI system for motor insurance underwriting, built on Databricks with best practices for CI/CD, testing, and deployment.

## 🚀 Overview

This project demonstrates an intelligent motor insurance underwriting system using **Agentic AI** principles. The system leverages multiple specialized AI agents to automate the underwriting process, from quote validation to risk assessment and pricing decisions.

### Key Features

- **🤖 Multi-Agent Architecture**: Specialized agents for different underwriting tasks
- **🔍 Quote Validation**: Automated verification of customer claims and disclosures
- **📊 Risk Assessment**: AI-powered risk scoring using multiple data sources
- **💰 Dynamic Pricing**: Real-time premium calculation based on risk factors
- **🗣️ Call Analysis**: Natural language processing of sales call transcripts
- **🏠 Property Intelligence**: Integration with property risk databases
- **📈 Real-time Dashboard**: Streamlit-based review interface

## 🏗️ Architecture

### Agent System Design

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Base Agent    │    │ Eligibility     │    │ Risk Assessment │
│                 │    │ Agent           │    │ Agent           │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ Pricing Agent   │    │ LangChain       │    │ Unity Catalog   │
│                 │    │ Orchestration   │    │ Data Layer      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Technology Stack

- **Platform**: Databricks with Unity Catalog
- **AI/ML**: LangChain, Meta-Llama-3.1-70B-Instruct
- **Data**: Unity Catalog tables for quotes, claims, property data
- **Orchestration**: Databricks Asset Bundles (DABs)
- **Infrastructure**: Terraform for cloud resources
- **CI/CD**: GitHub Actions
- **Testing**: pytest with Databricks Connect

## 📂 Project Structure

```
agentic-motor-underwriting/
├── README.md                    # This file
├── databricks.yml              # DAB configuration
├── requirements.txt            # Python dependencies
├── pyproject.toml             # Modern Python project config
├── .github/workflows/         # CI/CD pipelines
├── src/agentic_underwriting/  # Main source code
│   ├── agents/               # Agent implementations
│   ├── models/               # Scoring and data models
│   ├── tools/                # LangChain tools
│   └── utils/                # Utilities and configuration
├── notebooks/                 # Databricks notebooks
├── tests/                     # Test suite
├── resources/                 # DAB resource definitions
├── terraform/                 # Infrastructure as Code
└── docs/                      # Additional documentation
```

## 🚦 Quick Start

### Prerequisites

- **Databricks CLI** v0.218.0+
- **Python** 3.9+
- **Terraform** (for infrastructure deployment)
- **Git** for version control

### 1. Clone and Setup

```bash
git clone https://github.com/lingak2311/agentic-motor-underwriting.git
cd agentic-motor-underwriting

# Install dependencies
pip install -r requirements.txt

# Set up development environment
pip install -e .
```

### 2. Configure Databricks

```bash
# Configure Databricks CLI
databricks configure

# Validate DAB configuration
databricks bundle validate
```

### 3. Deploy to Development

```bash
# Deploy to dev environment
databricks bundle deploy --target dev

# Run a sample underwriting job
databricks bundle run --target dev underwriting_pipeline
```

### 4. Run Tests Locally

```bash
# Unit tests
pytest tests/unit/

# Integration tests (requires Databricks connection)
pytest tests/integration/
```

## 🔧 Development Guide

### Setting Up Local Development

1. **Create a virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. **Install in development mode**:
   ```bash
   pip install -e ".[dev]"
   ```

3. **Run pre-commit hooks**:
   ```bash
   pre-commit install
   pre-commit run --all-files
   ```

### Code Organization

- **Agents**: Implement the `BaseAgent` interface for consistency
- **Models**: Use Pydantic for data validation and serialization
- **Tools**: LangChain-compatible tools for agent interactions
- **Utils**: Shared utilities for configuration, logging, and database access

### Testing Strategy

- **Unit Tests**: Test individual components in isolation
- **Integration Tests**: Test end-to-end workflows
- **Notebook Tests**: Validate notebook execution and outputs

## 🚀 Deployment

### Environment Management

The project supports multiple deployment targets:

- **dev**: Development environment with user-specific prefixes
- **staging**: Pre-production testing environment
- **prod**: Production environment with strict governance

### Databricks Asset Bundles (DABs)

Deploy using DABs for full infrastructure and code deployment:

```bash
# Deploy to specific environment
databricks bundle deploy --target dev
databricks bundle deploy --target prod

# Run deployed jobs
databricks bundle run --target prod underwriting_job
```

### Terraform Infrastructure

For cloud infrastructure provisioning:

```bash
cd terraform/
terraform init
terraform plan
terraform apply
```

### CI/CD Pipeline

The project includes automated CI/CD via GitHub Actions:

1. **Pull Request Validation**:
   - Code quality checks
   - Unit test execution
   - Integration test validation

2. **Main Branch Deployment**:
   - Automatic deployment to staging
   - Manual promotion to production

## 📊 Key Components

### 1. Quote Validation Agent

Validates customer-provided information against verified data sources:

```python
from agentic_underwriting.agents import EligibilityAgent

agent = EligibilityAgent()
result = agent.run(quote_data, context={})
```

### 2. Risk Scoring Model

Advanced risk assessment using multiple factors:

```python
from agentic_underwriting.models import RiskScoringModel

model = RiskScoringModel()
risk_score = model.calculate_risk(
    age=35, vehicle_type="SUV", 
    claims_history=1, ncd_years=5
)
```

### 3. LangChain Integration

Tools for agent-based processing:

```python
from agentic_underwriting.tools import get_quote_details_tool

# Use with LangChain agents
tools = [get_quote_details_tool, validate_claims_tool]
agent = initialize_agent(tools, llm)
```

### 4. Dashboard Interface

Streamlit-based review dashboard for underwriters:

```python
streamlit run app/agent_underwriting.py
```

## 🧪 Testing

### Running Tests

```bash
# All tests
pytest

# Unit tests only
pytest tests/unit/

# Integration tests
pytest tests/integration/

# With coverage
pytest --cov=agentic_underwriting tests/
```

### Test Data

The project includes synthetic test data for development and testing:

- Sample quotes and customer profiles
- Mock property and claims data
- Configurable risk scenarios

## 📈 Monitoring and Observability

### Logging

Structured logging throughout the application:

```python
from agentic_underwriting.utils.logging import get_logger

logger = get_logger(__name__)
logger.info("Processing quote", extra={"quote_id": "R9999"})
```

### Metrics

Key performance indicators tracked:

- Processing time per quote
- Agent decision accuracy
- Model prediction quality
- System throughput

## 🔒 Security Considerations

- **Data Encryption**: All data encrypted in transit and at rest
- **Access Control**: Unity Catalog permissions for data governance
- **Secrets Management**: Databricks secrets for sensitive configuration
- **Audit Logging**: Complete audit trail of all decisions

## 🤝 Contributing

We welcome contributions! Please see our contributing guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Standards

- Follow PEP 8 coding standards
- Write comprehensive tests for new features
- Update documentation for API changes
- Use conventional commit messages

## 📚 Additional Resources

- [Databricks Asset Bundles Documentation](https://docs.databricks.com/dev-tools/bundles/)
- [LangChain Documentation](https://python.langchain.com/)
- [Unity Catalog Best Practices](https://docs.databricks.com/data-governance/unity-catalog/best-practices.html)
- [Agentic AI Patterns](https://docs.databricks.com/machine-learning/model-serving/agentic-ai.html)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/lingak2311/agentic-motor-underwriting/issues)
- **Discussions**: [GitHub Discussions](https://github.com/lingak2311/agentic-motor-underwriting/discussions)
- **Documentation**: [Project Wiki](https://github.com/lingak2311/agentic-motor-underwriting/wiki)

---

*Making intelligent underwriting accessible to data enthusiasts everywhere*
