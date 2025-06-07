# CLAUDE.md

This file provides guidance to Claude Code and other AI agents when working with the MoneyWorks AI Accountant project.

## Project Mission

Develop AI agents that can function as skilled accountants using MoneyWorks through Model Context Protocol (MCP) interfaces. Transform raw API access into intelligent accounting assistance that thinks, works, and communicates like professional accountants.

## Project Commands

```bash
# Development setup
npm install                 # Install dependencies
npm run dev                 # Start development environment
npm run test               # Run test suite
npm run test:accounting    # Run accounting competency tests
npm run test:workflows     # Run business workflow tests

# Testing and validation
npm run test:scenarios     # Run scenario-based tests
npm run validate:metadata  # Validate tool metadata integrity
npm run benchmark         # Run performance benchmarks against human experts

# Documentation and analysis
npm run docs:generate      # Generate documentation from metadata
npm run analyze:errors     # Analyze error patterns and improvement opportunities
npm run report:competency  # Generate AI competency assessment report
```

## Code Style and Architecture

### TypeScript Best Practices
- **Strict typing**: Use explicit types for all accounting concepts and business logic
- **Domain modeling**: Create strong types that reflect accounting principles
- **Error handling**: Distinguish between technical errors and business rule violations
- **Documentation**: JSDoc comments must include business context, not just technical details

### Accounting Domain Architecture
```typescript
// Good: Business-focused typing
interface AccountingTransaction {
  type: TransactionType;
  amount: MoneyAmount;
  businessPurpose: string;
  complianceChecks: ComplianceRule[];
}

// Avoid: Technical-only typing
interface Transaction {
  type: string;
  amount: number;
  data: any;
}
```

### Business Logic First
- **Business rules**: Implement accounting principles before technical optimizations
- **Validation**: Validate business logic before data validation
- **Error messages**: Use accounting terminology in error messages
- **Workflows**: Design around accounting processes, not API endpoints

## Working with Accounting Concepts

### Core Principles to Follow
1. **Double-entry bookkeeping**: Every transaction affects at least two accounts
2. **Audit trail**: All changes must be traceable and explainable
3. **Period integrity**: Respect accounting periods and closing procedures
4. **Regulatory compliance**: Ensure all operations follow accounting standards
5. **Business context**: Always consider the business purpose of operations

### MoneyWorks Integration Guidelines

#### Tool Enhancement Process
1. **Understand the business purpose** of each MoneyWorks operation
2. **Map accounting concepts** to MoneyWorks data structures
3. **Define business rules** that govern the operation
4. **Create intelligent metadata** that guides AI decision-making
5. **Test with real accounting scenarios**

#### Metadata Enhancement Pattern
```typescript
// Transform basic tool definitions into business-intelligent interfaces
interface EnhancedToolMetadata {
  // Standard MCP schema
  technical: MCPToolSchema;
  
  // Business intelligence layer
  accounting: {
    businessPurpose: string;
    accountingConcepts: string[];
    workflowPosition: WorkflowStep[];
    businessRules: BusinessRule[];
    commonMistakes: string[];
    relatedProcesses: string[];
  };
  
  // Learning and improvement
  examples: {
    scenarios: ScenarioExample[];
    expectedOutcomes: BusinessOutcome[];
    commonErrors: ErrorPattern[];
  };
}
```

### Testing Philosophy

#### Competency-Driven Testing
Tests should validate **accounting competency**, not just technical functionality:

```typescript
// Good: Business competency test
test('AI can process customer payment maintaining AR integrity', async () => {
  const scenario = new CustomerPaymentScenario();
  const result = await aiAgent.processPayment(scenario);
  
  expect(result.businessLogic.arBalanceReduced).toBe(true);
  expect(result.businessLogic.auditTrailComplete).toBe(true);
  expect(result.businessLogic.cashPositionIncreased).toBe(true);
});

// Avoid: Technical-only test
test('payment API returns 200', async () => {
  const response = await api.post('/payment', data);
  expect(response.status).toBe(200);
});
```

#### Test Categories
1. **Basic Operations** (95% accuracy target): CRUD operations with business validation
2. **Business Workflows** (90% accuracy target): Complete accounting processes
3. **Financial Analysis** (85% accuracy target): Interpretation and insights
4. **Advisory Functions** (75% accuracy target): Recommendations and explanations

