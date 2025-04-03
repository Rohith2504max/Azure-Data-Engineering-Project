# Azure-Data-Engineering-Project

# Adventure Works Data Engineering Project

## 🚀 Project Overview
This project demonstrates an **End-to-End Data Engineering Pipeline** using **Azure Data Factory, Azure Data Lake, Azure Databricks (PySpark), and Azure Synapse Analytics**. The goal is to process and analyze data efficiently using best practices in **ETL, data transformation, and data warehousing**.

## 🏗️ Architecture Overview
The project follows the **Bronze-Silver-Gold** data architecture:
- **Bronze Layer**: Raw data ingestion from different sources (CSV files, APIs, etc.).
- **Silver Layer**: Data cleansing, transformations, and schema validation using **PySpark** in Databricks.
- **Gold Layer**: Aggregated, ready-to-use data views stored in **Azure Synapse Analytics** for reporting.

## 🛠️ Tech Stack
- **Azure Data Factory** → For data orchestration
- **Azure Data Lake Storage Gen2** → For data storage
- **Azure Databricks (PySpark)** → For data transformation
- **Azure Synapse Analytics** → For querying and analytics
- **Power BI** → For visualization (Optional)

## 📂 Folder Structure
```
Adventure-Works-Data-Engineering-Project/
│── Data/                       # Raw CSV files (Bronze Layer)
│── Notebooks/                  # Databricks PySpark scripts (Silver Layer)
│── SQL_Scripts/                # SQL Views for Synapse (Gold Layer)
│── README.md                   # Project documentation
```

## 📜 Data Sources
The dataset used in this project includes:
- **Product Categories, Products, and Subcategories**
- **Sales Data (2015-2017)**
- **Customer Information**
- **Calendar and Territories Data**

## 🔧 Setup & Installation
### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/Adventure-Works-Data-Engineering-Project.git
cd Adventure-Works-Data-Engineering-Project
```
### 2️⃣ Upload Data to Azure Data Lake
Upload the CSV files to **Azure Data Lake Gen2** under the `bronze` container.

### 3️⃣ Run Databricks Notebook
1. Open **Azure Databricks**
2. Create a new Notebook and copy the **Silver Layer PySpark script**
3. Run the notebook to transform and save data in the `silver` container

### 4️⃣ Execute SQL Views in Synapse
1. Open **Azure Synapse Analytics**
2. Run the **Gold Layer SQL scripts** to create views for reporting

## 📌 Key Features & Code Highlights
### ✅ PySpark Transformations (Silver Layer)
```python
df_sales = df_sales.withColumn("StockDate",to_timestamp('StockDate'))
df_sales = df_sales.withColumn("OrderNumber",regexp_replace(col('OrderNumber'),'S','T'))
df_sales = df_sales.withColumn('multiply',col('OrderLineItem')*col('OrderQuantity'))
df_sales.write.format('parquet').mode('append').option("path","abfss://silver@storageaccount.dfs.core.windows.net/AdventureWorks_Sales").save()
```
### ✅ SQL Views (Gold Layer in Synapse)
```sql
CREATE VIEW gold.sales AS
SELECT * FROM OPENROWSET(
    BULK 'https://storageaccount.blob.core.windows.net/silver/AdventureWorks_Sales/',
    FORMAT = 'PARQUET'
) AS request1;
```

## 📊 Future Enhancements
- Automate pipelines using **Azure Data Factory**
- Implement **Real-time Data Processing** using Event Hub & Stream Analytics
- Optimize query performance in **Synapse Analytics**

## 💡 Conclusion
This project showcases how to build a **scalable and efficient Data Engineering solution** on **Azure**. It covers **data ingestion, transformation, and warehousing**, making it a great reference for **Azure Data Engineers**. 🚀

---
📌 **Feel free to fork this repo, contribute, or suggest improvements!** 😊

