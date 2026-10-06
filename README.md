\# Retail Demand Forecasting – Big Data Analytics



\## 1. Project Overview



Retail businesses need to accurately understand and forecast customer demand to support inventory planning, promotions and resource allocation.



This project develops a Big Data analytics workflow for Retail Demand Forecasting using distributed data storage, SQL-based analysis, Spark/PySpark processing, machine learning and HBase-based store-level lookup.



The project analyses a retail demand dataset containing 76,000 records and 16 columns and identifies important demand patterns related to stores, promotions, discounts, weather and epidemic conditions.



\---



\## 2. Business Problem



Retail demand can vary across stores, products, seasons, promotions, discounts and external conditions.



The objective of this project is to analyse historical retail demand data, identify important demand patterns and develop a forecasting model that can support better demand-planning decisions.



\---



\## 3. Project Objectives



The main objectives are:



\- Store and manage the retail dataset using HDFS.

\- Create a structured Hive representation of the dataset.

\- Perform SQL-based exploratory analysis using Hive.

\- Process and analyse the dataset using Spark/PySpark.

\- Perform data-quality checks and feature engineering.

\- Analyse demand patterns using distributed aggregations.

\- Develop and compare demand forecasting models using Spark MLlib.

\- Store store-level summary information in HBase.

\- Validate consistency between major project outputs.

\- Consolidate the results into a final Big Data analytics workflow.



\---



\## 4. Dataset Description



The project uses a retail demand dataset containing:



\- Records: 76,000

\- Columns: 16

\- Date range: 2022-01-01 to 2024-01-30



The dataset contains attributes related to:



\- Date

\- Store ID

\- Product ID

\- Category

\- Region

\- Inventory level

\- Units sold

\- Units ordered

\- Price

\- Discount

\- Weather condition

\- Promotion

\- Competitor pricing

\- Seasonality

\- Epidemic condition

\- Demand



\---



\## 5. Technologies Used



\- Hadoop HDFS – Distributed storage

\- Apache Hive – Data modelling and SQL analytics

\- Apache Spark / PySpark – Distributed data processing and analytics

\- Spark MLlib – Demand forecasting

\- HBase – Store-level summary lookup

\- Docker – Environment support for Hadoop/Hive/HBase components

\- Google Colab – Spark/PySpark execution environment

\- Python – Data processing and machine learning

\- Git / GitHub – Version control and project repository

---



\## 6. Big Data Architecture



The logical project workflow is:



```text

&#x20;                   Retail Demand Dataset

&#x20;                             |

&#x20;                             v

&#x20;                           HDFS

&#x20;                        Student 1

&#x20;                             |

&#x20;                             v

&#x20;                           Hive

&#x20;                        Student 2

&#x20;                             |

&#x20;                             v

&#x20;                      Spark / PySpark

&#x20;                        Student 3

&#x20;                             |

&#x20;                +------------+------------+

&#x20;                |                         |

&#x20;                v                         v

&#x20;      Distributed Analytics       MLlib Forecasting

&#x20;                |                         |

&#x20;                +------------+------------+

&#x20;                             |

&#x20;                             v

&#x20;                   Analytical Results

&#x20;                             |

&#x20;                             v

&#x20;                          HBase

&#x20;                        Student 4

&#x20;                             |

&#x20;                             v

&#x20;                 Integration \& Validation

&#x20;                        Student 5

&#x20;                             |

&#x20;                             v

&#x20;                Final Results \& Documentation



Execution Environment Note



The project components were developed and executed in different environments rather than in one continuously connected live cluster.



In particular, the Spark/PySpark workflow was executed in Google Colab using Spark local mode.



Therefore, the architecture above represents the logical end-to-end project workflow, while the individual technical stages were executed and verified in their respective environments.

---



\## 7. End-to-End Execution Flow



1\. Prepare the source retail dataset.

2\. Upload the raw dataset to HDFS.

3\. Verify HDFS files and directories.

4\. Create the Hive database and external table.

5\. Run Hive SQL queries for initial analysis.

6\. Process the dataset using Spark/PySpark.

7\. Perform data-quality checks and feature engineering.

8\. Perform distributed aggregations and analytical queries.

9\. Generate and store analytical results.

10\. Use HBase for store-level summary lookup.

11\. Validate the project outputs.

12\. Consolidate commands, code and findings into the documentation.

13\. Push project files to GitHub.

14\. Prepare the final presentation and technical demonstration.



\---



\## 8. Spark/PySpark Processing



The Spark workflow included:



\- Explicit schema definition.

\- Dataset loading and schema verification.

\- Record-count and partition checks.

\- Null-value checks.

\- Duplicate-record checks.

\- Duplicate key checks.

\- Validation of numerical values.

\- Validation of promotion and epidemic flags.

\- Date-based feature engineering.

\- Demand-gap calculation.

\- Price-related features.

\- Lag and rolling demand features.

\- Store-level and category-level analytics.

\- Spark SQL queries.

\- MLlib-based forecasting.



\---



\## 9. Forecasting Models



Three approaches were evaluated:



| Model | RMSE | MAE | R² |

|---|---:|---:|---:|

| Lag-1 Baseline | 51.465 | 39.671 | -0.312 |

| Linear Regression | 32.790 | 25.374 | 0.467 |

| Random Forest | 31.931 | 24.715 | 0.495 |



\### Best Performing Model



Random Forest performed best among the tested models.



\- RMSE: 31.931

\- MAE: 24.715

\- R²: 0.495



It achieved the lowest RMSE and MAE and the highest R² among the tested approaches.



\---



\## 10. Key Analytical Results



\### Store-Level Demand



\- S002 (South) recorded the highest total demand: 1,625,471.

\- S002 also recorded the highest average demand: 106.94.



\### Quarterly Demand



\- The highest reported average demand occurred in 2023 Q3, at 115.50.



\### Promotion Analysis



Demand during promotional periods was approximately 29–31% higher across the analysed categories.



\### Epidemic Analysis



\- Average demand during epidemic periods: 70.16

\- Average demand during non-epidemic periods: 112.86

\- Observed difference: approximately 38% lower demand during epidemic records.



\### Discount Analysis



Demand increased as discounts increased up to approximately 15–20%, after which the gains began to level off.



\### Unmet Demand



Groceries recorded the highest average demand gap at 18.10.



\### Weather Analysis



Sunny conditions recorded the highest average observed demand at 115.17.



These findings represent descriptive associations in the analysed dataset and should not be interpreted as proof of causation.





\### BLOCK 3 — Sections 11 to 15



```text

