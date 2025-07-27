# Fraud Detection Bounded Context

## Overview

The **Fraud Detection** bounded context is a specialized domain responsible for assessing and mitigating fraud risks in payment transactions. It provides real-time risk scoring and decision-making capabilities to protect the payment gateway from fraudulent activities while ensuring legitimate transactions proceed smoothly.

## Purpose

This bounded context exists to:
- Assess fraud risk for incoming payment transactions
- Provide real-time risk scoring and decision-making
- Protect the payment gateway from fraudulent activities
- Ensure legitimate transactions are not unnecessarily blocked
- Maintain compliance with fraud prevention regulations
- Provide comprehensive risk analytics and reporting

## Domain Boundaries

### What's Inside the Boundary

**Core Domain Objects:**
- **Risk Assessment**: The primary aggregate representing a fraud risk evaluation
- **Transaction Scorecard**: Comprehensive scoring model for transaction analysis
- **Risk Decision**: Final decision on transaction approval or rejection
- **Risk Level**: Classification of risk (LOW, MEDIUM, HIGH)
- **Score Components**: Individual scoring factors (value, seller, currency, etc.)

**Key Business Processes:**
- Transaction risk assessment
- Multi-factor scoring calculation
- Risk decision making
- Scorecard generation and analysis
- Risk level classification

**Domain Events:**
- `TransactionScorecardCreated`: Generated when comprehensive risk scoring is completed
- `RiskDecisionApproved`: Indicates transaction passed fraud assessment
- `RiskDecisionRejected`: Indicates transaction failed fraud assessment

### What's Outside the Boundary

**Payment Processing**: Actual payment execution and processing (handled by Payment Processing BC)
**Merchant Account Management**: Merchant account operations (handled by Merchant Account Management BC)
**Financial Recording**: Accounting and financial operations (handled by Financial Recording & Reporting BC)
**Refund Management**: Refund policy and operations (handled by Refund Management BC)

## Domain Events

### Incoming Events
- Payment creation events from Payment Processing BC
- Transaction data for risk assessment
- Merchant information for seller scoring

### Outgoing Events
- `RiskDecisionApproved`: Signals safe transaction to Payment Processing BC
- `RiskDecisionRejected`: Signals risky transaction to Payment Processing BC
- `TransactionScorecardCreated`: Provides detailed scoring to downstream systems

## Ubiquitous Language

**Risk Assessment**: The process of evaluating transaction fraud potential
**Scorecard**: Comprehensive risk scoring model with multiple factors
**Risk Decision**: Final determination of transaction approval or rejection
**Risk Level**: Categorization of risk (LOW, MEDIUM, HIGH)
**Value Score**: Risk assessment based on transaction amount
**Seller Score**: Risk assessment based on merchant history
**Currency Score**: Risk assessment based on currency used
**Average Value Score**: Risk assessment based on historical transaction patterns

## Strategic Context

### Supporting Domain
Fraud Detection is a **Supporting Domain** as it provides essential risk management capabilities that enable the core payment processing business.

### Dependencies
- **Upstream**: Payment Processing (for transaction data)
- **Downstream**: Payment Processing (for risk decisions)
- **External**: Fraud detection services, risk databases, compliance systems

## Integration Patterns

### Event-Driven Integration
- Consumes payment events for risk assessment
- Publishes risk decisions for payment processing
- Provides scorecard data for analytics and reporting

### API Integration
- RESTful APIs for risk assessment requests
- Real-time scoring endpoints
- Integration with external fraud detection services

## Business Rules

1. **Risk Scoring**: All transactions must receive a comprehensive risk score
2. **Decision Consistency**: Similar transactions should receive consistent risk decisions
3. **False Positive Management**: Legitimate transactions should not be blocked unnecessarily
4. **Compliance**: Risk assessment must comply with fraud prevention regulations
5. **Performance**: Risk assessment must complete within defined time limits

## Risk Assessment Model

### Scoring Components
1. **Value Score**: Based on transaction amount patterns
2. **Seller Score**: Based on merchant history and reputation
3. **Average Value Score**: Based on historical transaction value patterns
4. **Currency Score**: Based on currency risk factors

### Risk Level Classification
- **LOW**: Score 0-30 (Green zone - safe transactions)
- **MEDIUM**: Score 31-70 (Yellow zone - requires review)
- **HIGH**: Score 71-100 (Red zone - high risk)

### Decision Logic
- **APPROVED**: Transactions with LOW risk or approved MEDIUM risk
- **REJECTED**: Transactions with HIGH risk or rejected MEDIUM risk

## Success Metrics

- Fraud detection accuracy (true positive rate)
- False positive rate (legitimate transactions blocked)
- Risk assessment response time
- Fraud prevention effectiveness
- Compliance with fraud prevention regulations 