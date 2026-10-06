# Retail Demand Forecasting – Big Data Analytics

## 1. Project Overview

This project focuses on **Retail Demand Forecasting** using Big Data technologies and distributed analytics.

The project analyses historical retail demand data to identify demand patterns, understand the effect of business and environmental factors, and build machine learning models for demand forecasting.

The project demonstrates the use of:

- HDFS for distributed data storage
- Hive for data modelling and SQL-based analytics
- Apache Spark / PySpark for distributed processing and analytics
- Spark MLlib for demand forecasting
- HBase for store-level lookup of analytical results
- GitHub for project documentation and reproducibility

The project was completed as a five-member team, with each student responsible for a specific technical component.

---

## 2. Business Problem

Retail businesses need to maintain sufficient inventory to satisfy customer demand while avoiding overstocking.

Demand can vary depending on several factors, including:

- Price
- Discount
- Promotions
- Weather conditions
- Seasonality
- Epidemic conditions
- Store and product characteristics
- Competitor pricing

The objective of this project is to analyse these factors using Big Data technologies and develop a forecasting model that can help understand and predict retail demand.

---

## 3. Project Objectives

The main objectives of the project are:

- Store and process retail data using Big Data technologies.
- Perform data quality checks and cleaning.
- Analyse retail demand across stores, products, regions and time periods.
- Study the relationship between demand and factors such as promotions, discounts, weather and epidemic conditions.
- Perform distributed analytics using Apache Spark.
- Build and compare demand forecasting models using Spark MLlib.
- Store selected analytical results in HBase for lookup.
- Validate the consistency of outputs produced by different project components.
- Consolidate the final results and document the complete project workflow.

---

## 4. Dataset Description

The project uses a retail demand dataset containing **76,000 records and 16 columns**.

### Dataset Columns

| Column | Description |
|---|---|
| date | Date of the observation |
| store_id | Store identifier |
| product_id | Product identifier |
| category | Product category |
| region | Store region |
| inventory_level | Available inventory level |
| units_sold | Number of units sold |
| units_ordered | Number of units ordered |
| price | Product price |
| discount | Discount percentage |
| weather_condition | Weather condition |
| promotion | Promotion indicator |
| competitor_pricing | Competitor pricing |
| seasonality | Seasonal category |
| epidemic | Epidemic indicator |
| demand | Target demand value |

### Dataset Validation

The executed Spark workflow reported:

- Total records: **76,000**
- Total columns: **16**
- Date range: **2022-01-01 to 2024-01-30**
- Null values: **0**
- Full duplicate records: **0**
- Duplicate `(date, store_id, product_id)` keys: **0**
- Negative demand/units: **0**
- Non-positive prices: **0**
- Invalid promotion/epidemic flags: **0**

---

## 5. Technologies Used

| Technology | Purpose |
|---|---|
| HDFS | Distributed storage of raw retail data |
| Apache Hive | Data modelling and SQL analytics |
| Apache Spark | Distributed data processing |
| PySpark | Spark programming using Python |
| Spark MLlib | Machine learning and demand forecasting |
| HBase | Store-level analytical result lookup |
| Docker | Hadoop/Hive/HBase environment setup where applicable |
| Google Colab | Spark execution environment used by Student 3 |
| GitHub | Version control and project documentation |

---

## 6. Big Data Architecture

The logical project architecture is:

```text
                    Retail Demand Dataset
                              |
                              v
                            HDFS
                         Student 1
                              |
                              v
                            Hive
                         Student 2
                              |
                              v
                       Spark / PySpark
                         Student 3
                              |
                 +------------+------------+
                 |                         |
                 v                         v
       Distributed Analytics       MLlib Forecasting
                 |                         |
                 +------------+------------+
                              |
                              v
                    Analytical Results
                              |
                              v
                           HBase
                         Student 4
                              |
                              v
                  Integration & Validation
                         Student 5
                              |
                              v
                 Final Results & Documentation
```

### Important Execution Note

The architecture above represents the **logical end-to-end project workflow**.

The individual components were executed in their respective environments:

- Student 1 worked with Hadoop/HDFS.
- Student 2 used a Docker-based Hadoop/Hive environment.
- Student 3 executed Spark/PySpark in **Google Colab using Spark local mode**.
- Student 4 implemented the HBase lookup layer.
- Student 5 integrated the outputs from the individual stages, validated the hand-offs, consolidated results and prepared the final documentation.

Therefore, the project should not be described as one continuously connected live HDFS → Hive → Spark → HBase cluster.

---

## 7. End-to-End Execution Flow

The overall project workflow is:

```text
Raw Retail Dataset
        |
        v
HDFS Storage
        |
        v
Hive Data Modelling and SQL Analytics
        |
        v
Spark / PySpark Processing
        |
        +----------------------+
        |                      |
        v                      v
Data Cleaning          Feature Engineering
        |                      |
        +----------+-----------+
                   |
                   v
          Distributed Analytics
                   |
                   v
          Spark MLlib Forecasting
                   |
                   v
            Analytical Results
                   |
                   v
                 HBase
                   |
                   v
       Integration and Validation
                   |
                   v
        Final Results and Insights
```

The project uses individual technical contributions that are combined at the integration stage.

---

## 8. Spark / PySpark Processing

Student 3 performed the main Spark/PySpark processing using Google Colab in Spark local mode.

The Spark workflow included:

### Data Loading

The retail CSV dataset was loaded into Spark using an explicit 16-column schema.

### Data Quality Checks

The workflow checked:

- Null values
- Full duplicate records
- Duplicate business keys
- Negative demand and units
- Non-positive prices
- Invalid promotion flags
- Invalid epidemic flags
- Categorical values

### Feature Engineering

Additional features were created, including:

- Year
- Quarter
- Month
- Day of week
- Week of year
- Demand gap
- Price versus competitor price
- Effective price
- Demand lag features
- Rolling demand averages

Lag and rolling features were created using Spark window functions.

### Distributed Analytics

The Spark workflow generated multiple analytical outputs, including:

- Store-level demand summary
- Quarterly demand trends
- Promotion lift
- Epidemic impact
- Discount effect
- Unmet demand
- Top products by region

Spark SQL was also used for additional analytical queries.

---

## 9. Forecasting Models

Spark MLlib was used to compare different forecasting approaches.

The models evaluated were:

| Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Lag-1 Baseline | 51.465 | 39.671 | -0.312 |
| Linear Regression | 32.790 | 25.374 | 0.467 |
| Random Forest | 31.931 | 24.715 | 0.495 |

### Best Model

The **Random Forest** model produced the best performance among the tested models.

Its results were:

- RMSE: **31.931**
- MAE: **24.715**
- R²: **0.495**

The Random Forest model had the lowest RMSE and MAE and the highest R² among the tested models.

---

## 10. Key Analytical Results

### Store-Level Demand

| Store | Region | Total Demand | Average Demand |
|---|---|---:|---:|
| S001 | North | 1,547,573 | 101.81 |
| S002 | South | 1,625,471 | 106.94 |
| S003 | East | 1,618,324 | 106.47 |
| S004 | West | 1,529,651 | 100.63 |
| S005 | North | 1,607,085 | 105.73 |

**Key finding:** S002 in the South recorded the highest total demand at **1,625,471**.

### Demand Patterns

- Highest average-demand quarter: **2023 Q3 – 115.50**
- 2022 Q1 average demand: **112.73**
- Demand was approximately **29–31% higher during promotions** across categories.
- Average demand during epidemic periods: **70.16**
- Average demand without epidemic conditions: **112.86**
- Demand during epidemic periods was approximately **38% lower**.

### Discount Analysis

| Discount | Average Demand |
|---:|---:|
| 0% | 94.75 |
| 5% | 94.94 |
| 10% | 102.77 |
| 15% | 123.58 |
| 20% | 124.07 |
| 25% | 122.97 |

Demand increased with higher discounts up to around 15–20%, after which the gains began to level off.

### Unmet Demand Gap

| Category | Average Demand Gap |
|---|---:|
| Groceries | 18.10 |
| Clothing | 17.98 |
| Electronics | 14.44 |
| Toys | 14.16 |
| Furniture | 9.21 |

Groceries had the highest average unmet-demand gap.

### Weather Analysis

| Weather | Average Demand |
|---|---:|
| Sunny | 115.17 |
| Cloudy | 105.40 |
| Rainy | 95.11 |
| Snowy | 94.05 |

Average demand was highest during Sunny weather conditions.

### Important Interpretation Note

The observed relationships between demand and factors such as promotions, discounts, weather and epidemic conditions are **associations in the analysed data**. They should not be interpreted as proof of causation.

---

## 11. Validation and Testing

Validation was performed at both the data and result levels.

### Dataset Validation

The Spark workflow reported:

- 76,000 total records
- 16 columns
- 0 null values
- 0 full duplicate records
- 0 duplicate `(date, store_id, product_id)` keys
- 0 negative demand/units
- 0 non-positive prices
- 0 invalid promotion/epidemic flags

### Store Summary Validation

The store-level summary generated from the Spark analytical workflow was compared with the store-level records used by the HBase lookup layer.

All five stores matched:

