# Sample Reynolds & Reynolds XML Files

This directory contains fully anonymized sample XML files from Reynolds & Reynolds ERA system, representing the three major data types that the Hendrick Pipeline Engine must process.

## File Overview

All files have been **fully anonymized** with fake but realistic data and are safe for repository storage.

| Data Type | Sample File | Records | Documentation |
|-----------|-------------|---------|---------------|
| **Service Data** | `sample_repair_order_anonymized.xml` | 165 repair orders | [REPAIR_ORDERS_README.md](REPAIR_ORDERS_README.md) |
| **Sales Data** | `sample_fi_deals_anonymized.xml` | 59 F&I deals | [FI_DEALS_README.md](FI_DEALS_README.md) |
| **Inventory Data** | `sample_vehicle_inventory_anonymized.xml` | 394 vehicles | [INVENTORY_README.md](INVENTORY_README.md) |

## Data Types Summary

### 1. Service Repair Orders (`SRO` Task Code)
- **165 repair orders** from single branch (Store 01, Area 01)
- **Customer service data**: Repair work, labor operations, parts usage
- **Key PII**: Customer names, advisor names, technician names, VINs, phone numbers
- **Business value**: Service history, labor rates, parts consumption, warranty work

### 2. F&I Deals (`DH` Task Code) 
- **59 finance deals** from single branch (Store 01, Area 01)
- **Vehicle sales data**: New vehicle sales, trade-ins, financing, warranties
- **Key PII**: Customer demographics, financial data, addresses, employment info
- **Business value**: Sales performance, financing terms, aftermarket sales, customer profiles

### 3. Vehicle Inventory (`VI` Task Code)
- **394 vehicles** from single branch (Store 01, Area 01)
- **Current inventory data**: Available vehicles, pricing, costs, status
- **Key sensitive data**: Dealer costs, margins, internal references, license plates
- **Business value**: Stock levels, pricing strategy, vehicle aging, profitability

## Common XML Structure

All three data types follow the Reynolds & Reynolds STAR standard structure:

```xml
<?xml version="1.0" encoding="utf-8"?>
<rey_HendrickRWB[DataType] xmlns="http://www.starstandards.org/STAR">
  <ApplicationArea>
    <Sender>
      <Component>ERA</Component>
      <Task>[SRO|DH|VI]</Task>
      <DealerNumber>[dealer_id]</DealerNumber>
      <StoreNumber>01</StoreNumber>
      <AreaNumber>01</AreaNumber>
    </Sender>
    <CreationDateTime>[timestamp]</CreationDateTime>
    <BODId>[unique_batch_id]</BODId>
  </ApplicationArea>
  <!-- Data type specific content -->
</rey_HendrickRWB[DataType]>
```

## Branch-Level Organization

All sample files demonstrate the **branch-level organization** critical to Hendrick's operational structure:

```
DealerNumber: [Hendrick Entity ID]
├── StoreNumber: 01 (Individual dealership)
    └── AreaNumber: 01 (Branch within dealership)
```

This structure supports the **branch-level authorization** model where partners are authorized at the AreaNumber (branch) level due to shared accounting areas across multiple dealerships.

## Pipeline Engine Implications

These three data types demonstrate the comprehensive transformation requirements for the Hendrick Pipeline Engine:

### Multi-Output Transformation Patterns

Each data type requires splitting batch files into individual records plus summaries:

**Service Data Output:**
```
processed/
├── repair-orders/store-01/branch-01/{date}/RO-{RoNo}.json
├── daily-summaries/store-01/branch-01/{date}/summary.json
└── indexes/store-01/branch-01/{date}/ro-index.json
```

**Sales Data Output:**
```
processed/
├── fi-deals/store-01/branch-01/{date}/DEAL-{DealNo}.json
├── sales-summaries/store-01/branch-01/{date}/summary.json
└── customer-indexes/store-01/branch-01/{date}/customer-index.json
```

