# Merchant Account Management Bounded Context

## Overview

The **Merchant Account Management** bounded context is responsible for managing merchant accounts, wallets, and financial settlements within the payment gateway subdomain. It handles the registration of transactions in merchant wallets, manages payout schedules, and ensures proper financial tracking for merchants.

## Purpose

This bounded context exists to:
- Manage merchant accounts and wallet operations
- Register completed transactions in merchant wallets
- Handle merchant payout scheduling and processing
- Provide merchant financial tracking and reporting
- Ensure proper settlement and fund management
- Support merchant onboarding and account maintenance

## Domain Boundaries

### What's Inside the Boundary

**Core Domain Objects:**
- **Merchant Account**: The primary aggregate representing a merchant's account
- **Transaction Wallet**: Digital wallet for managing merchant funds
- **Payout**: Scheduled or immediate fund transfers to merchants
- **Settlement**: Financial settlement process for merchant transactions
- **Wallet Registration**: Process of recording transactions in merchant wallets

**Key Business Processes:**
- Transaction wallet registration
- Merchant payout management
- Settlement processing
- Account balance tracking
- Financial reconciliation

**Domain Events:**
- `TransactionWalletRegistered`: Generated when a transaction is registered in a merchant's wallet

### What's Outside the Boundary

**Payment Processing**: Payment transaction processing (handled by Payment Processing BC)
**Fraud Detection**: Risk assessment and fraud prevention (handled by Fraud Detection BC)
**Financial Recording**: Accounting and financial reporting (handled by Financial Recording & Reporting BC)
**Refund Management**: Refund policy and operations (handled by Refund Management BC)

## Domain Events

### Incoming Events
- Payment completion events from Payment Processing BC
- Transaction approval events for wallet registration
- Settlement requests from Financial Recording BC

### Outgoing Events
- `TransactionWalletRegistered`: Notifies about transaction registration in merchant wallet
- Payout status updates to merchants
- Settlement confirmations to Financial Recording BC

## Ubiquitous Language

**Merchant Account**: A registered account for a business to receive payments
**Transaction Wallet**: Digital wallet where merchant funds are held
**Wallet Registration**: Process of recording a transaction in merchant's wallet
**Payout**: Transfer of funds from wallet to merchant's bank account
**Settlement**: Final financial settlement of merchant transactions
**Scheduled Date**: Planned date for payout execution
**Payout Status**: Current state of payout (SCHEDULED, PROCESSING, COMPLETED)

## Strategic Context

### Supporting Domain
Merchant Account Management is a **Supporting Domain** as it provides essential account and wallet management capabilities that support the core payment processing business.

### Dependencies
- **Upstream**: Payment Processing (for completed transactions)
- **Downstream**: Financial Recording & Reporting (for settlement)
- **External**: Banking systems, payout processors, merchant onboarding systems

## Integration Patterns

### Event-Driven Integration
- Consumes payment completion events for wallet registration
- Publishes wallet registration events for downstream systems
- Integrates with payout processing systems

### API Integration
- RESTful APIs for merchant account management
- Payout scheduling and management endpoints
- Wallet balance and transaction history APIs

## Business Rules

1. **Wallet Registration**: All completed transactions must be registered in merchant wallets
2. **Payout Scheduling**: Payouts must be scheduled according to merchant agreements
3. **Balance Accuracy**: Wallet balances must always reflect accurate transaction amounts
4. **Settlement Compliance**: All settlements must comply with financial regulations
5. **Data Integrity**: Transaction data must be consistent across all systems

## Wallet Management Model

### Transaction Registration
- Automatic registration of completed transactions
- Real-time balance updates
- Transaction history maintenance
- Audit trail preservation

### Payout Management
- **Scheduled Payouts**: Regular transfers based on merchant agreements
- **Immediate Payouts**: On-demand transfers for eligible merchants
- **Payout Status Tracking**: Real-time status updates
- **Settlement Confirmation**: Verification of successful transfers

### Account Features
- **Balance Tracking**: Real-time wallet balance monitoring
- **Transaction History**: Complete transaction record
- **Payout Scheduling**: Flexible payout timing options
- **Settlement Reporting**: Comprehensive settlement reports

## Success Metrics

- Wallet registration accuracy
- Payout processing time
- Settlement success rate
- Account balance accuracy
- Merchant satisfaction scores 