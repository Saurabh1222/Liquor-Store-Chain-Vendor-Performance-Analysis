# Business Problem Statement
## Liquor Store Chain - Vendor Performance & Inventory Optimization Analysis

### Executive Summary
A multi-location liquor store chain needs to optimize its vendor relationships and inventory management to maximize profitability, reduce stockouts, and improve operational efficiency. The analysis will evaluate vendor performance, identify pricing opportunities, optimize inventory levels, and provide data-driven recommendations for procurement decisions.

---

## Business Context

The liquor store chain operates multiple locations across different cities, managing thousands of SKUs from numerous vendors. The business faces challenges in:
- Managing relationships with 50+ vendors
- Optimizing inventory levels across multiple stores
- Identifying profitable vs. underperforming products
- Negotiating better pricing with vendors
- Reducing carrying costs and stockouts
- Understanding sales patterns and trends

---

## Key Business Questions

### Vendor Performance Analysis
1. **Which vendors provide the best profit margins?**
   - Compare purchase prices vs. retail prices by vendor
   - Identify vendors with highest markup potential

2. **Which vendors are most reliable for timely deliveries?**
   - Analyze PO date → Receiving date → Invoice date cycles
   - Identify vendors with consistent delivery performance

3. **Which vendors have the highest sales volume?**
   - Total sales dollars by vendor
   - Total units sold by vendor

4. **What is the payment performance by vendor?**
   - Average days to payment (Invoice date → Pay date)
   - Freight costs as percentage of order value

### Inventory Optimization
5. **Which products have high turnover rates?**
   - Compare beginning inventory → sales → ending inventory
   - Identify fast-moving vs. slow-moving products

6. **Which stores have inventory imbalances?**
   - Stockout analysis (products with zero ending inventory)
   - Overstock analysis (high ending inventory with low sales)

7. **What is the inventory carrying cost?**
   - Calculate average inventory value by store
   - Identify dead stock (no sales during period)

### Profitability Analysis
8. **Which product categories are most profitable?**
   - Analyze profit margins by classification (spirits vs. wine)
   - Identify high-margin products

9. **Which vendors offer the best cost efficiency?**
   - Purchase price per unit vs. market average
   - Freight costs comparison

10. **What are the seasonal trends?**
    - Monthly sales patterns
    - Peak purchasing periods

---

## Data Sources

### Available Datasets

1. **begin_inventory.csv**
   - Starting inventory levels (January 1, 2024)
   - Fields: InventoryId, Store, City, Brand, Description, Size, onHand, Price, startDate

2. **end_inventory.csv**
   - Ending inventory levels (December 31, 2024)
   - Fields: InventoryId, Store, City, Brand, Description, Size, onHand, Price, endDate

3. **purchases.csv**
   - All purchase orders throughout the year
   - Fields: InventoryId, Store, Brand, Description, Size, VendorNumber, VendorName, PONumber, PODate, ReceivingDate, InvoiceDate, PayDate, PurchasePrice, Quantity, Dollars, Classification

4. **sales.csv**
   - Daily sales transactions
   - Fields: InventoryId, Store, Brand, Description, Size, SalesQuantity, SalesDollars, SalesPrice, SalesDate, Volume, Classification, ExciseTax, VendorNo, VendorName

5. **purchase_prices.csv**
   - Master pricing list from vendors
   - Fields: Brand, Description, Price, Size, Volume, Classification, PurchasePrice, VendorNumber, VendorName

6. **vendor_invoice.csv**
   - Vendor invoice summary
   - Fields: VendorNumber, VendorName, InvoiceDate, PONumber, PODate, PayDate, Quantity, Dollars, Freight, Approval

---

## Expected Outcomes & Deliverables

### 1. Vendor Performance Scorecard
- Ranking of vendors by profitability, reliability, and volume
- Vendor comparison dashboard
- Recommendations for vendor consolidation or expansion

### 2. Inventory Optimization Report
- Optimal stock levels by product and store
- Reorder point recommendations
- Dead stock identification and clearance strategy

### 3. Profitability Analysis
- Product-level profit margin analysis
- Store-level performance comparison
- Category performance insights

### 4. Operational Metrics Dashboard
- Inventory turnover ratio
- Days inventory outstanding (DIO)
- Gross margin return on investment (GMROI)
- Vendor payment cycle analysis

### 5. Strategic Recommendations
- Vendor negotiation priorities
- Product mix optimization
- Store-specific inventory strategies
- Pricing optimization opportunities

---

## Success Metrics

1. **Vendor Performance**
   - Identify top 20% vendors contributing to 80% of profit
   - Reduce vendor payment cycle by 10%
   - Improve on-time delivery rate to 95%

2. **Inventory Efficiency**
   - Reduce dead stock by 30%
   - Improve inventory turnover ratio by 15%
   - Reduce stockouts by 25%

3. **Profitability**
   - Increase overall gross margin by 5%
   - Identify $100K+ in cost savings opportunities
   - Optimize product mix for 10% revenue growth

---

## Stakeholders

- **Procurement Team**: Vendor negotiations and purchasing decisions
- **Store Managers**: Inventory management and ordering
- **Finance Team**: Payment terms and cash flow optimization
- **Executive Leadership**: Strategic decision-making and vendor relationships
- **Operations Team**: Supply chain and logistics optimization

---

## Project Timeline

- **Week 1**: Data exploration and quality assessment
- **Week 2**: Database design and ETL pipeline development
- **Week 3**: Vendor performance analysis
- **Week 4**: Inventory optimization analysis
- **Week 5**: Profitability and trend analysis
- **Week 6**: Dashboard development and reporting
- **Week 7**: Recommendations and presentation

---

## Technical Approach

- **Python**: Data processing, analysis, and automation
- **SQLite**: Data storage and complex queries
- **Pandas**: Data manipulation and aggregation
- **Matplotlib/Seaborn**: Visualization and reporting
- **Jupyter Notebook**: Interactive analysis and documentation
- **Logging**: Comprehensive audit trail and error tracking
