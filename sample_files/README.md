# Sample Files - Reynolds & Reynolds Data

This directory contains fully anonymized sample files from Reynolds & Reynolds ERA system, representing both XML and CSD data formats that the Hendrick Pipeline Engine must process.

## Directory Structure

```
sample_files/
├── README.md (this file)
├── sample_xml_files/
│   ├── README.md
│   ├── REPAIR_ORDERS_README.md
│   ├── FI_DEALS_README.md
│   ├── INVENTORY_README.md
│   ├── sample_repair_order_anonymized.xml
│   ├── sample_fi_deals_anonymized.xml
│   └── sample_vehicle_inventory_anonymized.xml
└── sample_csd_files/
    ├── README.md
    ├── DAT-WRH-TDSPARTS-ACCTBAL-HOC-06-16-25_13.48.22_anonymized.csv
    ├── DAT-WRH-TDSPARTS-ACCTDETAILS-HOC-06-16-25_13.48.18_anonymized.csv
    ├── DAT-WRH-TDSPARTS-COSTOVERRIDES-HOC-06-16-25_13.48.08_anonymized.csv
    ├── DAT-WRH-TDSPARTS-INVENTORY-HOC-06-16-25_13.47.40_anonymized.csv
    ├── DAT-WRH-TDSPARTS-MOVEMENT-HOC-06-16-25_13.47.49_anonymized.csv
    ├── DAT-WRH-TDSPARTS-PURCHASEORDER-HOC-06-16-25_13.48.13_anonymized.csv
    ├── DAT-WRH-TDSPARTS-SALES-HOC-06-16-25_13.48.02_anonymized.csv
    └── DAT-WRH-TDSPARTS-WIP-HOC-06-16-25_13.47.57_anonymized.csv
```

## Data Format Overview

| Format | Files | Total Records | Description |
|--------|-------|---------------|-------------|
| **XML** | 3 files | 618 records | Service, Sales, and Inventory data |
| **CSD** | 8 files | 103,802 records | Parts management operational data |
| **Total** | **11 files** | **104,420 records** | **Complete dataset** |

## Data Types Summary

### XML Files (STAR Standard Format)
- **Service Data**: 165 repair orders from Reynolds & Reynolds service operations
- **Sales Data**: 59 F&I deals from vehicle sales and financing
- **Inventory Data**: 394 vehicles from current inventory system

### CSD Files (Parts Management System)
- **Account Balance**: 4 financial account balance records
- **Account Details**: 88 detailed account transaction records
- **Cost Overrides**: 91,792 parts cost override records (largest dataset)
- **Inventory**: 3,838 current parts inventory records
- **Movement**: 978 parts movement and transfer records
- **Purchase Order**: 112 purchase order records
- **Sales**: 307 parts sales transaction records
- **WIP**: 6,683 work in progress parts records

## Anonymization Summary

### Complete Anonymization Results:
- **1,348 dealership names** anonymized across XML and CSD files
- **1,137 employee names** anonymized (staff, managers, advisors, technicians)
- **1,905 vendor names** anonymized (suppliers, manufacturers, vendors)
- **1,272 unique ID numbers** anonymized (customer IDs, deal numbers, RO numbers, user IDs)
- **649 unique VINs** anonymized (vehicle identification numbers)
- **204 unique addresses** anonymized (customer and business addresses)
- **122 unique phone numbers** anonymized (customer and business contacts)

### Data Sensitivity Levels:

| Data Category | XML Files | CSD Files | Total Anonymized |
|---------------|-----------|-----------|------------------|
| **Dealership Names** | 919 | 429 | 1,348 |
| **Employee Names** | 919 | 218 | 1,137 |
| **Vendor Names** | 89 | 1,816 | 1,905 |
| **ID Numbers** | 1,253 | 19 | 1,272 |
| **VIN Numbers** | 649 | 0 | 649 |
| **Addresses** | 204 | 0 | 204 |
| **Phone Numbers** | 122 | 0 | 122 |

## Pipeline Engine Processing Requirements

### Multi-Format Processing
The Hendrick Pipeline Engine must handle both XML and CSD formats:

1. **XML Processing**: STAR standard format with nested hierarchical data
2. **CSD Processing**: CSV format with high-volume tabular data
3. **Volume Scaling**: From 618 XML records to 103,802 CSD records
4. **Real-time Requirements**: Parts inventory and WIP data requires near real-time processing

### Transformation Patterns

**XML Multi-Output Processing:**
```
processed/
├── repair-orders/store-{store}/branch-{branch}/{date}/RO-{RoNo}.json
├── fi-deals/store-{store}/branch-{branch}/{date}/DEAL-{DealNo}.json
├── inventory/store-{store}/branch-{branch}/{date}/VEHICLE-{VIN}.json
├── daily-summaries/store-{store}/branch-{branch}/{date}/summary.json
└── indexes/store-{store}/branch-{branch}/{date}/index.json
```

**CSD Multi-Output Processing:**
```
processed/
├── parts-data/
│   ├── inventory/store-{store}/branch-{branch}/{date}/
│   ├── sales/store-{store}/branch-{branch}/{date}/
│   └── wip/store-{store}/branch-{branch}/{date}/
├── financial/
│   ├── account-balances/store-{store}/branch-{branch}/{date}/
│   └── cost-overrides/store-{store}/branch-{branch}/{date}/
└── operational/
    └── movement/store-{store}/branch-{branch}/{date}/
```

### Processing Priorities

| Data Type | Format | Records | Priority | Update Frequency |
|-----------|--------|---------|----------|------------------|
| **Service Orders** | XML | 165 | High | Real-time |
| **Sales Deals** | XML | 59 | High | Real-time |
| **Vehicle Inventory** | XML | 394 | High | Real-time |
| **Parts Inventory** | CSD | 3,838 | High | Real-time |
| **Parts WIP** | CSD | 6,683 | High | Real-time |
| **Parts Sales** | CSD | 307 | High | Real-time |
| **Cost Overrides** | CSD | 91,792 | Medium | Daily |
| **Parts Movement** | CSD | 978 | Medium | Hourly |
| **Purchase Orders** | CSD | 112 | Medium | Daily |
| **Account Details** | CSD | 88 | Low | Daily |
| **Account Balance** | CSD | 4 | Low | Daily |

## Security Requirements

### Data Classification:
- **High Sensitivity**: Customer PII, financial data, employee information
- **Medium Sensitivity**: Business relationships, vendor information, internal IDs
- **Low Sensitivity**: Part numbers, descriptions, non-PII business data

### Encryption Requirements:
- **Field-level encryption**: Customer names, addresses, phone numbers, financial data
- **Partner-specific keys**: Branch-level encryption with partner-specific KMS keys
- **Data-at-rest**: All processed data encrypted in S3
- **Data-in-transit**: All data transfers encrypted with TLS

## Usage

### Development & Testing:
- **Multi-format processing**: Testing XML vs CSD processing differences
- **Volume scaling**: From small XML files to large CSD files (91K+ records)
- **Real-time processing**: Inventory and WIP data processing requirements
- **Branch authorization**: Testing branch-level data filtering and access

### Architecture Design:
- **Processing patterns**: Multi-output transformation for both formats
- **Scalability**: Handling high-volume CSD files efficiently
- **Partner integration**: Designing API endpoints for both data types
- **Security implementation**: Field-level encryption and authorization

### Performance Testing:
- **Throughput**: Processing 104K+ records efficiently
- **Latency**: Real-time processing requirements
- **Concurrency**: Multiple file processing without conflicts
- **Resource utilization**: CPU, memory, and I/O optimization

## Getting Started

1. **Review XML Data**: Start with `sample_xml_files/README.md` for structured data
2. **Review CSD Data**: Continue with `sample_csd_files/README.md` for high-volume data
3. **Pipeline Development**: Use samples for Hendrick Pipeline Engine implementation
4. **Integration Testing**: Validate multi-format processing capabilities
5. **Performance Validation**: Test with realistic data volumes and patterns

These comprehensive samples provide everything needed to implement the Hendrick Pipeline Engine's complete data processing capabilities while maintaining security, performance, and partner isolation requirements across both XML and CSD data formats.