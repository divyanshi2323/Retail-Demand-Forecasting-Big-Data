\# Student 5 – Validation Report



\## 1. Project



\*\*Project Title:\*\* Retail Demand Forecasting – Big Data Analytics



\*\*Student:\*\* Divyanshi



\*\*Role:\*\* Student 5 – Integration, Validation and Documentation



\---



\## 2. Objective



The objective of this validation activity was to verify the consistency of the store-level analytical results produced during the Spark/PySpark processing stage with the corresponding store-level records prepared for the HBase lookup layer.



The validation focused on checking whether the same store-level information was preserved across the two project outputs.



\---



\## 3. Components Compared



The following two outputs were compared:



\### Spark Analytical Output



\*\*File:\*\*



```text

results/store\_summary.csv

```



This file contains the store-level summary generated from the Spark analytical workflow.



\### HBase Lookup Data



\*\*File:\*\*



```text

hbase/retail\_store\_summary.tsv

```



This file contains the store-level summary data used for the HBase lookup layer.



The HBase implementation itself was performed by \*\*Student 4\*\*. The purpose of this activity was to validate the consistency of the outputs as part of the Student 5 integration responsibility.



\---



\## 4. Validation Fields



The following fields were compared for every store:



| Field | Description |

|---|---|

| `store\_id` | Store identifier |

| `region` | Store region |

| `records` | Number of records associated with the store |

| `total\_demand` | Total demand for the store |

| `avg\_demand` | Average demand for the store |

| `avg\_demand\_gap` | Average demand gap for the store |



A record was considered successfully validated when all six fields matched between the Spark output and the HBase-side data.



\---



\## 5. Validation Method



The validation was performed manually by opening the two project outputs and comparing the corresponding records for each store.



The following process was followed:



1\. Opened `results/store\_summary.csv`.

2\. Opened `hbase/retail\_store\_summary.tsv`.

3\. Identified the records for stores S001 to S005.

4\. Compared the `store\_id` and `region`.

5\. Compared the `records` count.

6\. Compared `total\_demand`.

7\. Compared `avg\_demand`.

8\. Compared `avg\_demand\_gap`.

9\. Recorded the validation result for each store.



\---



\## 6. Validation Results



| Store | Region | Records | Total Demand | Avg Demand | Avg Demand Gap | Result |

|---|---|---:|---:|---:|---:|---|

| S001 | North | 15,200 | 1,547,573 | 101.81 | 15.09 | PASS |

| S002 | South | 15,200 | 1,625,471 | 106.94 | 15.75 | PASS |

| S003 | East | 15,200 | 1,618,324 | 106.47 | 15.97 | PASS |

| S004 | West | 15,200 | 1,529,651 | 100.63 | 14.57 | PASS |

| S005 | North | 15,200 | 1,607,085 | 105.73 | 16.07 | PASS |



\---



\## 7. Validation Summary



The comparison produced the following result:



\- Stores checked: \*\*5\*\*

\- Fields checked per store: \*\*6\*\*

\- Total field comparisons: \*\*30\*\*

\- Matching store records: \*\*5\*\*

\- Mismatched store records: \*\*0\*\*

\- Overall validation status: \*\*PASS\*\*



All five stores matched across all six validation fields.



Therefore, the store-level analytical output from the Spark workflow was consistent with the corresponding data used for the HBase lookup layer.



\---



\## 8. Interpretation



The successful comparison demonstrates that the store-level analytical results were transferred consistently between the two project outputs.



In particular:



\- Store identifiers were consistent.

\- Regions were consistent.

\- Record counts were consistent.

\- Total demand values were consistent.

\- Average demand values were consistent.

\- Average demand gap values were consistent.



This provides evidence that the store-summary result hand-off was internally consistent.



\---



\## 9. Important Architecture Note



The project components were executed in their respective environments rather than as one continuously connected live cluster.



The logical project workflow was:



```text

Retail Dataset

&#x20;     |

&#x20;     v

&#x20;    HDFS

&#x20;     |

&#x20;     v

&#x20;   Hive

&#x20;     |

&#x20;     v

Spark / PySpark

&#x20;     |

&#x20;     v

Analytical Results

&#x20;     |

&#x20;     v

&#x20;    HBase

&#x20;     |

&#x20;     v

Integration and Validation

&#x20;     |

&#x20;     v

Final Results

```



Student 5's role was to integrate and validate the outputs of these individual stages.



This validation should therefore be understood as \*\*result hand-off validation\*\*, rather than evidence of a direct live Spark-to-HBase connection.



\---



\## 10. Student 5 Contribution



As Student 5, my contribution to this validation activity was:



\- Identifying the relevant outputs from the Spark and HBase stages.

\- Comparing the store-level results across the two outputs.

\- Checking six fields for each of the five stores.

\- Confirming that all five store records matched.

\- Recording the validation results.

\- Consolidating the findings for the final project documentation.

\- Supporting the integration of the individual technical components into the final project workflow.



I did not implement the HBase component. The HBase implementation was completed by Student 4.



\---



\## 11. Final Conclusion



The validation was completed successfully.



All five store records — \*\*S001, S002, S003, S004 and S005\*\* — matched across all six checked fields.



The validation therefore confirms that the store-level analytical results from the Spark stage were consistent with the corresponding HBase lookup data.



\*\*Final Validation Status: PASS\*\*



This validation forms part of the Student 5 contribution for \*\*Integration, Validation and Documentation\*\*.

