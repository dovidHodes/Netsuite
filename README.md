# NetSuite

NetSuite automation scripts and utilities for EDI processing and invoice management.

## Project Structure

```
├── README.md                           # This file
├── NetSuite_Troubleshooting_Memories.md # Lessons learned and troubleshooting guide
├── EDI_Error_Record_Reference.md       # EDI error record structure reference
└── scripts/                            # NetSuite scripts folder
    ├── setInvoiceAsReadyToSend.js      # Auto-approve invoices for EDI transmission
    ├── setIFasReadyToSend.js           # Set Item Fulfillments as ready to send
    └── retrieve_and_attach_PODs.js     # Automated FedEx POD document retrieval and attachment
```

## Scripts

### setInvoiceAsReadyToSend.js
Scheduled script that automatically processes invoices for EDI transmission approval by verifying sibling Item Fulfillment shipping status and applying customer-specific business logic. Failed processing attempts are logged through EDI error records with trading partner identification.

#### Custom Logic
• TP Target (entity 546) invoices have their integration status set to 9 and bypass EDI approval entirely

### setIFasReadyToSend.js
Scheduled script that automatically approves Item Fulfillments for EDI transmission. Processes IFs from a saved search and applies customer-specific logic before setting the EDI approval field.

#### Custom Logic
• Menards (entity 545): Sets ASN status to 16 when PO Type is 'DR'

### retrieve_and_attach_PODs.js
Suitelet for automated FedEx POD (Proof of Delivery) document retrieval and attachment to package records. Processes tracking numbers through the FedEx API to fetch POD documents and automatically attaches them to the corresponding NetSuite package records. Includes comprehensive error handling with EDI error record creation and dynamic account number mapping based on Walmart DC numbers.

#### Custom Logic
• Dynamic date range based on package creation date (start date = creation date, end date = creation date + 1 month)
• Walmart DC number validation (must be exactly 4 digits)
• Account number mapping from Walmart DC number to FedEx account number via custom transaction record
• Comprehensive EDI error record creation with action internal ID 9 for all error scenarios

## Documentation

- **NetSuite_Troubleshooting_Memories.md**: Comprehensive troubleshooting guide with lessons learned from NetSuite development
- **EDI_Error_Record_Reference.md**: Reference for EDI error record structure and usage patterns

## Getting Started

1. Clone this repository
2. Review the troubleshooting memories for common NetSuite development patterns
3. Use the EDI error record reference for consistent error handling
4. Deploy scripts to your NetSuite environment

## Contributing

When adding new scripts or discovering new patterns:
1. Add to the troubleshooting memories file
2. Update relevant documentation
3. Follow established patterns for error handling and logging 