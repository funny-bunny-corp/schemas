# Schemas

Welcome to our JSON Schema Repository for Payment Gateway Integration! This repository is dedicated to providing robust and comprehensive JSON schemas designed to streamline and standardize the integration of payment gateway systems in various applications. Our schemas are crafted to cater to a wide range of payment processing needs, including transaction handling, payment methods, customer details, and refund processes.

The purpose of these schemas is to offer developers a reliable and consistent structure for payment data, ensuring seamless interoperability between different systems and components in the e-commerce and online transaction space. Whether you're building a new e-commerce platform, integrating a payment gateway into an existing system, or developing tools for financial transactions, these schemas are designed to simplify your development process and enhance data integrity.

Our repository is community-driven and open to contributions. We encourage collaboration and feedback to continuously improve and update the schemas in line with the latest industry standards and practices. Let's work together to make online payment processing easier, safer, and more efficient for everyone.

## Schema Structure and Organization

### Domain-Driven Design
Our schemas are organized by bounded contexts, following Domain-Driven Design principles:

- **Payment Processing**: Core payment lifecycle events (creation, processing, completion)
- **Fraud Detection**: Risk assessment and decision-making events
- **Merchant Account Management**: Merchant and account-related events
- **Financial Recording**: Accounting and financial reporting events
- **Refund Management**: Refund request and processing events

### Schema Validation
All schemas follow JSON Schema Draft 2020-12 specification and include:
- Comprehensive field descriptions
- Data type validation
- Format constraints (UUID, date-time, regex patterns)
- Required field specifications
- Real-world examples

### Common Data Types
Our schemas use standardized data types across all domains:
- **UUIDs**: For unique identifiers (`format: "uuid"`)
- **Monetary amounts**: Decimal strings with pattern `^\\d+\\.\\d{2}$`
- **Currency codes**: ISO 4217 three-letter codes (`^[A-Z]{3}$`)
- **Timestamps**: ISO 8601 date-time format
- **Document numbers**: Brazilian CPF pattern for buyer identification

## Usage Guide

### Integration Steps
1. **Choose your domain**: Select the appropriate bounded context for your use case
2. **Review the schema**: Understand the required and optional fields
3. **Validate your data**: Use the JSON Schema for client-side validation
4. **Check examples**: Reference the sample files for implementation guidance
5. **Implement CloudEvents**: Use the provided CloudEvent types for event publishing

### Best Practices
- Always validate data against the schema before processing
- Use idempotency keys to prevent duplicate processing
- Include proper error handling for schema validation failures
- Follow the CloudEvents specification for event structure
- Use the provided examples as templates for your implementations

## Cloud Events

