# MoneyWorks AI Accountant Manual

## Executive Summary

This manual provides comprehensive instructions for setting up and developing AI agents that can function as skilled accountants using MoneyWorks through Model Context Protocol (MCP) interfaces. The goal is to bridge the gap between raw API access and accounting expertise, creating AI agents that think, work, and communicate like professional accountants.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [MoneyWorks MCP Setup](#moneyworks-mcp-setup)
4. [Testing Framework](#testing-framework)
5. [Development Methodology](#development-methodology)
6. [Implementation Roadmap](#implementation-roadmap)
7. [Appendices](#appendices)

---

## 1. Project Overview

### Vision
Create AI agents that can perform the full spectrum of accounting tasks using MoneyWorks, from basic data entry to complex financial analysis and advisory services.

### Current State vs. Target State

**Current State: Technical Database Access**
- 44 MCP tools providing raw MoneyWorks API access
- Basic CRUD operations on accounting data
- No accounting domain intelligence
- Limited error context and business logic

**Target State: Intelligent Accounting Assistant**
- AI agents that understand accounting principles
- Context-aware business process automation
- Intelligent data assembly and interpretation
- Advisory capabilities with actionable insights

### Core Challenges

1. **Semantic Gap**: Raw data vs. business meaning
2. **Workflow Intelligence**: Individual tools vs. business processes
3. **Domain Expertise**: Technical validation vs. accounting principles
4. **Contextual Assembly**: Single responses vs. comprehensive analysis

---

## 2. Prerequisites

### System Requirements
- **MoneyWorks Server**: Running and accessible
- **Bun Runtime**: v1.2+ for MCP server execution
- **Node.js**: v18+ for package management
- **Git**: For version control and collaboration

### Knowledge Requirements
- Basic understanding of accounting principles
- Familiarity with MoneyWorks workflows
- Understanding of MCP (Model Context Protocol)
- Experience with Claude Code/Desktop

### Accounting Domain Knowledge
- Chart of accounts structure
- Double-entry bookkeeping principles
- Financial statement relationships
- Business process workflows
- Regulatory compliance requirements

---

## 3. MoneyWorks MCP Setup

### 3.1 Environment Preparation

#### Clone the Core MoneyWorks Project
```bash
# Navigate to your development directory
cd ~/Development/gitprojects/AgileWorksZA

# Clone the mw-core project (if not already done)
git clone <mw-core-repository-url>
cd mw-core/packages/mcp-server
```

#### Install Dependencies
```bash
# Install MCP server dependencies
bun install

# Set up error tracking database
bun run db:migrate

# Build the MCP server
bun run build
```

#### Create MoneyWorks Configuration
```bash
# Copy example config
cp ../api/mw-config.example.json ../api/mw-config.json

# Edit with your MoneyWorks server details
nano ../api/mw-config.json
```

**Configuration Template:**
```json
{
  "host": "your-moneyworks-server.local",
  "port": 6710,
  "dataFile": "YourCompany.moneyworks",
  "username": "your-username",
  "password": "your-password",
  "folderAuth": {
    "folderName": "YourFolder",
    "password": "folder-password"
  }
}
```

### 3.2 Claude Code CLI Setup

#### Add MoneyWorks MCP Server
```bash
# Add to Claude Code CLI (using fish shell)
fish -c "claude mcp add moneyworks-server bun -- run /path/to/mw-core/packages/mcp-server/src/index.ts"

# Verify installation
fish -c "claude mcp list"
```

#### Test CLI Integration
```bash
# Start Claude Code session
claude

# Test MoneyWorks connectivity
# In Claude session: "Use the MoneyWorks MCP server to list available tables"
```

### 3.3 Claude Desktop Setup

#### Configure Claude Desktop
Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "moneyworks": {
      "command": "/Users/yourusername/.bun/bin/bun",
      "args": ["run", "/path/to/mw-core/packages/mcp-server/src/index.ts"],
      "env": {
        "PATH": "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin",
        "MW_CONFIG_PATH": "/path/to/mw-core/packages/api/mw-config.json",
        "TICKETS_DB_PATH": "/path/to/mw-core/packages/mcp-server/data/tickets.db",
        "MW_CACHE_DIR": "/path/to/mw-core/packages/api/cache"
      }
    }
  }
}
```

#### Restart and Test
1. Restart Claude Desktop
2. Test: "What MoneyWorks tools do you have available?"
3. Verify: All 44 tools should be listed

### 3.4 Troubleshooting Setup

#### Common Issues

**Cache Directory Errors:**
```bash
# Create cache directory manually
mkdir -p /path/to/mw-core/packages/api/cache
```

**Permission Issues:**
```bash
# Fix file permissions
chmod +x /path/to/mw-core/packages/mcp-server/src/index.ts
```

**MoneyWorks Connection Issues:**
- Verify MoneyWorks server is running
- Check network connectivity
- Validate credentials in mw-config.json

#### Log Analysis
```bash
# Check Claude Desktop logs
tail -f ~/Library/Logs/Claude/mcp-server-moneyworks.log

# Check for specific errors
grep -i error ~/Library/Logs/Claude/mcp-server-moneyworks.log
```

---

## 4. Testing Framework

### 4.1 Competency Assessment Framework

#### Test Categories

**1. Basic Data Operations (95% Accuracy Target)**
- Create, read, update customer records
- Search and filter transactions
- Generate basic reports

**2. Business Process Workflows (90% Accuracy Target)**
- Complete sales cycle (quote → invoice → payment)
- Purchase cycle (order → receipt → payment)
- Month-end reconciliation processes

**3. Financial Analysis (85% Accuracy Target)**
- Aged trial balance interpretation
- Cash flow analysis
- Variance reporting

**4. Advisory Capabilities (75% Accuracy Target)**
- Identify collection opportunities
- Recommend process improvements
- Explain financial trends

#### Test Scenario Structure
```yaml
scenario_name: "Customer Payment Processing"
description: "Process payment against existing customer invoice"
prerequisites:
  - "Customer 'ACME Corp' exists with open invoice INV-001"
  - "Invoice amount is $1,200.00"
  - "Payment received is $800.00"

steps:
  1. "Find customer ACME Corp"
  2. "Locate open invoice INV-001"
  3. "Verify payment amount is valid"
  4. "Record partial payment of $800"
  5. "Update invoice status to partial"
  6. "Generate payment receipt"

expected_outcomes:
  - "Invoice status changes to 'PA' (Partial)"
  - "Customer balance reduces by $800"
  - "Payment transaction created"
  - "Receipt generated with correct details"

business_validation:
  - "Payment amount <= outstanding balance"
  - "Proper audit trail maintained"
  - "Aging report reflects updated balance"
```

### 4.2 Automated Testing Suite

#### Test Runner Implementation
```typescript
interface TestScenario {
  name: string;
  description: string;
  setup: () => Promise<void>;
  execute: (agent: AIAgent) => Promise<TestResult>;
  validate: (result: any) => Promise<ValidationResult>;
  cleanup: () => Promise<void>;
}

interface TestResult {
  success: boolean;
  executionTime: number;
  toolsUsed: string[];
  errors: string[];
  businessLogicViolations: string[];
}
```

#### Performance Metrics
- **Accuracy**: Percentage of correct outcomes
- **Efficiency**: Tools used vs. optimal path
- **Speed**: Time to completion vs. human benchmark
- **Business Logic Compliance**: Adherence to accounting principles

### 4.3 Continuous Improvement Loop

#### Error Analysis Pipeline
1. **Capture**: Log all agent interactions and outcomes
2. **Categorize**: Technical vs. business logic errors
3. **Analyze**: Root cause identification
4. **Improve**: Update tool metadata and workflows
5. **Retest**: Validate improvements

#### Human Expert Validation
- Monthly review sessions with qualified accountants
- Benchmark against human performance
- Identify knowledge gaps and blind spots

---

## 5. Development Methodology

### 5.1 Enhanced Tool Intelligence

#### Semantic Enrichment Framework
Transform basic field descriptions into business-intelligent metadata:

**Before:**
```json
{
  "status": {
    "type": "string",
    "description": "Transaction status code"
  }
}
```

**After:**
```json
{
  "status": {
    "type": "string",
    "description": "Transaction status in accounting workflow",
    "businessContext": {
      "values": {
        "OP": {
          "meaning": "Open - invoice issued, payment pending",
          "implications": "Affects AR aging and cash flow projections",
          "nextActions": ["Record payment", "Send reminder", "Apply credit"]
        },
        "CL": {
          "meaning": "Closed - fully paid and complete",
          "implications": "No further action required",
          "nextActions": ["Generate receipt", "File documents"]
        }
      }
    },
    "relatedConcepts": ["accounts_receivable", "cash_flow", "aging_reports"],
    "businessRules": ["Cannot modify closed transactions", "Status affects reporting"]
  }
}
```

#### Workflow Documentation System
```json
{
  "workflows": {
    "customer_payment_process": {
      "description": "Process customer payment against outstanding invoices",
      "businessPurpose": "Maintain accurate AR and cash position",
      "steps": [
        {
          "step": 1,
          "tool": "names",
          "operation": "search",
          "purpose": "Verify customer exists and get details",
          "businessValidation": "Customer must be active and not on hold"
        },
        {
          "step": 2,
          "tool": "transactions",
          "operation": "search",
          "purpose": "Find open invoices for customer",
          "businessValidation": "Only process payments against open invoices"
        }
      ],
      "qualityChecks": [
        "Payment amount <= total outstanding",
        "Customer credit status acceptable",
        "Proper authorization for large payments"
      ]
    }
  }
}
```

### 5.2 Domain Knowledge Integration

#### Accounting Concepts Database
```json
{
  "concepts": {
    "accounts_receivable": {
      "definition": "Money owed by customers for goods/services delivered",
      "moneyworksImplementation": {
        "tables": ["Name", "Transaction"],
        "filters": "Type=SI AND Status IN ('OP', 'PA')",
        "calculations": "SUM(Gross - AmtPaid)"
      },
      "businessRules": [
        "Must be aged monthly for collection purposes",
        "Write-offs require management approval",
        "Bad debt provisions affect financial statements"
      ],
      "relatedReports": ["Customer Aging", "AR Summary", "Cash Flow"],
      "kpis": ["Days Sales Outstanding", "Collection Rate", "Bad Debt %"]
    }
  }
}
```

#### Business Process Patterns
```json
{
  "processes": {
    "month_end_close": {
      "description": "Monthly accounting close process",
      "frequency": "Monthly",
      "timing": "First 5 business days of new month",
      "checklist": [
        "Reconcile all bank accounts",
        "Review and approve journal entries",
        "Generate aged trial balance",
        "Prepare management reports",
        "Close accounting period"
      ],
      "toolSequences": {
        "bank_reconciliation": ["accounts->search", "transactions->search", "reconcile"],
        "aging_analysis": ["names->search", "transactions->summary", "generateReport"]
      }
    }
  }
}
```

### 5.3 Intelligence Architecture

#### Contextual Assembly Engine
```typescript
interface ContextualAssembly {
  query: string;
  requiredData: DataRequirement[];
  assemblyLogic: AssemblyRule[];
  businessValidation: ValidationRule[];
  outputFormat: OutputSpecification;
}

interface DataRequirement {
  concept: string;
  tables: string[];
  relationships: string[];
  filters: FilterCriteria[];
}
```

#### Decision Support System
```typescript
interface DecisionSupport {
  situation: BusinessSituation;
  recommendations: Recommendation[];
  riskFactors: RiskFactor[];
  alternatives: Alternative[];
}

interface Recommendation {
  action: string;
  reasoning: string;
  impact: ImpactAssessment;
  urgency: UrgencyLevel;
}
```

---

## 6. Implementation Roadmap

### Phase 1: Foundation (Months 1-2)
**Goal**: Establish enhanced MCP server with business intelligence

**Deliverables:**
- Enhanced tool metadata with business context
- Basic workflow documentation
- Initial testing framework
- Error tracking and improvement pipeline

**Success Criteria:**
- 95% accuracy on basic data operations
- 50% reduction in tool usage for common tasks
- Automated error categorization and logging

### Phase 2: Business Intelligence (Months 3-4)
**Goal**: Implement accounting domain knowledge and workflow intelligence

**Deliverables:**
- Comprehensive accounting concepts database
- Business process pattern library
- Contextual data assembly engine
- Advanced testing scenarios

**Success Criteria:**
- 90% accuracy on business process workflows
- AI agents can explain accounting implications
- Automated workflow optimization recommendations

### Phase 3: Advisory Capabilities (Months 5-6)
**Goal**: Enable advanced analysis and advisory functions

**Deliverables:**
- Decision support system
- Predictive analytics capabilities
- Advanced reporting and insights
- Human expert validation framework

**Success Criteria:**
- 85% accuracy on financial analysis tasks
- AI agents provide actionable business insights
- Performance comparable to junior accountants

### Phase 4: Production Deployment (Months 7-8)
**Goal**: Full deployment with continuous improvement

**Deliverables:**
- Production-ready AI accounting assistant
- Comprehensive training materials
- Ongoing improvement methodology
- Performance monitoring dashboard

**Success Criteria:**
- 75% accuracy on advisory capabilities
- Positive ROI demonstration
- User adoption and satisfaction metrics

---

## 7. Appendices

### Appendix A: Tool Reference

#### Current MoneyWorks MCP Tools (44 total)

**Core Operations:**
- `accounts` - Account management and search
- `transactions` - Transaction operations
- `names` - Contact/customer management
- `builds` - Build and assembly management

**System Information:**
- `listTables` - List all MoneyWorks tables
- `describeTableSchema` - Get table structure and fields
- `getSystemInfo` - MoneyWorks system information
- `getCompanyInformation` - Company settings and details

**Advanced Features:**
- Currency operations (`convertCurrency`, `getCurrencyInfo`)
- Date formatting (`getDateFormats`, `parseDateString`)
- Validation rules (`getValidationRules`, `getBusinessRules`)
- Permissions (`checkUserPermissions`, `getUserRoles`)
- Expression evaluation (`evaluateExpression`, `evaluateTemplate`)
- Report generation (`generateReport`, `listCommonReports`)
- Field labels (`getTableLabels`, `generateAllLabels`)

**Error Tracking:**
- `logTicket` - Manual issue logging
- Automatic error tracking for all failed operations

### Appendix B: Configuration Templates

#### MoneyWorks Configuration
```json
{
  "host": "moneyworks-server.local",
  "port": 6710,
  "dataFile": "CompanyName.moneyworks",
  "username": "api-user",
  "password": "secure-password",
  "folderAuth": {
    "folderName": "CompanyFolder",
    "password": "folder-password"
  }
}
```

#### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "moneyworks": {
      "command": "/path/to/bun",
      "args": ["run", "/path/to/mcp-server/src/index.ts"],
      "env": {
        "PATH": "/usr/local/bin:/usr/bin:/bin",
        "MW_CONFIG_PATH": "/path/to/mw-config.json",
        "TICKETS_DB_PATH": "/path/to/tickets.db",
        "MW_CACHE_DIR": "/path/to/cache"
      }
    }
  }
}
```

### Appendix C: Business Logic Examples

#### Account Types and Their Purposes
```json
{
  "accountTypes": {
    "A": {
      "name": "Asset",
      "normalBalance": "Debit",
      "purpose": "Resources owned by the company",
      "examples": ["Cash", "Accounts Receivable", "Inventory"],
      "reportingCategory": "Balance Sheet"
    },
    "L": {
      "name": "Liability", 
      "normalBalance": "Credit",
      "purpose": "Debts owed by the company",
      "examples": ["Accounts Payable", "Loans", "Accrued Expenses"],
      "reportingCategory": "Balance Sheet"
    },
    "I": {
      "name": "Income",
      "normalBalance": "Credit", 
      "purpose": "Revenue earned by the company",
      "examples": ["Sales Revenue", "Interest Income", "Rental Income"],
      "reportingCategory": "Profit & Loss"
    },
    "E": {
      "name": "Expense",
      "normalBalance": "Debit",
      "purpose": "Costs incurred to generate revenue",
      "examples": ["Cost of Goods Sold", "Salaries", "Rent"],
      "reportingCategory": "Profit & Loss"
    }
  }
}
```

#### Transaction Types and Workflows
```json
{
  "transactionTypes": {
    "SI": {
      "name": "Sales Invoice",
      "purpose": "Bill customer for goods/services",
      "workflow": ["Create invoice", "Send to customer", "Receive payment"],
      "affectedAccounts": ["Sales Revenue (Credit)", "Accounts Receivable (Debit)"],
      "businessRules": ["Customer must exist", "Items must be available"]
    },
    "SR": {
      "name": "Sales Receipt", 
      "purpose": "Record payment from customer",
      "workflow": ["Identify customer", "Apply to invoices", "Update balances"],
      "affectedAccounts": ["Cash (Debit)", "Accounts Receivable (Credit)"],
      "businessRules": ["Payment <= outstanding balance", "Customer must have open invoices"]
    }
  }
}
```

---

## Getting Started

1. **Set up MoneyWorks MCP** following Section 3
2. **Run basic tests** using the examples in Section 4
3. **Review the methodology** in Section 5
4. **Begin implementation** following the roadmap in Section 6

For questions or support, refer to the error tracking system or consult with the development team.

---

*This manual is a living document and should be updated as the project evolves and new insights are gained.*