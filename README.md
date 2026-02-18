# Vendor Performance Analysis

## Problem Statement

A multi-location liquor store chain needs to optimize vendor relationships across its stores. The analysis aims to:
- **Evaluate vendor performance** based on profitability, delivery reliability, and sales volume
- **Identify pricing opportunities** through vendor comparison and margin analysis
- **Improve cash flow** by analyzing payment cycles and freight costs
- **Maximize profitability** through data-driven product mix decisions

This analysis will help procurement and operations teams make informed decisions about vendor contracts, inventory policies, and pricing strategies.

## Business Questions to Answer

### Vendor Performance
1. Which vendors provide the best profit margins?
2. Which vendors have the most reliable delivery times?
3. Which vendors generate the highest sales volume?
4. What are the payment terms and freight costs by vendor?
5. Which vendors should we prioritize for negotiations?


### Profitability
6. Which products have the highest profit margins?
7. Which product categories (spirits vs. wine) are most profitable?
8. What are the seasonal sales trends?
9. Which stores are most/least profitable?

## Tech Stack

- **Python 3.x** - Data processing and analysis
- **SQLite** - Relational database for data storage
- **Pandas** - Data manipulation and aggregation
- **Matplotlib/Seaborn** - Data visualization
- **Jupyter Notebook** - Interactive analysis
- **Logging** - Audit trail and error tracking

## Project Structure

```
Project1/
│
├── BUSINESS_PROBLEM.md              # Detailed business problem document
├── README.md                        # This file
├── requirements.txt                 # Python dependencies
│
├── data/
│   ├── raw/                        # Original CSV files
│   │   ├── begin_inventory.csv
│   │   ├── end_inventory.csv
│   │   ├── purchases.csv
│   │   ├── sales.csv
│   │   ├── purchase_prices.csv
│   │   └── vendor_invoice.csv
│   │
│   └── processed/
│       └── liquor_store.db         # SQLite database
│
├── notebooks/
│   ├── 01_data_exploration.ipynb   # Initial data exploration
│   ├── 02_vendor_analysis.ipynb    # Vendor performance analysis
│   ├── 03_inventory_analysis.ipynb # Inventory optimization
│   └── 04_profitability_analysis.ipynb # Profit & trend analysis
│
├── src/
│   ├── __init__.py
│   ├── config.py                   # Configuration settings
│   ├── logger.py                   # Logging setup
│   ├── data_loader.py              # Load CSV files
│   ├── database_setup.py           # Create SQLite database
│   ├── sql_queries.py              # SQL query templates
│   ├── vendor_analysis.py          # Vendor metrics calculation
│   ├── inventory_analysis.py       # Inventory metrics calculation
│   └── visualization.py            # Chart generation
│
├── sql/
│   ├── create_tables.sql           # DDL statements
│   ├── vendor_queries.sql          # Vendor analysis queries
│   ├── inventory_queries.sql       # Inventory analysis queries
│   └── profitability_queries.sql   # Profit analysis queries
│
├── reports/
│   ├── figures/                    # Generated charts
│   └── vendor_performance_report.pdf
│
├── logs/
│   └── analysis.log                # Application logs
│
└── main.py                         # Main execution script
```

## Dataset Schema

### Tables in SQLite Database

**1. begin_inventory**
- InventoryId (PRIMARY KEY)
- Store
- City
- Brand
- Description
- Size
- onHand
- Price
- startDate

**2. end_inventory**
- InventoryId (PRIMARY KEY)
- Store
- City
- Brand
- Description
- Size
- onHand
- Price
- endDate

**3. purchases**
- PurchaseId (PRIMARY KEY)
- InventoryId
- Store
- Brand
- Description
- Size
- VendorNumber (FOREIGN KEY)
- VendorName
- PONumber
- PODate
- ReceivingDate
- InvoiceDate
- PayDate
- PurchasePrice
- Quantity
- Dollars
- Classification

**4. sales**
- SaleId (PRIMARY KEY)
- InventoryId
- Store
- Brand
- Description
- Size
- SalesQuantity
- SalesDollars
- SalesPrice
- SalesDate
- Volume
- Classification
- ExciseTax
- VendorNo (FOREIGN KEY)
- VendorName

**5. purchase_prices**
- Brand (PRIMARY KEY)
- Description
- Price
- Size
- Volume
- Classification
- PurchasePrice
- VendorNumber (FOREIGN KEY)
- VendorName

**6. vendor_invoice**
- InvoiceId (PRIMARY KEY)
- VendorNumber (FOREIGN KEY)
- VendorName
- InvoiceDate
- PONumber
- PODate
- PayDate
- Quantity
- Dollars
- Freight
- Approval

**7. vendors (Derived)**
- VendorNumber (PRIMARY KEY)
- VendorName
- TotalPurchases
- TotalSales
- AvgDeliveryDays
- AvgPaymentDays
- TotalFreight

## Key Performance Indicators (KPIs)

### Vendor Metrics
1. **Profit Margin by Vendor** = (Avg Sales Price - Avg Purchase Price) / Avg Sales Price × 100
2. **Delivery Performance** = Avg(ReceivingDate - PODate)
3. **Payment Cycle** = Avg(PayDate - InvoiceDate)
4. **Freight Cost %** = Total Freight / Total Purchase Dollars × 100
5. **Sales Volume** = Total Sales Dollars by Vendor


### Profitability Metrics
6. **Gross Margin** = (Sales - COGS) / Sales × 100
7. **GMROI** = Gross Margin / Average Inventory Cost
8. **Sales per Square Foot** = Total Sales / Store Size (if available)
9. **Category Mix** = Category Sales / Total Sales × 100

## Implementation Steps

### Phase 1: Environment Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create directory structure
python src/setup_project.py
```

### Phase 2: Data Loading & Database Setup
```bash
# Load CSV files and create SQLite database
python src/database_setup.py

# Verify data integrity
python src/data_loader.py --validate
```

### Phase 3: Analysis Execution
```bash
# Run complete analysis pipeline
python main.py

# Or run individual analyses
python src/vendor_analysis.py
python src/inventory_analysis.py
```

### Phase 4: Interactive Analysis
```bash
# Launch Jupyter notebook
jupyter notebook notebooks/
```

### Phase 5: Generate Reports
```bash
# Generate all reports and visualizations
python src/generate_reports.py
```



## Logging Configuration

All operations are logged with timestamps and severity levels:
- **INFO**: Normal operations (data loading, query execution)
- **WARNING**: Data quality issues (missing values, outliers)
- **ERROR**: Processing failures (database errors, file not found)
- **DEBUG**: Detailed execution information

Log file location: `logs/analysis.log`

## Expected Outcomes

1. **Vendor Scorecard Dashboard**
   - Top 10 vendors by profitability
   - Vendor delivery performance metrics
   - Payment cycle analysis

2. **Profitability Analysis**
   - Product margin analysis
   - Category performance comparison
   - Seasonal trend identification

3. **Strategic Recommendations**
   - Vendor consolidation opportunities
   - Pricing optimization strategies
   - Inventory policy improvements

## Future Enhancements

- Real-time dashboard using Streamlit
- Predictive analytics for demand forecasting
- Automated reorder point calculations
- Vendor performance alerts
- Integration with POS systems
- Machine learning for price optimization

## Dependencies

```
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
sqlite3 (built-in)
jupyter>=1.0.0
openpyxl>=3.1.0
python-dateutil>=2.8.0
```