\---



\## 11. Validation and Testing



The following validation checks were performed or reviewed:



\- Total records: 76,000

\- Total columns: 16

\- Null values: 0

\- Full duplicate records: 0

\- Duplicate (date, store\_id, product\_id) keys: 0

\- Negative demand/units: 0

\- Non-positive prices: 0

\- Invalid promotion/epidemic flags: 0

\- Hive record count: 76,000

\- HBase store-summary records: 5

\- Forecasting models compared: 3



\### Cross-Stage Validation



The Spark store-summary output was compared with the corresponding HBase store-summary records.



All five stores — S001, S002, S003, S004 and S005 — matched between the two outputs.



This provided evidence of consistency between the Spark analytical output and the HBase lookup stage.



\---



\## 12. Individual Contributions



\### Student 1 – Aisha Rasifa PS



Contribution: Data ingestion and HDFS storage



\- Prepared and uploaded the raw dataset to HDFS.

\- Worked with HDFS directories and file verification.



\### Student 2 – Abina A



Contribution: Hive data modelling and SQL analytics



\- Created the Hive database and external table.

\- Performed SQL-based analysis of the retail dataset.



\### Student 3 – Akhila Vaidya



Contribution: Spark/PySpark processing, analytics and forecasting



\- Developed the Spark/PySpark workflow.

\- Performed data-quality checks and feature engineering.

\- Performed distributed analytics and Spark SQL analysis.

\- Developed and compared forecasting models using Spark MLlib.



\### Student 4 – Anushka Misra



Contribution: HBase advanced technology



\- Created the store-summary HBase table.

\- Implemented store-level row-key and column-family structure.

\- Performed HBase lookup and verification.



\### Student 5 – Divyanshi



Contribution: Integration, documentation, final results and validation



\- Documented the end-to-end project workflow.

\- Consolidated outputs from the individual technical stages.

\- Reviewed and validated project results.

\- Compared Spark store-summary results with HBase records.

\- Consolidated final analytical findings.

\- Prepared project documentation and README.

\- Supported final presentation and technical demonstration.



\---



\## 13. Repository Structure



```text

Retail-Demand-Forecasting-Big-Data/

|

├── data/

│   └── retail\_demand.csv

|

├── hdfs/

│   └── Student1\_HDFS\_Contribution\_Report.pdf

|

├── hive/

│   └── Student2\_Hive\_Contribution\_Report.pdf

|

├── spark/

│   ├── Student3\_Spark\_Contribution\_Report.pdf

│   └── retail\_spark\_analysis.ipynb

|

├── hbase/

│   ├── Student4\_HBase\_Contribution\_Report.md

│   ├── hbase\_commands.txt

│   ├── retail\_store\_summary.tsv

│   └── screenshots/

|

├── results/

│   ├── final\_results.md

│   ├── forecasting\_results.csv

│   └── store\_summary.csv

|

├── documentation/

│   └── Retail\_Demand\_Forecasting\_Final\_Documentation.pdf

|

├── docker/

│   └── docker-compose.yml

|

├── presentation/

|

└── README.md





\---



\## 14. Project Limitations



The project was developed across multiple execution environments.



The Spark/PySpark workflow was executed in Google Colab using Spark local mode, rather than through a continuously connected Spark cluster reading directly from the team's HDFS instance.



Similarly, the HBase component was implemented separately and its outputs were subsequently reviewed during the integration stage.



Therefore, the documented architecture represents the logical integration of the project components, rather than claiming a single continuously running physical pipeline.



\---



\## 15. Final Outcome



The project successfully demonstrated a Big Data analytics workflow for retail demand forecasting using HDFS, Hive, Spark/PySpark, MLlib and HBase.



The analysis identified important demand patterns and compared multiple forecasting approaches. Random Forest achieved the best performance among the tested models, while cross-stage validation confirmed consistency between the Spark store-summary results and the HBase records.



The project provides a foundation for using historical retail data to support demand analysis, inventory planning and forecasting decisions.