For our ecosystem we are using Cloud Events in Binary Mode. The Cloud Events specification can be found [here](https://github.com/cloudevents/spec/blob/main/cloudevents/spec.md)

| Bounded Context     | Json Schema                                                                                                       | CloudEvent type                                                                  | Sample                                                                                                            |
|---------------------|-------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Payment Processing  | [paymentCreated](payment-processing/payment-processing.v1.payment-created.json)                                     | funny-bunny.xyz.payment-processing.v1.payment.created                               | [Payment Created](cloud-events-samples/payment-processing/payment-processing.v1.payment-created.json)               |
| Payment Processing  | [sellerRequestedPaymentDataProduct](payment-processing/payment-processing.v1.sellers-orders.json)                   | funny-bunny.xyz.payment-processing.v1.data.product.sellers-requested-payments-total | [Sellers Orders](samples/payment-processing/sellers-orders-example.json) |
| Payment Processing  | [refundCreated](payment-processing/payment-processing.v1.refund-created.json)                                       | funny-bunny.xyz.payment-processing.v1.refund.created                                | [Refund Created](samples/payment-processing/refund-created-example.json)                 |
| Payment Processing  | [refundStarted](payment-processing/payment-processing.v1.refund-started.json)                                       | funny-bunny.xyz.payment-processing.v1.refund.started                                | [Refund Started](samples/payment-processing/refund-started-example.json)                 |
| Payment Processing  | [paymentOrderDeclined](payment-processing/payment-processing.v1.transaction-declined.json)                          | funny-bunny.xyz.payment-processing.v1.payment-order.declined                        | [Transaction Declined](samples/payment-processing/transaction-declined-example.json)                                                                                                         |
| Payment Processing  | [paymentOrderStarted](payment-processing/payment-processing.v1.payment-order-started.json)                          | funny-bunny.xyz.payment-processing.v1.payment-order.started                         | [Payment Order Started](samples/payment-processing/payment-order-started-example.json)   |
| Payment Processing  | [paymentOrderApproved](payment-processing/payment-processing.v1.transaction-approved.json)                          | funny-bunny.xyz.payment-processing.v1.payment-order.approved                        | [Transaction Approved](samples/payment-processing/transaction-approved-example.json)   |
| Payment Processing  | [paymentDone](payment-processing/payment-processing.v1.payment-done.json)                                           | funny-bunny.xyz.payment-processing.v1.payment.done                                  | [Payment Done](samples/payment-processing/payment-done-example.json)                                                                                                            |
| Merchant Account    | [transactionWalletRegistered](merchant-account-management/merchant-account-management.v1.transaction-wallet-registered.json) | funny-bunny.xyz.merchant-account.v1.transaction.registered                          | [Transaction Wallet Registered](samples/merchant-account-management/transaction-wallet-registered-example.json)                                                                                                         |
| Financial Recording | [transactionBooked](financial-recording-reporting/financial-recording-reporting.v1.transaction-booked.json)          | funny-bunny.xyz.financial-reporting.v1.transaction.booked                           | [Transaction Booked](samples/financial-recording-reporting/transaction-booked-example.json)                                                                                                         |
| Fraud Detection     | [riskDecisionApproved](fraud-detection/fraud-detection.v1.risk-decision-approved.json)                              | funny-bunny.xyz.fraud-detection.v1.risk-decision.approved                          | [Risk Decision Approved](samples/fraud-detection/risk-decision-approved-example.json)                                                                                                         |
| Fraud Detection     | [riskDecisionRejected](fraud-detection/fraud-detection.v1.risk-decision-rejected.json)                              | funny-bunny.xyz.fraud-detection.v1.risk-decision.rejected                          | [Risk Decision Rejected](samples/fraud-detection/risk-decision-rejected-example.json)                                                                                                         |
| Fraud Detection     | [transactionScorecardCreated](fraud-detection/fraud-detection.v1.transaction-scorecard-created.json)                | funny-bunny.xyz.fraud-detection.v1.transaction-scorecard.created                   | [Transaction Scorecard Created](samples/fraud-detection/transaction-scorecard-created-example.json)                                                                                                         |
| Refund Management   | [refundRequest](refund-management/refund-management.v1.refund-request.json)                                          | funny-bunny.xyz.refund-management.v1.refund.request                                | [Refund Request](samples/refund-management/refund-request-example.json)                                                                                                         |

## Apache Pinot Integration

This repository also includes Apache Pinot table and schema definitions for real-time analytics:

### Analytics Tables
- **Fraud Detection Analytics**: Real-time risk assessment metrics and decision tracking
- **Payment Processing Analytics**: Transaction flow analysis and performance metrics
- **Merchant Account Analytics**: Account activity and transaction volume tracking

The Pinot schemas are located in the `apache-pinot/` directory and are designed to work with the CloudEvents data structure for seamless analytics integration.

## Repository Structure

```
schemas/
├── payment-processing/          # Payment lifecycle schemas
├── fraud-detection/            # Risk assessment schemas
├── merchant-account-management/ # Account management schemas
├── financial-recording-reporting/ # Financial reporting schemas
├── refund-management/          # Refund processing schemas
├── samples/                    # Example JSON files for each schema
├── apache-pinot/              # Analytics table definitions
└── cloud-events-samples/      # CloudEvents format examples
```

## Contributing

We welcome contributions to improve and extend these schemas. Please ensure:
1. All schemas follow JSON Schema Draft 2020-12 specification
2. Include comprehensive descriptions for all fields
3. Provide example files for new schemas
4. Update the README documentation
5. Test schema validation before submitting

