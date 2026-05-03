# 💳 Financial Transactions BI Solution
### Data Warehousing & Business Intelligence | IT3021 | SLIIT

A complete end-to-end Business Intelligence solution built on a Financial Transactions Data Warehouse, demonstrating ETL pipeline design, OLAP cube implementation, multidimensional analysis, and interactive reporting.

---

## 📊 Dataset
- **Source:** CaixaBank Tech Financial Transactions Dataset ([Kaggle](https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets))
- **Size:** 621,435 transaction records
- **Domain:** Financial transactions with fraud detection

---

## 🏗️ Architecture Overview

```
Raw Data (CSV)
     ↓
[SQL Server - FinancialSourceDB]
     ↓  ETL (SSIS)
[SQL Server - FinancialStaging]
     ↓  ETL (SSIS)
[SQL Server - FinancialDW] ← Star Schema Data Warehouse
     ↓
[SSAS - Cube_FinancialDW] ← OLAP Cube
     ↓              ↓
[Excel OLAP]    [Power BI Reports]
```

---

## 🗄️ Data Warehouse Schema (Star Schema)

| Table | Type | Rows | Description |
|-------|------|------|-------------|
| FactTransaction | Fact | 621,435 | Central fact table with transaction measures |
| DimDate | Dimension | 3,652 | Date dimension with hierarchy |
| DimCustomer | Dimension | 2,000 | Customer dimension (SCD Type 2) |
| DimCard | Dimension | 6,146 | Payment card dimension |
| DimMerchant | Dimension | 53,244 | Merchant dimension |
| DimMCC | Dimension | 109 | Merchant Category Code dimension |

---

## 🔧 Technologies Used

| Tool | Purpose |
|------|---------|
| SQL Server 2019 | Database Engine |
| SQL Server 2022 Analysis Services | OLAP Cube (SSAS) |
| Visual Studio 2026 + AS Extension 4.0.0 | Cube Development |
| SSIS (SQL Server Integration Services) | ETL Pipeline |
| Microsoft Excel | OLAP Operations |
| Power BI Desktop + Service | Interactive Reports |

---

## 📁 Repository Structure

```
Financial-Transactions-BI-Solution/
│
├── FinancialDW_ETL/                  # Assignment 1 - ETL Pipeline
│   ├── SSIS packages (.dtsx)         # Data extraction, transformation, load
│   └── ...
│
├── CubeProject_IT23363434/           # Assignment 2 - SSAS Cube
│   ├── Cube_FinancialDW.cube         # Cube definition
│   ├── Dim Date.dim                  # Date dimension
│   ├── Dim Customer.dim              # Customer dimension
│   ├── Dim Card.dim                  # Card dimension
│   ├── Dim Merchant.dim              # Merchant dimension
│   ├── DS_FinancialDW.ds             # Data source
│   └── DSV_FinancialDW.dsv           # Data source view
│
├── Excel_IT23363434.xlsx             # Excel OLAP Operations
├── PowerBIReports_IT23363434.pbix    # Power BI Reports
└── README.md
```

---

## 🔷 Component 1: ETL Pipeline (SSIS)

Built a 3-layer ETL architecture:

- **Extract:** Loaded raw CSV data into `FinancialSourceDB`
- **Transform:** Cleaned and transformed data in `FinancialStaging`
  - Handled null values, data type conversions
  - Applied business rules and data quality checks
- **Load:** Populated star schema in `FinancialDW`
  - Implemented SCD Type 2 for DimCustomer
  - Generated surrogate keys for all dimensions
  - Loaded 621,435 fact records

---

## 🔶 Component 2: SSAS OLAP Cube

Built a multidimensional OLAP cube `Cube_FinancialDW` using SQL Server Analysis Services:

**Dimensions:**
- 📅 **Dim Date** — Date Hierarchy: Year → Quarter → Month → Day
- 👤 **Dim Customer** — Demographics, income, credit score
- 💳 **Dim Card** — Card type, brand, credit limit, security flags
- 🏪 **Dim Merchant** — Location, MCC category

**Measures:**
- Transaction Amount
- Is Fraud (fraud indicator)
- Transaction Processing Time (hours)

**Deployed to:** SQL Server 2022 Analysis Services

---

## 📊 Component 3: Excel OLAP Operations

Connected Excel to the SSAS cube and demonstrated all 5 OLAP operations:

| Operation | Description | Example |
|-----------|-------------|---------|
| **Roll-up** | Aggregate to higher level | Total amount by Year |
| **Drill-down** | Navigate to lower level | Year → Quarter → Month → Day |
| **Slice** | Filter by one dimension | Card Type = Credit only |
| **Dice** | Filter by multiple dimensions | Card Type = Credit AND State = CA |
| **Pivot** | Rotate data perspective | Card Types as column headers |

---

## 📈 Component 4: Power BI Reports

Four interactive reports published to Power BI Service:

### Report 1 — Matrix Visual
- Transaction amounts by Year/Month (rows) vs Card Type (columns)
- Row and column subtotals enabled

### Report 2 — Cascading Slicers
- Slicer 1: Card Type → dynamically filters → Slicer 2: Card Brand
- Multiple visuals: Bar Chart + Pie Chart updating in real-time

### Report 3 — Drill-Down Report
- Column chart with Date Hierarchy
- Navigate: Year → Quarter → Month → Day

### Report 4 — Drill-Through Report
- Main page: Transaction summary by Merchant State
- Right-click → Drill through → Detail page with transaction breakdown

---

## 🚀 How to Run

### Prerequisites
- SQL Server 2019+ with Analysis Services
- Visual Studio 2022+ with Analysis Services Projects extension
- Power BI Desktop
- Microsoft Excel

### Steps
1. Restore `FinancialDW` database from backup
2. Open `CubeProject_IT23363434` in Visual Studio
3. Update connection string in `DS_FinancialDW.ds`
4. Deploy the cube to your SSAS instance
5. Open `Excel_IT23363434.xlsx` and refresh the connection
6. Open `PowerBIReports_IT23363434.pbix` in Power BI Desktop

---

## 📚 Key Concepts Demonstrated

- ✅ Star Schema Data Warehouse design
- ✅ ETL pipeline with SSIS
- ✅ Slowly Changing Dimensions (SCD Type 2)
- ✅ OLAP cube with dimensions, measures and hierarchies
- ✅ Multidimensional expressions (MDX)
- ✅ All 5 OLAP operations (Roll-up, Drill-down, Slice, Dice, Pivot)
- ✅ Power BI data modeling and DAX
- ✅ Interactive dashboard publishing

---

## 👩‍💻 Author

**Hafsa Rifai** | Department of Data Science | Faculty of Computing | SLIIT

---

*This project was completed as part of the IT3021 Data Warehousing and Business Intelligence module at Sri Lanka Institute of Information Technology (SLIIT).*
