# Create-a-medallion-architecture-in-a-Microsoft-Fabric-lakehouse

# Microsoft Fabric Lakehouse - Medallion Architecture Demo

This project demonstrates how to implement a Medallion Architecture using Microsoft Fabric Lakehouse and Notebooks. It is structured to follow best practices for modern data engineering by processing data in three layers: **Bronze**, **Silver**, and **Gold**.

## 🚀 Overview

You will build a complete medallion architecture in Microsoft Fabric, transforming raw CSV files into structured Delta tables for analytics. The process includes data ingestion, transformation, and modeling into a star schema, all inside a Lakehouse environment.

### Architecture Layers

- **Bronze**: Raw data ingestion (CSV files)
- **Silver**: Cleaned and validated Delta tables
- **Gold**: Star schema with dimension and fact tables for reporting

## 🧰 Technologies Used

- Microsoft Fabric (Lakehouse, Notebooks, SQL Endpoint)
- PySpark
- Delta Lake
- Power BI Semantic Model

## 📂 Project Structure

```plaintext
/bronze
    - 2019.csv
    - 2020.csv
    - 2021.csv

/silver
    - sales_silver (Delta table)

/gold
    - dimDate_gold
    - dimCustomer_gold
    - factSales_gold
```

## 📋 Steps

1. **Create Workspace**  
   Start by creating a Microsoft Fabric workspace with trial or premium capacity.

2. **Create Lakehouse**  
   Create a new Lakehouse named `Sales`.

3. **Upload Data**  
   Download and upload `2019.csv`, `2020.csv`, and `2021.csv` to the `bronze` folder.

4. **Transform to Silver Layer**  
   Use PySpark notebooks to load, clean, and enrich the data, saving it as a Delta table in the `silver` layer.

5. **Explore with SQL**  
   Use SQL Analytics Endpoint to query and analyze data in the `sales_silver` table.

6. **Transform to Gold Layer**  
   Create dimensional and fact tables (e.g., `dimDate_gold`, `dimCustomer_gold`) from silver data.

7. **Create Semantic Model**  
   Enable Data Model Editing and relate gold tables for Power BI analysis.

## 📈 Example Queries

```sql
-- Total sales by year
SELECT YEAR(OrderDate) AS Year,
       CAST(SUM(Quantity * (UnitPrice + Tax)) AS DECIMAL(12, 2)) AS TotalSales
FROM sales_silver
GROUP BY YEAR(OrderDate)
ORDER BY Year

-- Top 10 customers by quantity
SELECT TOP 10 CustomerName, SUM(Quantity) AS TotalQuantity
FROM sales_silver
GROUP BY CustomerName
ORDER BY TotalQuantity DESC
```

## 🧼 Clean Up

Don’t forget to delete your workspace and all associated resources when finished to avoid unnecessary charges if using a paid capacity.

## 📎 Resources

- [Microsoft Fabric Documentation](https://learn.microsoft.com/fabric)
- [Delta Lake Documentation](https://delta.io/)
- [Official GitHub Sample Data](https://github.com/MicrosoftLearning/dp-data)

---

**Author**: *Your Name*  
**License**: MIT
