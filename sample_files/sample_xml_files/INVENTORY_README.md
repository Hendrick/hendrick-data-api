# Sample Reynolds & Reynolds Vehicle Inventory XML

## File Status: FULLY ANONYMIZED ✅

**File**: `sample_vehicle_inventory_anonymized.xml`  
**Status**: All 394 vehicle inventory records have been fully anonymized and are safe for repository storage.

## Original File Description

**Original File**: `RRO_D_VI_HendrickRWB_542951325614443__01_01_1_ddd70a46-c37c-4ccb-af4b-f1b119039910.xml`
**Source**: Reynolds & Reynolds ERA system
**Data Type**: Vehicle inventory records (current dealership stock)
**Branch**: Store 01, Area 01 (single branch)
**Date**: January 25, 2022
**File Size**: 11,640 lines

## Data Structure

This XML file demonstrates the structure of vehicle inventory data received from Reynolds & Reynolds:

### XML Schema Information
- **Root Element**: `rey_HendrickRWBVehicleInventory`
- **Task Code**: `VI` (Vehicle Inventory)
- **Record Element**: `<VehInvRec>` (Vehicle Inventory Record)
- **Namespace**: STAR standard (http://www.starstandards.org/STAR)

### Organizational Hierarchy
```
DealerNumber: 542951325614443 (Hendrick entity)
├── StoreNumber: 01 (Individual dealership)
    └── AreaNumber: 01 (Branch within dealership)
```

### Key Components

1. **ApplicationArea** - Metadata about the file
   - Sender information (ERA system)
   - Dealer/Store/Area identification
   - Creation timestamp and BOD ID

2. **VehInvRec** - Individual vehicle inventory records containing:
   - **Vehicle** - Vehicle specifications and details
   - **StockingInfo** - Inventory status and location
   - **MiscInfo** - Purchase info and memo lines
   - **PriceCost** - Pricing and cost information
   - **DlrOption** - Dealer-added options and services
   - **Floorplan** - Financing information (for new vehicles)

### Sample Vehicle Inventory Structure

Each vehicle inventory record (`VehInvRec`) contains:

**Vehicle Information:**
- **Basic Details**: Year, make, model, VIN, color, mileage
- **Technical Specs**: Engine config, transmission, fuel type, body size
- **Classification**: New/Used, vehicle class, trim level
- **Identification**: Stock ID, key numbers, license plates

**Inventory Management:**
- **Status**: IN-STOCK, CO VEH (Company Vehicle), etc.
- **Location**: Physical lot location codes
- **Dates**: Receipt date, purchase date
- **Vehicle Type**: T (Trade), P (Purchase), etc.

**Financial Information:**
- **Pricing**: List price, sales cost, inventory amount
- **Costs**: Purchase cost, reconditioning expenses
- **Margins**: Holdback amounts, pack fees
- **Floorplan**: External inventory financing

**Dealer Options & Services:**
- **New Vehicle Prep**: PDI, accessories, floor mats
- **Reconditioning**: Service work, repairs, detailing
- **Add-ons**: Alarms, extended warranties, protection packages
- **Reference Links**: Connection to service ROs and part orders

## Data Classification

### Business Data (Safe for Partners)
- Vehicle specifications and features
- Inventory status and availability
- Basic pricing information (subject to partner agreements)
- Vehicle history and condition information

### Sensitive Business Data (Restricted)
- **Actual dealer costs and margins**
- **Floorplan financing details**
- **Internal accounting codes and procedures**
- **Specific inventory locations and security information**

### Anonymized Data (Originally Sensitive)
- **VIN Numbers**: Replaced with 1FAKE prefix format
- **License Plates**: Replaced with fake plate numbers
- **Reference Numbers**: Service RO and part order references
- **Stock IDs**: Internal tracking numbers
- **Key Numbers**: Vehicle key identification codes
- **Engine Numbers**: Engine serial numbers
- **Memo Lines**: Internal references and fleet source information

## Anonymization Results

The anonymization script successfully processed:
- **394 unique VINs** (all vehicles replaced with 1FAKE prefix)
- **66 unique license plates** (replaced with ABC1234 format)
- **667 unique reference numbers** (service/parts references anonymized)
- **394 unique stock IDs** (internal tracking numbers replaced)
- **313 unique key numbers** (vehicle key codes anonymized)
- **29 unique engine numbers** (engine serial numbers replaced)

### Sample Anonymized Data:
- **VIN Numbers**: "1FAKE4XT3MEYPK0CH", "1FAKECV9DHPU6E39R"
- **License Plates**: "KHJ4534", "KFW4066", "TKU9125"
- **Reference Numbers**: "RO456789", "567890", "678901"
- **Stock IDs**: "22A4567", "21B8901", "20C2345"
- **Key Numbers**: "000P193", "000R456", "000T789"
- **Engine Numbers**: "K20C2-2018833", "J35Y6-3456789"

### Anonymization Features:
- **Consistent Replacement**: Same real VIN always maps to same fake VIN
- **Format Preservation**: Maintains realistic VIN/license/reference formats
- **Relationship Integrity**: Service references maintain logical connections
- **Complete Coverage**: Processes all 394 vehicles in the file
- **Business Continuity**: Preserves all business logic and relationships

## Pipeline Engine Implications

This vehicle inventory file demonstrates critical considerations for the Hendrick Pipeline Engine:

### Unique Transformation Requirements
- **Real-time Inventory**: Unlike historical transactions (ROs, deals), inventory is current state
- **Frequent Updates**: Inventory changes throughout the day (sales, receipts, status changes)
- **Complex Relationships**: Vehicles connect to service history, options, financing
- **Cost Sensitivity**: Dealer costs and margins require careful partner authorization

### Multi-Output Transformation Patterns
Vehicle inventory should be split into logical business units:

```
processed/
├── inventory/
│   ├── store-01/branch-01/2022/01/25/VEHICLE-1FAKE4XT3MEYPK0CH.json
│   ├── store-01/branch-01/2022/01/25/VEHICLE-1FAKECV9DHPU6E39R.json
│   └── ...
├── inventory-summaries/
│   └── store-01/branch-01/2022/01/25/inventory-summary.json
├── vehicle-indexes/
│   └── store-01/branch-01/2022/01/25/vehicle-index.json
└── availability-feeds/
    └── store-01/branch-01/2022/01/25/available-vehicles.json
```

### Suggested Output Types:
1. **Individual Vehicle JSONs**: Complete vehicle details for specific lookup
2. **Inventory Summary**: Counts by make/model/year, total values, age analysis
3. **Vehicle Index**: Quick lookup table with basic info and availability
4. **Availability Feed**: Public-facing inventory for partner websites
5. **Cost Summary**: Internal financial summary (restricted partners only)

### Partner Authorization Considerations:
- **Public Partners**: Basic vehicle specs, availability, public pricing
- **Dealer Partners**: Full specifications, detailed history, some cost data
- **Financial Partners**: Complete cost structure, margins, floorplan info
- **Service Partners**: Service history, reconditioning details, maintenance needs

## Usage

This anonymized file can be used for:
- **Pipeline Engine Development**: Testing inventory processing and transformation logic
- **Schema Validation**: Understanding Reynolds & Reynolds inventory XML structure
- **Multi-Output Testing**: Validating individual vehicle extraction (394 vehicles)
- **Branch Authorization**: Testing branch-level inventory filtering
- **Real-time Processing**: Testing frequent inventory update scenarios
- **Cost Data Handling**: Testing financial data sensitivity and partner restrictions
- **Documentation**: Reference for inventory transformation configuration examples

## File Statistics

- **Total Vehicles**: 394
- **File Size**: 11,640 lines
- **Mix**: New and used vehicles
- **Single Branch**: All inventory from Store 01, Area 01
- **Vehicle Range**: 2002-2022 model years
- **Brands**: Honda, Chevrolet, Toyota, Jeep, and others
- **Status Types**: IN-STOCK, Company Vehicles, etc.

This sample demonstrates the third major data type (alongside repair orders and F&I deals) that the Hendrick Pipeline Engine must handle. Inventory data requires unique processing patterns for real-time updates, cost sensitivity, and complex partner authorization schemes.

## Key Differences from Other Data Types

| Data Type | Frequency | Purpose | Sensitivity | Partner Access |
|-----------|-----------|---------|-------------|----------------|
| **Repair Orders** | Historical transactions | Service work completed | Customer PII | Service details |
| **F&I Deals** | Historical transactions | Sales completed | Financial/Personal PII | Sales data |
| **Inventory** | Current state/real-time | Available vehicles | Cost/Margin data | Public availability |

The Pipeline Engine architecture must handle these three distinct data types with appropriate transformation logic, update frequencies, and partner authorization levels.