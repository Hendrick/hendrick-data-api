# Sample CSD Files - Anonymized Parts Data

This directory contains fully anonymized sample CSD (CSV) files from Reynolds & Reynolds parts management system, representing detailed parts operations and inventory data that the Hendrick Pipeline Engine must process.

## File Overview

All files have been **fully anonymized** with fake but realistic data and are safe for repository storage.

| File Type | Sample File | Records | Description |
|-----------|-------------|---------|-------------|
| **Account Balance** | `DAT-WRH-TDSPARTS-ACCTBAL-HOC-06-16-25_13.48.22_anonymized.csv` | 4 | Financial account balances |
| **Account Details** | `DAT-WRH-TDSPARTS-ACCTDETAILS-HOC-06-16-25_13.48.18_anonymized.csv` | 88 | Detailed account transactions |
| **Cost Overrides** | `DAT-WRH-TDSPARTS-COSTOVERRIDES-HOC-06-16-25_13.48.08_anonymized.csv` | 91,792 | Parts cost override records |
| **Inventory** | `DAT-WRH-TDSPARTS-INVENTORY-HOC-06-16-25_13.47.40_anonymized.csv` | 3,838 | Current parts inventory |
| **Movement** | `DAT-WRH-TDSPARTS-MOVEMENT-HOC-06-16-25_13.47.49_anonymized.csv` | 978 | Parts movement history |
| **Purchase Order** | `DAT-WRH-TDSPARTS-PURCHASEORDER-HOC-06-16-25_13.48.13_anonymized.csv` | 112 | Purchase order data |
| **Sales** | `DAT-WRH-TDSPARTS-SALES-HOC-06-16-25_13.48.02_anonymized.csv` | 307 | Parts sales transactions |
| **WIP** | `DAT-WRH-TDSPARTS-WIP-HOC-06-16-25_13.47.57_anonymized.csv` | 6,683 | Work in progress parts |

## Data Type Summary

### Parts Management System Data
- **103,802 total records** across 8 different operational data types
- **Real-time operational data**: Current inventory levels, sales transactions, purchase orders
- **Financial data**: Account balances, cost overrides, pricing information
- **Workflow data**: Work in progress, parts movement, transaction history

### Business Value
- **Inventory Management**: Real-time parts availability and movement tracking
- **Financial Operations**: Cost management, account reconciliation, pricing strategies
- **Supply Chain**: Purchase order management, vendor relationships, procurement cycles
- **Operations Analytics**: Parts usage patterns, sales performance, workflow optimization

## Common CSD Structure

All CSD files follow a consistent CSV format with quoted fields:

```csv
"FIELD1","FIELD2","FIELD3","FIELD4"
"value1","value2","value3","value4"
```

### Key Fields Across Files:
- **SYS.STBR-NAME**: Store/Branch name (anonymized)
- **PART#**: Honda part numbers (preserved - not sensitive)
- **DESC**: Part descriptions (preserved - not sensitive)
- **Financial Data**: Costs, prices, balances (preserved - business data)
- **Dates**: Transaction dates (preserved - not sensitive)
- **Quantities**: Inventory and transaction quantities (preserved - business data)

## Anonymization Summary

### Comprehensive Data Anonymization Results:
- **429 dealership names** anonymized (e.g., "Honda of Concord" → "Delta Dealer")
- **218 employee names** anonymized (various field names and references)
- **1,816 vendor names** anonymized (supplier and vendor references)
- **19 user IDs** anonymized (system user identifiers)
- **20,009 RO references** anonymized (repair order and transaction references)

### Data Sensitivity Categories:

| Data Type | Sensitivity Level | Anonymization Applied |
|-----------|------------------|----------------------|
| **Dealership Names** | High | Replaced with fake dealer names |
| **Employee Names** | High | Replaced with fake employee names |
| **Vendor Names** | Medium | Replaced with fake vendor names |
| **User IDs** | Medium | Replaced with fake user identifiers |
| **RO References** | Medium | Replaced with fake reference numbers |
| **Part Numbers** | Low | Preserved (not sensitive) |
| **Financial Data** | Low | Preserved (business data, not PII) |
| **Dates** | Low | Preserved (not sensitive) |

### Anonymization Features:
- **Consistent replacement**: Same original data always maps to same fake data
- **Relationship preservation**: Business relationships and data integrity maintained
- **Format integrity**: All fake data maintains realistic formats and business logic
- **Complete PII removal**: No real personal, employee, or sensitive business names remain

## File Details

### 1. Account Balance (4 records)
```csv
"ACCT-NO","ACCT-DESC","BEG-BAL","CUR-BAL","END-BAL"
"1260A","Joy Motors",832199.77,16644.84,848844.61
```
- **Purpose**: Financial account balance tracking
- **Anonymized**: Account descriptions with dealership references

### 2. Account Details (88 records)
```csv
"ACCT-NO","ACCT-DESC","TRANS-DATE","TRANS-AMT","TRANS-TYPE"
```
- **Purpose**: Detailed account transaction history
- **Anonymized**: Account descriptions and transaction references