- S001
- S002
- S003
- S004
- S005

The validation confirms consistency between the Spark store-summary output and the HBase lookup records.

This validates the **result hand-off**, rather than claiming that Spark and HBase were directly connected through one live pipeline.

### Forecasting Validation

The forecasting models were evaluated using:

- RMSE
- MAE
- R²

Random Forest produced the best performance among the tested models.

---

## 12. Individual Contributions

### Student 1 – Aisha Rasifa PS

**Contribution: Data Ingestion and HDFS**

- Prepared the raw retail dataset for Big Data processing.
- Ingested the dataset into HDFS.
- Maintained the HDFS storage structure.
- Provided evidence of HDFS ingestion.

### Student 2 – Abina A

**Contribution: Hive and Data Modelling**

- Set up the Docker-based Hadoop/Hive environment.
- Created the Hive database and external table.
- Verified the retail dataset in Hive.
- Performed SQL-based analytical queries.
- Documented Hive data modelling and analytics.

### Student 3 – Akhila Vaidya

**Contribution: Spark / PySpark and Forecasting**

- Implemented Spark/PySpark processing.
- Performed data quality checks.
- Performed feature engineering.
- Implemented distributed analytics.
- Used Spark SQL for analytical queries.
- Built and evaluated forecasting models using Spark MLlib.
- Produced store summaries and forecasting results.
- Executed Spark in Google Colab using local mode.

### Student 4 – Anuska Misra

**Contribution: HBase Advanced Technology**

- Set up and used HBase.
- Created the `retail_store_summary` table.
- Used a store-based row-key structure.
- Loaded store-level analytical results into HBase.
- Demonstrated HBase scan and lookup operations.

### Student 5 – Divyanshi Mishra

**Contribution: Integration, Validation and Documentation**

- Integrated the outputs of the individual Big Data components into a coherent project workflow.
- Documented the logical end-to-end flow from HDFS and Hive through Spark/PySpark and HBase.
- Consolidated the final analytical results.
- Validated the consistency of the Spark store-summary output with the HBase lookup records.
- Checked the forecasting metrics and consolidated model results.
- Prepared the GitHub repository, README and final project documentation .
- Supported final presentation and technical demonstration.

---

## 13. Repository Structure

The project repository is organised as follows:

```text
Retail-Demand-Forecasting-Big-Data/
│
├── data/
│   └── retail_demand.csv
│
├── hdfs/
│   └── Student1_HDFS_Contribution_Report.pdf
│
├── hive/
│   └── Student2_Hive_Contribution_Report.pdf
│
├── spark/
│   ├── Student3_Spark_Contribution_Report.pdf
│   └── retail_spark_analysis.ipynb
│
├── hbase/
│   ├── Student4_HBase_Contribution_Report.md
│   ├── hbase_commands.txt
│   ├── retail_store_summary.tsv
│   └── screenshots/
│
├── results/
│   ├── final_results.md
│   ├── forecasting_results.csv
│   └── store_summary.csv
│
├── documentation/
│   └── Retail_Demand_Forecasting_Final_Documentation.pdf
│
├── docker/
│   └── docker-compose.yml
│
└── presentation/
```

---

## 14. Project Limitations

The following limitations should be considered when interpreting the project:

- The individual Big Data components were executed in different environments.
- Student 3 executed Spark in Google Colab using local Spark mode rather than directly connecting to the HDFS environment.
- Student 2's Hive environment was a separate Docker-based environment.
- The architecture therefore represents a logical end-to-end workflow rather than one continuously connected live cluster.
- The forecasting models were evaluated using the available dataset and selected features.
- The reported relationships between demand and business/environmental factors are observational associations and do not establish causation.
- The project focuses on demonstrating a Big Data analytics workflow and forecasting approach rather than deploying a production retail forecasting system.

---

## 15. Final Outcome

The project successfully demonstrates an end-to-end **Retail Demand Forecasting** workflow using multiple Big Data technologies.

The main outcomes are:

- Retail data was processed using Big Data technologies.
- Data quality and consistency were checked.
- Hive was used for structured data modelling and SQL analytics.
- Spark/PySpark was used for distributed processing and analytical computation.
- Spark MLlib was used to build and compare forecasting models.
- HBase was used as a store-level lookup layer.
- Analytical results were consolidated and validated.
- The Random Forest model achieved the best performance among the tested models with an R² of **0.495** and RMSE of **31.931**.
- The final project documentation and repository provide evidence of the individual contributions and overall workflow.

The project demonstrates how different Big Data components can contribute to a retail analytics pipeline, from data storage and processing to forecasting, result lookup, validation and final documentation.
