# MoneyWorks AI Accountant

> Developing AI agents that think, work, and communicate like professional accountants using MoneyWorks through intelligent MCP interfaces.

## 🎯 Vision

Transform AI agents from simple API consumers into skilled accounting professionals who understand business context, apply accounting principles, and provide intelligent insights using MoneyWorks data.

## 🚀 Project Overview

This project bridges the gap between raw MoneyWorks API access and true accounting expertise by:

- **🧠 Embedding Business Intelligence** directly into MCP tool metadata
- **📊 Providing Contextual Data Assembly** that understands accounting relationships
- **⚖️ Applying Accounting Principles** automatically to all operations
- **📈 Enabling Continuous Learning** through systematic error analysis and improvement
- **🎓 Creating Competency Testing** frameworks to validate AI accounting skills

## 🏗️ Architecture

```
AI Agent Layer (Claude, etc.)
           ↓
Enhanced MCP Interface Layer
  • Business Logic Engine
  • Domain Knowledge Model  
  • Decision Support System
  • Workflow Intelligence
  • Error Tracking & Learning
           ↓
Core MCP Server (44 tools)
           ↓
MoneyWorks API & Database
```

## 📚 Documentation

- **[CLAUDE.md](CLAUDE.md)** - Guidelines for AI agents working on this project
- **[DESIGN.md](DESIGN.md)** - Comprehensive technical architecture and methodology
- **[Setup Manual](../../MONEYWORKS_AI_ACCOUNTANT_MANUAL.md)** - Complete setup and development guide

## 🎯 Current Capabilities vs. Target State

| Aspect | Current State | Target State |
|--------|---------------|--------------|
| **Data Access** | ✅ 44 MCP tools for raw API access | ✅ Same tools + business intelligence |
| **Business Logic** | ❌ No accounting principles | ✅ Embedded accounting expertise |
| **Error Handling** | ⚠️ Technical errors only | ✅ Business context + learning |
| **Workflow Intelligence** | ❌ Individual tool operations | ✅ Complete business processes |
| **Advisory Capabilities** | ❌ Data retrieval only | ✅ Analysis + recommendations |
| **Learning System** | ❌ Static functionality | ✅ Continuous improvement |

## 🛠️ Development Phases

### Phase 1: Foundation (Months 1-2)
- Enhanced tool metadata with business context
- Basic business rule validation
- Error tracking and improvement pipeline
- **Target**: 95% accuracy on basic operations

### Phase 2: Business Intelligence (Months 3-4)
- Comprehensive accounting domain knowledge
- Workflow pattern recognition
- Contextual data assembly
- **Target**: 90% accuracy on business processes

### Phase 3: Advisory Capabilities (Months 5-6)
- Decision support system
- Predictive analytics
- Advanced reporting and insights
- **Target**: 85% accuracy on financial analysis

### Phase 4: Production Deployment (Months 7-8)
- Full AI accounting assistant deployment
- Continuous improvement automation
- Performance monitoring
- **Target**: 75% accuracy on advisory functions

## 🧪 Testing Framework

### Competency Assessment Levels

- **Basic Operations** (95% accuracy): CRUD operations with business validation
- **Business Workflows** (90% accuracy): Complete accounting processes  
- **Financial Analysis** (85% accuracy): Interpretation and insights
- **Advisory Functions** (75% accuracy): Recommendations and explanations

### Example Test Scenario
```yaml
scenario: "Customer Payment Processing"
setup: 
  - Customer 'ACME Corp' with open invoice $1,200
  - Payment received: $800
steps:
  - "Find customer and verify status"
  - "Locate open invoices" 
  - "Validate payment amount"
  - "Apply partial payment"
  - "Update customer balance"
expected_outcomes:
  - Invoice status: 'Partial'
  - Customer balance reduced by $800
  - Complete audit trail maintained
```

## 🔧 Technical Stack

- **Runtime**: Bun/Node.js with TypeScript
- **MCP Protocol**: Model Context Protocol for AI integration
- **Database**: SQLite for error tracking and learning
- **MoneyWorks**: REST API integration
- **Testing**: Scenario-based competency assessment

## 🚀 Getting Started

### Prerequisites
- MoneyWorks server running and accessible
- Bun v1.2+ or Node.js v18+
- Access to Claude Code CLI or Claude Desktop

### Quick Setup
```bash
# Clone this repository
git clone https://github.com/hjonck/moneyworks-ai-accountant.git
cd moneyworks-ai-accountant

# Install dependencies
npm install

# Run setup validation
npm run setup:validate

# Start development environment
npm run dev
```

### Configure MoneyWorks MCP
Follow the comprehensive setup guide in [MONEYWORKS_AI_ACCOUNTANT_MANUAL.md](../../MONEYWORKS_AI_ACCOUNTANT_MANUAL.md) for complete configuration instructions.

## 📊 Project Status

| Component | Status | Notes |
|-----------|--------|-------|
| Core MCP Server | ✅ Complete | 44 tools operational |
| Enhanced Metadata | 🚧 In Progress | Business context being added |
| Business Rules Engine | 📋 Planned | Phase 1 deliverable |
| Testing Framework | 📋 Planned | Scenario development underway |
| Documentation | ✅ Complete | Comprehensive guides available |

## 🤝 Contributing

This project requires collaboration between:
- **Technical Developers** - MCP server development and AI integration
- **Accounting Professionals** - Domain expertise and validation
- **AI Specialists** - Agent behavior and learning systems

See [CLAUDE.md](CLAUDE.md) for detailed development guidelines.

## 📈 Success Metrics

- **Accuracy**: AI performance on accounting tasks vs. human experts
- **Efficiency**: Tool usage optimization and process improvement
- **Learning**: Continuous improvement through error analysis
- **Adoption**: User satisfaction and business value demonstration

## 🔮 Future Vision

Creating AI agents that can:
- ✅ **Think like accountants** - Apply proper accounting principles automatically
- ✅ **Work like MoneyWorks experts** - Follow established business workflows  
- ✅ **Communicate like advisors** - Explain findings in clear business terms
- ✅ **Learn from experience** - Continuously improve through systematic feedback

## 📄 License

This project is part of the AgileWorks ecosystem. See LICENSE for details.

---

**Ready to create AI agents that truly understand accounting?** Start with our [setup manual](../../MONEYWORKS_AI_ACCOUNTANT_MANUAL.md) and join the revolution in AI-powered accounting assistance.