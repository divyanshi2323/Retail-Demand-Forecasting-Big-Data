# RETAIL DEMAND FORECASTING
## Student 4 — Advanced Technology: HBase

### 1. My Technical Objective

Implement an HBase-based lookup layer for the retail demand project. The HBase layer stores compact store-level demand summaries so that a store can be retrieved directly by a row key instead of rerunning an aggregation over the full retail dataset.

### 2. Why HBase Is Appropriate Here

HBase is useful when the application needs key-based, low-latency access to selected records rather than repeatedly performing full-table analytical queries.

For this project, the forecasting and large analytical calculations are already produced upstream. My HBase contribution turns one useful summary into a lookup-oriented NoSQL structure:

**Store ID → demand summary**

This gives the project a different access pattern from SQL aggregation:
- Hive/Spark: calculate summaries across many records.
- HBase: retrieve a known store summary directly by row key.

The HBase table is therefore used as a serving/lookup layer, not as a replacement for Hive or Spark.

### 3. HBase Table Design

**Table:** `retail_store_summary`

**Row key:** `STORE#<Store ID>`

Examples:
- `STORE#S001`
- `STORE#S002`

**Column family:** `demand`

Columns:
- `demand:region`
- `demand:records`
- `demand:total_demand`
- `demand:avg_demand`
- `demand:avg_demand_gap`

The row key is chosen so the store identifier is unique and can be used directly for point lookup.

### 4. Data Used

The supplied project dataset contains 76,000 records and 16 columns. The store-level summary below is taken from Student 3's A1 store-performance result, which was calculated from the project `retail_demand.csv` using:
- Store ID
- Region
- Demand
- Units Sold
The `avg_demand_gap` field represents the average of `Demand - Units Sold`.

The five stores in the dataset are S001 to S005.

### 5. HBase Summary Data

| Row Key | Region | Records | Total Demand | Avg Demand | Avg Demand Gap |
|---|---|---:|---:|---:|---:|
| STORE#S001 | North | 15,200 | 1,547,573 | 101.81 | 15.09 |
| STORE#S002 | South | 15,200 | 1,625,471 | 106.94 | 15.75 |
| STORE#S003 | East | 15,200 | 1,618,324 | 106.47 | 15.97 |
| STORE#S004 | West | 15,200 | 1,529,651 | 100.63 | 14.57 |
| STORE#S005 | North | 15,200 | 1,607,085 | 105.73 | 16.07 |

These values match the supplied Student 3 A1 store-performance result, which is based on the project `retail_demand.csv`.

### 6. Docker / HBase Setup

The project Docker Compose file provides HBase as a `full`-profile service using `bde2020/hbase-standalone:1.0.0-hbase1.2.6`. Its HBase Master Web UI is exposed on port 16010, ZooKeeper on 2181, and its configured HBase root directory is `hdfs://namenode:8020/hbase`.

Start it with:

```bash
docker-compose --profile full up -d
```

Then verify:

```bash
docker ps
docker logs hbase
```

The browser evidence for the HBase Master UI is:

```text
http://localhost:16010
```

### 7. Create the HBase Table

Open the HBase shell:

```bash
docker exec -it hbase bash
hbase shell
```

Create the table:

```text
create 'retail_store_summary', 'demand'
```

Explain:

- `retail_store_summary` is the logical table.
- `demand` is the column family.
- Individual values are stored inside that family.
- The row key identifies the store.

### 8. Bulk Loading

A headerless TSV file named `student4_hbase_store_summary.tsv` is supplied with this contribution. It contains the five store-summary rows shown above.

Copy it into the NameNode container:

```bash
docker cp student4_hbase_store_summary.tsv namenode:/tmp/student4_hbase_store_summary.tsv
```

Place it in HDFS:

```bash
docker exec -it namenode hdfs dfs -mkdir -p /data/retail/results/hbase
docker exec -it namenode hdfs dfs -put -f /tmp/student4_hbase_store_summary.tsv /data/retail/results/hbase/
```

Then import it:

```bash
hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.separator=$'\t' -Dimporttsv.columns=HBASE_ROW_KEY,demand:region,demand:records,demand:total_demand,demand:avg_demand,demand:avg_demand_gap retail_store_summary hdfs://namenode:8020/data/retail/results/hbase/student4_hbase_store_summary.tsv
```

