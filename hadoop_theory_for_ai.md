# Hadoop for Data Science & AI in Service-Based Companies

## 1. Introduction: The "Why" behind Big Data
In service-based companies like Cognizant, TCS, Infosys, and Accenture, clients often come with massive legacy data warehouses or rapidly growing data streams that traditional databases (RDBMS) cannot handle. This is where the Hadoop Ecosystem comes in.

As an AI/Data Science engineer, you might think, "I just build models." However, in a real-world project, 80% of the work is **Data Engineering**. You need to process, clean, and aggregate terabytes of raw data before your model can even see it. Hadoop is the storage and processing engine often used for this "pre-modeling" phase.

## 2. Core Components of Hadoop
Hadoop is not a single tool but an ecosystem. The primary components you need to know for interviews and projects are:

### A. HDFS (Hadoop Distributed File System) - "The Storage"
*   **Concept:** Imagine breaking a large 1TB file into small 128MB chunks and spreading them across 100 cheap computers. That is HDFS.
*   **Real-World Scenario:** A retail client (e.g., Walmart) stores 5 years of transaction logs. This data is too big for a single server. It is dumped into HDFS as raw CSV or Parquet files.
*   **Key Interview Question:** "How does HDFS handle hardware failure?"
    *   *Answer:* Data replication (usually 3 copies). If one node fails, the data is available on another.

### B. YARN (Yet Another Resource Negotiator) - "The Operating System"
*   **Concept:** Since you have a cluster of 100 computers, you need a manager to say, "Job A gets 10GB of RAM on Node 5." That is YARN.
*   **Relevance:** When you run a PySpark job, it asks YARN for resources to execute the task.

### C. MapReduce - "The Old Processing Engine"
*   **Concept:** The original way to process data in Hadoop. It writes intermediate results to disk, making it slow.
*   **Status in 2024:** Mostly replaced by **Spark** (which processes in-memory). However, understanding the logic (Split -> Map -> Shuffle -> Reduce) is still crucial for logical thinking.

### D. Hive - "SQL on Hadoop"
*   **Concept:** A data warehouse software project built on top of Apache Hadoop for providing data query and analysis.
*   **Real-World Scenario:** Business Analysts don't know Java or Python. They know SQL. They use Hive to query data stored in HDFS.
*   **AI Context:** You will often use Hive queries (`spark.sql("SELECT * FROM ...")`) to pull your initial training dataset.

## 3. The Modern Data Lake Architecture in Service Companies
In a typical project (e.g., for a Banking Client), the architecture often looks like this:

1.  **Ingestion:** Data comes from Mainframes, SQL Servers, or APIs -> Landed in **HDFS (Landing Zone)**.
2.  **Processing (ETL):** **PySpark** jobs read raw data, clean it, handle nulls, and format dates -> Stored in **HDFS (Processed Zone)**.
3.  **Analysis/AI:** Data Scientists read processed data using Spark, build features, train models (XGBoost, Logistic Regression) -> Save model/predictions.
4.  **Consumption:** Results are pushed to a dashboard (Tableau/PowerBI) or a fast database (NoSQL) for the app to read.

## 4. Common Problems Solved using Hadoop/Spark
1.  **ETL Offloading:** Moving expensive data processing from expensive Data Warehouses (like Teradata) to cheaper Hadoop clusters.
2.  **360-Degree Customer View:** Joining data from ATM logs, website clicks, and branch visits (all distinct, massive datasets) to understand a customer.
3.  **Archival:** Storing years of regulatory data cheaply.

## 5. Interview Prep: What Service Companies Ask
*   "Tell me about a challenging data scenario you faced."
    *   *Tip:* Don't just say "I built a model." Say "The data was 500GB, stored in HDFS. I used PySpark to partition the data, optimized the join operations to avoid OOM (Out of Memory) errors, and then built the model."
*   "Difference between HDFS and S3?" (If cloud project).
*   "File formats: Parquet, Avro, ORC. Which did you use and why?" (Parquet is best for columnar data needed in AI).

---
*Note: While Hadoop provides the base, PySpark is your tool of choice to interact with it efficiently.*
