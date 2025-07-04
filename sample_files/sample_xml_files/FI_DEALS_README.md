# Sample Reynolds & Reynolds F&I Deals XML

## File Status: FULLY ANONYMIZED ✅

**File**: `sample_fi_deals_anonymized.xml`  
**Status**: All 59 F&I deals have been fully anonymized and are safe for repository storage.

## Original File Description

**Original File**: `RRO_D_DH_HendrickRWB_542281322638767__01_01_1_fb9d318b-48be-4cdd-89fd-98c5b1ed9e58.xml`
**Source**: Reynolds & Reynolds ERA system
**Data Type**: Finance & Insurance closed deals (vehicle sales)
**Branch**: Store 01, Area 01 (single branch)
**Date Range**: January 2022
**File Size**: 7,344 lines

## Data Structure

This XML file demonstrates the structure of F&I deal data received from Reynolds & Reynolds:

### XML Schema Information
- **Root Element**: `rey_HendrickRWBFIClosedDeal`
- **Task Code**: `DH` (Deal History/Closed Deal)
- **Namespace**: STAR standard (http://www.starstandards.org/STAR)

### Organizational Hierarchy
```
DealerNumber: 542281322638767 (Hendrick entity)
├── StoreNumber: 01 (Individual dealership)
    └── AreaNumber: 01 (Branch within dealership)
```

### Key Components

1. **ApplicationArea** - Metadata about the file
   - Sender information (ERA system)
   - Dealer/Store/Area identification
   - Creation timestamp and BOD ID

2. **FIDeal** - Container for all F&I deals
   - **FIDealFin** - Individual finance deal data
   - **Buyer** - Customer information and demographics
   - **TransactionVehicle** - New vehicle details
   - **TradeIn** - Trade-in vehicle information
   - **FinanceInfo** - Loan terms and lender details
   - **SalesStaff** - Sales team information
   - **Aftermarket** - Add-on products and services

### Sample F&I Deal Structure

Each F&I deal (`FIDealFin`) contains:

**Vehicle Information:**
- **New Vehicle**: Make, model, year, VIN, MSRP, sale price
- **Trade-In Vehicle**: VIN, year, make, model, trade value, payoff amount

**Customer Information:**
- **Personal**: Name, address, phone, DOB, license number
- **Employment**: Employer name, occupation
- **Financial**: Income, employment details

**Financial Terms:**
- **Loan Details**: Amount financed, APR, term, monthly payment
- **Lender**: Financial institution, address, contact info
- **Incentives**: Rebates, dealer cash, manufacturer incentives

**Sales Information:**
- **Sales Staff**: Salesperson, F&I manager, sales manager
- **Dealership**: Name, address, contact information
- **Aftermarket**: Add-on products, warranties, accessories

## Data Classification

### PII Fields (Require Encryption)
- `FirstName`, `LastName`, `MidName` - Customer and staff names
- `Addr1`, `City`, `Zip` - Customer addresses
- `Num` - Phone numbers
- `LicNum` - Driver's license numbers
- `date` - Birth dates
- `EmployerName` - Employment information

### Financial Fields (Highly Sensitive)
- `AmtFinanced`, `APR`, `MonthlyPayment` - Loan terms
- `DealNo` - Deal identification numbers
- `NameRecId` - Customer record IDs
- Lender information and financial institution details

### Business Fields (Plaintext for Queries)
- `Vin` - Vehicle identification numbers
- `DealerNumber`, `StoreNumber`, `AreaNumber` - Branch identification
- Vehicle specifications and options
- Financial amounts and dates

## Anonymization Results

The anonymization script successfully processed:
- **291 unique names** (customers, sales staff, F&I managers)
- **204 unique addresses** (customer and business addresses)
- **122 unique phone numbers** (home, cell, business, work)
- **80 unique VINs** (new and trade-in vehicles)
- **195 unique IDs/numbers** (deal numbers, stock IDs, name record IDs)

### Sample Anonymized Data:
- **Customer Names**: "ELIZABETH JONES", "ROBERT MOORE", "DANIEL HARRIS"
- **Addresses**: "807 THIRD PL, HIGH POINT", "4641 STATE WAY, RALEIGH"
- **VIN Numbers**: "1FAKEE460RZ16UTR6", "1FAKEVK4PJR55F4NG"
- **Phone Numbers**: "5551234567", "5557890123"
- **Employers**: "BANK OF AMERICA", "DUKE ENERGY", "WELLS FARGO"

### Anonymization Features:
- **Consistent Replacement**: Same real name always maps to same fake name
- **Preserves Relationships**: Customer-salesperson-manager relationships maintained
- **Valid Formats**: Fake data maintains realistic NC addresses, valid phone formats
- **Complete Coverage**: Processes all 59 F&I deals in the file
- **Financial Compliance**: Anonymizes sensitive financial and personal data

## Pipeline Engine Implications

This F&I deals file demonstrates several important considerations for the Hendrick Pipeline Engine:

### Different Transformation Requirements
- **Multi-Entity Relationships**: Customer + co-buyer, trade-in vehicles, lenders
- **Financial Data Sensitivity**: Requires special handling for regulated financial information
- **Complex Data Structure**: More nested and complex than repair orders

### Multi-Output Transformation Patterns
Similar to repair orders, F&I deals should be split into:
- **Individual Deal JSONs**: One JSON per F&I deal
- **Daily Sales Summaries**: Aggregated sales metrics by branch
- **Customer Indexes**: Efficient customer lookup and relationship tracking

### Suggested Output Structure:
```
processed/
├── fi-deals/
│   ├── store-01/branch-01/2022/01/25/DEAL-450123.json
│   ├── store-01/branch-01/2022/01/25/DEAL-450124.json
│   └── ...
├── sales-summaries/
│   └── store-01/branch-01/2022/01/25/summary.json
└── customer-indexes/
    └── store-01/branch-01/2022/01/25/customer-index.json
```

## Usage

This anonymized file can be used for:
- **Pipeline Engine Development**: Testing F&I deal parsing and transformation logic
- **Schema Validation**: Understanding Reynolds & Reynolds F&I deal XML structure
- **Multi-Output Testing**: Validating individual deal extraction (59 deals)
- **Branch Authorization**: Testing branch-level data filtering for sales data
- **Financial Data Handling**: Testing encryption and compliance requirements
- **Documentation**: Reference for F&I deal transformation configuration examples

## File Statistics

- **Total F&I Deals**: 59
- **File Size**: 7,344 lines
- **Date Range**: January 2022 deals
- **Single Branch**: All deals from Store 01, Area 01
- **Vehicle Types**: New vehicle sales with trade-ins
- **Financing**: Mix of retail financing and leasing deals

This sample demonstrates the volume and complexity of F&I deal data that the Hendrick Pipeline Engine must process alongside repair orders, requiring separate transformation configurations for sales vs service data.