### 9. Verification

Open the shell:

```bash
hbase shell
```

Check the schema:

```text
describe 'retail_store_summary'
```

Count rows:

```text
count 'retail_store_summary'
```

Expected count:

```text
5
```

Display all rows:

```text
scan 'retail_store_summary'
```

Point lookup:

```text
get 'retail_store_summary', 'STORE#S002'
```

Another point lookup:

```text
get 'retail_store_summary', 'STORE#S004'
```

### 10. What the HBase Commands Demonstrate

`create` creates the HBase table and column family.

`scan` reads multiple rows from the table.

`get` retrieves one row using its row key.

`count` checks the number of stored rows.

The important difference from SQL is that the HBase lookup is organized around the row key. For example, when `STORE#S002` is known, HBase can directly retrieve that row.

### 11. Technical Architecture

```text
Retail demand data
        |
        v
Store-level aggregation
        |
        v
TSV lookup file
        |
        v
HDFS input location
        |
        v
HBase ImportTsv
        |
        v
retail_store_summary
        |
        +--> get STORE#S002
        |
        +--> get STORE#S004
        |
        +--> scan all stores
```

### 12. Validation

Validation consists of:
1. Confirming the HBase service is running.
2. Confirming the table exists.
3. Confirming the expected five store rows are present.
4. Comparing the HBase values with Student 3's supplied A1 store summary.
5. Performing individual `get` operations using known row keys.

The HBase values are expected to match the A1 store-summary values shown in Section 5.

### 13. Why Not Put the Whole CSV in HBase?

The HBase contribution is intentionally lookup-oriented. The full 76,000-row CSV is already handled by the distributed storage and analytics workflow. Putting every raw field into HBase would not add a clear access-pattern benefit for this project.

Instead, HBase stores a compact summary that is useful for direct retrieval by store.

### 14. Why This Is Different from Hive

Hive is SQL-oriented and is useful for questions such as:

```sql
GROUP BY store_id
```

HBase is organized around a row key and is useful for a question such as:

```text
Give me the stored summary for STORE#S002
```

So the technologies serve different purposes.

### 15. Viva-Ready Explanation

**What did you implement?**

I implemented an HBase lookup layer called `retail_store_summary`. I stored one row per store using `STORE#<store_id>` as the row key and a `demand` column family containing the store's region and demand statistics.

**Why HBase?**

The purpose was fast key-based retrieval of selected summaries. Instead of recomputing a store aggregation every time, a known store can be fetched directly with an HBase `get`.

**Why not use Hive for this?**

Hive is better suited to SQL aggregation and analytical queries across the dataset. HBase is designed around key-based row access, so it demonstrates a different access pattern.

**What is the row key?**

The row key uniquely identifies the row. Here it is `STORE#S001`, `STORE#S002`, and so on.

**What is a column family?**

A column family groups related columns physically/logically in HBase. Here the family is `demand`.

**What does `get` do?**

`get` retrieves one row using its row key.

**What does `scan` do?**

`scan` reads rows across a table.

**Where does HBase store its data in this Docker project?**

The Docker configuration sets the HBase root directory to `hdfs://namenode:8020/hbase`.

**How does this fit a Big Data architecture?**

HDFS provides distributed storage, Hive provides SQL modeling/analysis, Spark performs distributed transformations and forecasting, and HBase provides lookup-oriented access to selected results.

### 16. Evidence to Capture for My Contribution

Capture these screenshots during execution:
- Docker containers showing `hbase` running.
- HBase Master Web UI at `localhost:16010`.
- `create 'retail_store_summary', 'demand'`.
- `describe 'retail_store_summary'`.
- `count 'retail_store_summary'` showing 5 rows.
- `scan 'retail_store_summary'` showing the five stores.
- `get 'retail_store_summary', 'STORE#S002'` showing one row.

### 17. Conclusion

The HBase stage adds a NoSQL, key-based lookup layer to the Retail Demand Forecasting project. A store-level summary is transformed into an HBase table with a clear row-key design, loaded into HBase, and verified through `scan`, `count`, `describe`, and `get` operations. The implementation demonstrates a concrete use of HBase that is different from SQL aggregation and directly supports quick retrieval of retail demand summaries.
