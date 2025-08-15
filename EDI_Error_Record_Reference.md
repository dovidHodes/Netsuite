# EDI Error Record Structure Reference

## Record Type
- **Internal ID**: `customrecord_edi_error`

## Required Fields
- **Record**: `custrecord_edi_error_record` (Transaction ID - Invoice ID, Sales Order ID, etc.)
- **Action**: `custrecord233` (Set to internal ID 8)
- **Trading Partner**: `custrecord232` (Entity ID)
- **Error Message**: `custrecord234` (Long text field)
- **Status**: `custrecord235` (Set to internal ID 1 - New)

## Optional Fields
- **PO Number**: `custrecord_edi_error_po_number` (Free-form text)

## Usage Example
```javascript
function createEDIErrorRecord(transactionId, errorMessage, tradingPartnerId) {
    const ediErrorRecord = record.create({
        type: 'customrecord_edi_error'
    });
    
    ediErrorRecord.setValue({
        fieldId: 'custrecord_edi_error_record',
        value: transactionId
    });
    
    ediErrorRecord.setValue({
        fieldId: 'custrecord233', // Action field
        value: 8
    });
    
    ediErrorRecord.setValue({
        fieldId: 'custrecord234', // Error Message field
        value: errorMessage
    });

    if (tradingPartnerId) {
        ediErrorRecord.setValue({
            fieldId: 'custrecord232', // Trading Partner field
            value: tradingPartnerId
        });
    }
    
    return ediErrorRecord.save();
}
``` 