**Inventory Data Output:**
```
processed/
├── inventory/store-01/branch-01/{date}/VEHICLE-{VIN}.json
├── inventory-summaries/store-01/branch-01/{date}/summary.json
└── availability-feeds/store-01/branch-01/{date}/available-vehicles.json
```

### Data Sensitivity Levels

Each data type has different sensitivity requirements:

| Data Type | PII Level | Business Sensitivity | Partner Access |
|-----------|-----------|---------------------|----------------|
| **Service** | High (Customer names, phones) | Medium (Labor rates) | Service partners |
| **Sales** | Very High (Financial, personal) | Medium (Sales margins) | Sales partners |
| **Inventory** | Low (No customer data) | High (Dealer costs) | Public + financial partners |

### Transformation Configuration Examples

The Pipeline Engine requires separate transformation configs for each data type:

```json
{
  "repair_orders": {
    "transformation_id": "repair_order_multi_output",
    "input_pattern": "RRO_*_SRO_*.xml",
    "outputs": ["individual_ros", "daily_summary", "ro_index"]
  },
  "fi_deals": {
    "transformation_id": "fi_deal_multi_output", 
    "input_pattern": "RRO_*_DH_*.xml",
    "outputs": ["individual_deals", "sales_summary", "customer_index"]
  },
  "inventory": {
    "transformation_id": "inventory_multi_output",
    "input_pattern": "RRO_*_VI_*.xml", 
    "outputs": ["individual_vehicles", "inventory_summary", "availability_feed"]
  }
}
```

## Anonymization Summary

### Total Anonymization Results:
- **919 unique names** (customers, staff, managers across all files)
- **649 unique VINs** (vehicles across all data types)
- **1,253 unique ID numbers** (customer IDs, deal numbers, RO numbers, etc.)
- **204 unique addresses** (customer and business addresses)
- **122 unique phone numbers** (customer and business contacts)

### Anonymization Features:
- **Consistent replacement**: Same real data always maps to same fake data across files
- **Relationship preservation**: Customer-vehicle-service relationships maintained
- **Format integrity**: All fake data maintains realistic formats and business logic
- **Complete PII removal**: No real personal, financial, or sensitive business data remains

## Usage

These anonymized files support:

### Development & Testing:
- **Pipeline Engine development**: Testing multi-data-type processing
- **Transformation logic**: Validating individual record extraction and aggregation
- **Branch authorization**: Testing branch-level data filtering
- **Schema validation**: Understanding Reynolds & Reynolds XML structures

### Architecture Design:
- **Multi-output patterns**: Designing efficient partner consumption models
- **Data sensitivity**: Planning encryption and authorization strategies
- **Scaling requirements**: Understanding data volumes and processing needs
- **Partner integration**: Designing API endpoints and data access patterns

### Documentation & Training:
- **Technical specifications**: Reference for transformation configurations
- **Business requirements**: Understanding automotive dealership data flows
- **Security compliance**: Demonstrating PII handling and anonymization capabilities

## File Statistics

| Metric | Service | Sales | Inventory | **Total** |
|--------|---------|-------|-----------|-----------|
| **Records** | 165 | 59 | 394 | **618** |
| **File Size** | 14,369 lines | 7,344 lines | 11,640 lines | **33,353 lines** |
| **Date Range** | May-June 2020 | January 2022 | January 2022 | **Multi-year** |
| **Branches** | 1 | 1 | 1 | **Consistent** |

## Next Steps

1. **Review documentation**: Read detailed README files for each data type
2. **Pipeline development**: Use samples for Hendrick Pipeline Engine implementation
3. **Partner integration**: Design API endpoints based on multi-output patterns
4. **Authorization testing**: Validate branch-level access controls
5. **Performance testing**: Scale processing logic with realistic data volumes

These comprehensive samples provide everything needed to implement the Hendrick Pipeline Engine's multi-data-type processing capabilities while maintaining security, performance, and partner isolation requirements.