## AI Agent Development Guidelines

### Thinking Like an Accountant
When developing AI capabilities, consider how a professional accountant would approach each task:

1. **Verify data integrity** before making any changes
2. **Understand the business context** of each transaction
3. **Apply appropriate accounting principles** automatically
4. **Maintain complete audit trails** for all operations
5. **Provide clear explanations** in business terms

### Error Handling and Learning
```typescript
interface AccountingError {
  technicalError?: Error;
  businessRuleViolation?: BusinessRuleViolation;
  accountingImplication: string;
  suggestedCorrection: string;
  learningOpportunity: LearningItem;
}
```

### Decision Support Framework
AI agents should provide recommendations based on:
- **Accounting best practices**
- **Business impact analysis**
- **Risk assessment**
- **Regulatory requirements**
- **Process optimization opportunities**

## File Organization

```
/
├── src/
│   ├── domain/              # Accounting domain models and rules
│   ├── intelligence/        # AI-specific business logic
│   ├── testing/            # Competency testing framework
│   ├── workflows/          # Business process definitions
│   └── metadata/           # Enhanced tool metadata
├── tests/
│   ├── scenarios/          # Real-world accounting scenarios
│   ├── competency/         # AI competency assessments
│   └── benchmarks/         # Performance vs human experts
├── docs/
│   ├── setup/              # Installation and configuration
│   ├── methodology/        # Development approach
│   └── accounting/         # Business domain documentation
└── examples/
    ├── workflows/          # Example business processes
    └── scenarios/          # Sample accounting situations
```

## Development Workflow

### 1. Business Analysis
- **Understand the accounting requirement** thoroughly
- **Research MoneyWorks implementation** of the business process
- **Identify business rules and constraints**
- **Define success criteria** in accounting terms

### 2. Intelligence Design
- **Create enhanced metadata** with business context
- **Design AI decision-making logic** based on accounting principles
- **Plan error handling** for both technical and business issues
- **Define testing scenarios** with realistic data

### 3. Implementation
- **Build technical implementation** following business requirements
- **Implement business rule validation**
- **Add comprehensive logging** for learning and improvement
- **Create clear user-facing explanations**

### 4. Validation
- **Test with accounting scenarios** before technical tests
- **Validate against human expert performance**
- **Review with accounting professionals**
- **Document lessons learned** for future improvements

## Best Practices

### Do
- ✅ **Start with business requirements** before technical implementation
- ✅ **Use accounting terminology** consistently throughout the codebase
- ✅ **Implement complete audit trails** for all operations
- ✅ **Provide business context** in all error messages and responses
- ✅ **Test with realistic accounting scenarios**
- ✅ **Validate business logic** before data validation
- ✅ **Document the "why"** not just the "how"

### Don't
- ❌ **Expose raw API responses** without business interpretation
- ❌ **Implement technical features** without understanding business purpose
- ❌ **Bypass business rules** for technical convenience
- ❌ **Use generic error messages** instead of accounting-specific guidance
- ❌ **Test only happy paths** - accounting has many edge cases
- ❌ **Assume technical correctness** equals business correctness

## Integration with MoneyWorks Core

This project builds upon the existing MoneyWorks MCP server but focuses on:
- **Business intelligence layer** on top of technical API access
- **AI-specific metadata** and decision support
- **Competency testing framework** for AI accounting capabilities
- **Continuous improvement methodology** based on real-world usage

When making changes that affect the core MCP server, coordinate with the main mw-core project to ensure compatibility.

## Contributing

When contributing to this project:
1. **Understand the business context** of your changes
2. **Test with accounting scenarios** not just technical tests
3. **Document business implications** of technical decisions
4. **Consider the learning implications** for AI agents
5. **Review with both technical and accounting perspectives**

## Questions to Ask

Before implementing any feature, ask:
- **What accounting principle does this support?**
- **How would a professional accountant approach this?**
- **What could go wrong from a business perspective?**
- **How will an AI agent learn from this?**
- **What business context should be preserved?**

This project is about creating AI that truly understands accounting, not just processes accounting data.