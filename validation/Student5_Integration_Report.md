\# Student 5 – Integration Report



\## 1. Project



\*\*Project Title:\*\* Retail Demand Forecasting – Big Data Analytics



\*\*Student:\*\* Divyanshi



\*\*Role:\*\* Student 5 – Integration, Validation and Documentation



\---



\## 2. Objective



The objective of the integration activity was to bring together the outputs produced by the individual team members and document them as one coherent Big Data analytics workflow.



Each team member was responsible for a different technical component of the project. Student 5's responsibility was to understand how these components fit together, consolidate their outputs, validate important result hand-offs, and prepare the final project documentation.



\---



\## 3. Team Components



The project was divided into the following technical responsibilities:



| Student | Responsibility | Main Output |

|---|---|---|

| Student 1 – Aisha Rasifa PS | Data Ingestion and HDFS | Retail dataset stored in HDFS |

| Student 2 – Abina A | Hive and Data Modelling | Hive table and SQL analytics |

| Student 3 – Akhila Vaidya | Spark / PySpark and Forecasting | Cleaned data, analytical summaries and forecasting results |

| Student 4 – Anushka Misra | HBase Advanced Technology | HBase store-level lookup table |

| Student 5 – Divyanshi | Integration, Validation and Documentation | Integrated workflow, validated results and final documentation |



\---



\## 4. Logical Integration Architecture



The overall logical flow of the project is:



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

```



This architecture represents the \*\*logical project-level workflow\*\* and shows how the individual technical contributions relate to one another.



\---



\## 5. Integration of Individual Components



\### 5.1 Data Ingestion and HDFS



Student 1 handled the initial data ingestion and HDFS storage stage.



The retail demand dataset was prepared and stored using HDFS as part of the Big Data storage layer.



This stage provided the foundation for subsequent processing and analysis.



\---



\### 5.2 Hive and Data Modelling



Student 2 worked with Hadoop/Hive using a Docker-based environment.



The retail dataset was represented through a Hive external table and SQL queries were used for structured analytics.



The Hive stage provided a structured SQL-based view of the retail data.



\---



\### 5.3 Spark / PySpark Processing



Student 3 performed the main distributed processing and forecasting workflow using PySpark.



The Spark workflow included:



\- Data loading

\- Schema definition

\- Data quality checks

\- Data cleaning

\- Feature engineering

\- Distributed aggregations

\- Spark SQL analysis

\- Forecasting using Spark MLlib



The main outputs relevant to integration included:



```text

results/store\_summary.csv

results/forecasting\_results.csv

results/final\_results.md

```



These outputs provided the analytical results used during the final project consolidation.



\---



\### 5.4 HBase Lookup Layer



Student 4 implemented the HBase component.



The store-level analytical summary was represented in HBase using the `retail\_store\_summary` table.



The HBase records contained store-level fields including:



\- Region

\- Record count

\- Total demand

\- Average demand

\- Average demand gap



Student 5 reviewed these records as part of the integration and validation process.



The HBase implementation itself was performed by Student 4.



\---



\## 6. Student 5 Integration Activity



The Student 5 integration activity consisted of the following steps:



\### Step 1 – Review Individual Outputs



Reviewed the outputs produced by the HDFS, Hive, Spark/PySpark and HBase stages.



\### Step 2 – Identify the Main Result Flow



Mapped the individual technical contributions into a single logical workflow:



```text

Data

&#x20; |

&#x20; v

HDFS

&#x20; |

&#x20; v

Hive

&#x20; |

&#x20; v

Spark / PySpark

&#x20; |

&#x20; v

Analytical Results

&#x20; |

&#x20; v

HBase

&#x20; |

&#x20; v

Validation

&#x20; |

&#x20; v

Final Documentation

```



\### Step 3 – Consolidate Analytical Results



Consolidated the main analytical findings from the Spark workflow, including:



\- Store-level demand

\- Demand trends

\- Promotion effects

\- Epidemic-period demand

\- Discount effects

\- Unmet demand

\- Weather-related demand patterns

\- Forecasting model performance



\### Step 4 – Validate Result Hand-off



Compared the Spark-generated store summary with the corresponding HBase-side store records.



The validation covered:



\- Store ID

\- Region

\- Number of records

\- Total demand

\- Average demand

\- Average demand gap



All five stores matched across the checked fields.



Detailed evidence is documented in:



```text

validation/Student5\_Validation\_Report.md

```



\### Step 5 – Prepare Final Documentation



The integrated workflow, analytical results, validation findings and individual contributions were consolidated into the final project documentation and README.



\---



\## 7. Integrated Analytical Results



The major results consolidated during the integration stage included:



\### Store-Level Result



S002 recorded the highest total demand:



```text

Store: S002

Region: South