### 3. Cost Overrides (91,792 records) - **Largest dataset**
```csv
"PART#","OVERRIDE-COST","EFFECTIVE-DATE","USER-ID"
```
- **Purpose**: Parts cost override management
- **Anonymized**: User IDs and system references
- **Note**: Contains majority of data records

### 4. Inventory (3,838 records)
```csv
"SYS.STBR-NAME","PART#","PTS MK NAME","DESC","BASE-COST","QOH"
"Delta Dealer","HP00279-BLK16-01","HONDA","0W16 OE TOYOTA",4.00,28
```
- **Purpose**: Current parts inventory levels
- **Anonymized**: Store names and vendor references
- **Preserved**: Part numbers, descriptions, costs, quantities

### 5. Movement (978 records)
```csv
"PART#","MOVEMENT-TYPE","QUANTITY","DATE","REFERENCE"
```
- **Purpose**: Parts movement and transfer tracking
- **Anonymized**: Reference numbers and user identifiers

### 6. Purchase Order (112 records)
```csv
"PO-NUMBER","VENDOR-NAME","PART#","QUANTITY","COST"
```
- **Purpose**: Purchase order management
- **Anonymized**: Vendor names and PO references

### 7. Sales (307 records)
```csv
"SYS.STBR-NAME","INV#","PART#","DESC","EXT-COST"
"Delta Dealer","463324-1","HP71200-T43-A01","GRILLE ASSY., FR.",114.88
```
- **Purpose**: Parts sales transaction history
- **Anonymized**: Store names and invoice references
- **Preserved**: Part numbers, descriptions, costs

### 8. WIP - Work in Progress (6,683 records)
```csv
"PART#","WIP-STATUS","QUANTITY","DATE","REFERENCE"
```
- **Purpose**: Work in progress parts tracking
- **Anonymized**: Reference numbers and status codes

## Pipeline Engine Implications

### CSD Processing Requirements

The Pipeline Engine must handle CSD files differently from XML files:

1. **High Volume Processing**: 91,792 records in cost overrides file alone
2. **Multiple Data Types**: 8 different operational data types require separate processing
3. **Real-time Data**: Inventory and WIP data requires near real-time processing
4. **Financial Sensitivity**: Cost and pricing data requires secure handling

### Transformation Patterns

**CSD Multi-Output Processing:**
```
processed/
├── parts-data/
│   ├── inventory/store-{store}/branch-{branch}/{date}/
│   ├── sales/store-{store}/branch-{branch}/{date}/
│   ├── purchase-orders/store-{store}/branch-{branch}/{date}/
│   └── wip/store-{store}/branch-{branch}/{date}/
├── financial/
│   ├── account-balances/store-{store}/branch-{branch}/{date}/
│   ├── cost-overrides/store-{store}/branch-{branch}/{date}/
│   └── account-details/store-{store}/branch-{branch}/{date}/
└── operational/
    └── movement/store-{store}/branch-{branch}/{date}/
```

### Processing Considerations

1. **Volume Handling**: Cost overrides file with 91K+ records requires efficient processing
2. **Data Relationships**: Parts data across files must maintain referential integrity
3. **Real-time Requirements**: Inventory and WIP data may require faster processing
4. **Financial Security**: Cost and pricing data requires additional encryption

## Performance Metrics

| File Type | Records | Processing Priority | Update Frequency |
|-----------|---------|-------------------|------------------|
| **Cost Overrides** | 91,792 | Medium | Daily |
| **WIP** | 6,683 | High | Real-time |
| **Inventory** | 3,838 | High | Real-time |
| **Movement** | 978 | Medium | Hourly |
| **Sales** | 307 | High | Real-time |
| **Purchase Order** | 112 | Medium | Daily |
| **Account Details** | 88 | Low | Daily |
| **Account Balance** | 4 | Low | Daily |

## Usage

### Development & Testing:
- **High-volume processing**: Testing with 91K+ record files
- **Multi-format processing**: CSV vs XML processing differences
- **Real-time scenarios**: Inventory and WIP data processing
- **Financial data security**: Cost and pricing data encryption

### Architecture Design:
- **Scalability planning**: Handling large CSD files efficiently
- **Processing prioritization**: Real-time vs batch processing requirements
- **Data relationships**: Maintaining parts data integrity across files
- **Security requirements**: Financial data encryption and access controls

## Next Steps

1. **Pipeline Engine Enhancement**: Implement CSD file processing capabilities
2. **Performance Testing**: Validate processing of 91K+ record files
3. **Real-time Processing**: Design near real-time processing for inventory/WIP data
4. **Financial Security**: Implement additional encryption for cost/pricing data
5. **Integration Testing**: Validate CSD and XML data processing together

These anonymized CSD files provide comprehensive test data for implementing the Hendrick Pipeline Engine's parts management processing capabilities while maintaining security and data integrity requirements.