# Sample Reynolds & Reynolds Repair Order XML

## File Status: FULLY ANONYMIZED ✅

**File**: `sample_repair_order_anonymized.xml`  
**Status**: All 165 repair orders have been fully anonymized and are safe for repository storage.

## Original File Description

**Original File**: `RRO_D_RO_HendrickRWB_170161325514576__01_01_1_0053568a-aa0b-4264-8392-c0fd624b906b.xml`
**Source**: Reynolds & Reynolds ERA system  
**Data Type**: Repair order batch file (165 repair orders)
**Branch**: Store 01, Area 01 (single branch)
**Date Range**: May-June 2020
**File Size**: ~1MB (14,369 lines)

## Data Structure

This XML file demonstrates the structure of repair order data received from Reynolds & Reynolds:

### Organizational Hierarchy
```
DealerNumber: 170161325514576 (Hendrick entity)
├── StoreNumber: 01 (Individual dealership)
    └── AreaNumber: 01 (Branch within dealership)
```

### Key Components

1. **ApplicationArea** - Metadata about the file
   - Sender information (ERA system)
   - Dealer/Store/Area identification
   - Creation timestamp and BOD ID

2. **RepairOrder** - Container for all repair orders
   - **RoRecord** - Individual repair order data
   - **Rolabor** - Labor operations and technician details
   - **Ropart** - Parts used in repair operations

### Sample Repair Order Structure

Each repair order (`RoRecord`) contains:
- **Customer Information**: Name, customer number
- **Vehicle Information**: VIN, make/model, mileage
- **Service Advisor**: Name and advisor number
- **Financial Details**: Totals by payment type (customer, warranty, internal)
- **Labor Operations**: Detailed work performed with technician time
- **Parts Information**: Parts used with cost breakdown

## Data Classification

### PII Fields (Require Encryption)
- `CustName` - Customer name
- `AdvName` - Service advisor name
- `TechName` - Technician name
- Phone numbers in comments
- Customer addresses (if present)

### Business Fields (Plaintext for Queries)
- `Vin` - Vehicle identification number
- `RoNo` - Repair order number
- `DealerNumber`, `StoreNumber`, `AreaNumber` - Branch identification
- Part numbers and operation codes
- Financial amounts and dates

## Anonymization Script Available

A comprehensive Python anonymization script (`anonymize_repair_orders.py`) has been created that will:

### PII Data to be Anonymized:
- **Customer Names** → Random fake names (consistent per customer)
- **Advisor Names** → Random fake names (consistent per advisor)  
- **Technician Names** → Random fake names (consistent per technician)
- **VIN Numbers** → Fake VINs with "1FAKE" prefix (17 chars, valid format)
- **Phone Numbers** → 555.xxx.xxxx format
- **Customer Numbers** → 10xxxx format
- **Advisor Numbers** → 20xxxx format
- **Technician Numbers** → 30xxxx format
- **RO Numbers** → 40xxxx format
- **Appointment Numbers** → 50xxxx format

### Anonymization Features:
- **Consistent Replacement**: Same real name always maps to same fake name
- **Preserves Relationships**: Customer-advisor-technician relationships maintained
- **Valid Formats**: Fake data maintains realistic formats and lengths
- **Complete Coverage**: Processes all 165+ repair orders in the file

## Anonymization Results

The anonymization script successfully processed:
- **164 unique names** (customers, advisors, technicians)
- **155 unique VINs** (all replaced with 1FAKE prefix)
- **391 unique ID numbers** (customer, advisor, technician, RO, appointment numbers)

### Sample Anonymized Data:
- **Customer Names**: "CHARLES WILSON", "JANE LISA MOORE", "SUSAN JACKSON"
- **VIN Numbers**: "1FAKE6TXHEPGPWXG9", "1FAKE40VTAJSF17H3"  
- **Phone Numbers**: "555.550.6824", "555.107.4070"
- **ID Numbers**: Customer (10xxxxxx), Advisor (20xxxxxx), Tech (30xxxxxx), RO (40xxxxxx)

## Usage

This anonymized file can be used for:
- **Pipeline Engine Development**: Testing XML parsing and transformation logic
- **Schema Validation**: Understanding Reynolds & Reynolds XML structure
- **Multi-Output Testing**: Validating individual RO extraction (165 records)
- **Branch Authorization**: Testing branch-level data filtering
- **Documentation**: Reference for transformation configuration examples

## File Statistics

- **Total Repair Orders**: 165
- **File Size**: ~1MB
- **Total Lines**: 14,369
- **Date Range**: 2020-05-20 to 2020-06-09
- **Single Branch**: All records from Store 01, Area 01

This sample demonstrates the volume and complexity of data that the Hendrick Pipeline Engine must process efficiently while maintaining branch-level authorization and PII encryption requirements.