Total Demand: 1,625,471

Average Demand: 106.94

```



\### Demand Pattern



The highest average-demand quarter reported by the Spark analysis was:



```text

2023 Q3

Average Demand: 115.50

```



\### Promotion Analysis



Demand was approximately \*\*29–31% higher during promotions\*\* across categories in the analysed data.



\### Epidemic Analysis



Average demand was:



```text

During epidemic periods: 70.16

Without epidemic conditions: 112.86

```



This corresponds to an approximately \*\*38% lower average demand\*\* during epidemic periods.



\### Discount Analysis



Demand increased with higher discounts up to approximately 15–20%, after which the gains began to level off.



\### Unmet Demand



Groceries had the highest average demand gap at:



```text

18.10

```



\### Weather Analysis



Sunny weather had the highest average demand:



```text

115.17

```



\### Forecasting



The Random Forest model produced the best performance among the tested models:



```text

RMSE: 31.931

MAE: 24.715

R²: 0.495

```



\---



\## 8. Integration Validation



The store-level results were compared between the Spark analytical output and the HBase-side data.



| Store | Spark Output | HBase Data | Result |

|---|---:|---:|---|

| S001 | Matching | Matching | PASS |

| S002 | Matching | Matching | PASS |

| S003 | Matching | Matching | PASS |

| S004 | Matching | Matching | PASS |

| S005 | Matching | Matching | PASS |



All five stores matched across the six checked fields.



Therefore, the store-level result hand-off was considered successfully validated.



\---



\## 9. Execution Environment Note



The individual components were not executed as one continuously connected live Big Data cluster.



The actual execution environments were:



\- Student 1: Hadoop/HDFS environment

\- Student 2: Docker-based Hadoop/Hive environment

\- Student 3: Google Colab using Spark local mode

\- Student 4: HBase environment

\- Student 5: Cross-stage integration, result comparison, validation and documentation



Therefore, the integration described in this report refers to \*\*integration of the individual project outputs and logical workflow\*\*, rather than the implementation of a single live HDFS-to-Hive-to-Spark-to-HBase pipeline.



\---



\## 10. Student 5 Contribution



My contribution as Student 5 was focused on:



\- Understanding the outputs produced by each technical stage.

\- Mapping the individual components into a coherent project workflow.

\- Consolidating the final analytical results.

\- Comparing Spark analytical results with HBase-side records.

\- Validating the store-level result hand-off.

\- Documenting the integration process.

\- Preparing the final README.

\- Preparing the final project documentation.

\- Supporting the final presentation and technical demonstration.



I did not implement the HBase component. HBase was implemented by Student 4.



\---



\## 11. Evidence



The following project files provide supporting evidence for the integration activity:



```text

results/store\_summary.csv

results/forecasting\_results.csv

results/final\_results.md

hbase/retail\_store\_summary.tsv

validation/Student5\_Validation\_Report.md

README.md

```



The individual contribution reports are also available in the project repository.



\---



\## 12. Challenges and Handling



\### Challenge 1 – Different Execution Environments



The project components were executed in different environments.



\*\*Handling:\*\*



The integration was treated as a project-level logical workflow, with the outputs from each stage reviewed and consolidated rather than claiming a continuously connected live pipeline.



\### Challenge 2 – Combining Results from Different Stages



Different team members produced different outputs for storage, SQL analytics, Spark processing, forecasting and HBase lookup.



\*\*Handling:\*\*



The main analytical outputs were identified and consolidated into the final results and documentation.



\### Challenge 3 – Ensuring Result Consistency



The store-level summary needed to be checked across the Spark and HBase stages.



\*\*Handling:\*\*



The store-level records for S001–S005 were compared across the two outputs. All five records matched across the six checked fields.



\---



\## 13. Final Integration Status



| Integration Area | Status |

|---|---|

| HDFS contribution reviewed | Completed |

| Hive contribution reviewed | Completed |

| Spark/PySpark contribution reviewed | Completed |

| Forecasting results consolidated | Completed |

| HBase output reviewed | Completed |

| Store-level result validation | PASS |

| Final analytical results consolidated | Completed |

| README prepared | Completed |

| Final documentation prepared | Completed |



\### Overall Status



\*\*INTEGRATION COMPLETED\*\*



\---



\## 14. Conclusion



The Student 5 integration activity brought together the individual technical contributions of the project into a coherent Big Data analytics workflow.



The analytical results produced by the Spark stage were consolidated with the outputs of the other project components, and the store-level results were validated against the HBase lookup data.



All five stores matched across the checked fields.



The final integrated project therefore provides a documented workflow covering data storage, data modelling, distributed processing, analytics, forecasting, result lookup, validation and final documentation.



\*\*Final Integration Status: COMPLETED\*\*



