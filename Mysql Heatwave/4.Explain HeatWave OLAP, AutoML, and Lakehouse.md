### **1. Introduction & Overview**
*   We will start with an overview of what is required for a working MySQL database service system.
*   We will go over the steps and reasons for creating the database system.
*   We will finish by going over the methods for connecting and using the new MySQL database service system.

### **2. MySQL HeatWave: The Unified Platform**
*   MySQL HeatWave is the only cloud database service that combines:
    *   Transactions
    *   Real-time analytics (across data warehouses and data lakes)
    *   Machine learning
*   ...into **one** MySQL database.
*   It eliminates the complexity, latency, risks, and costs of ETL duplication.
*   HeatWave can be accessed through:
    *   Oracle Cloud Infrastructure (OCI)
    *   Amazon Web Services (AWS)
    *   Microsoft Azure

### **3. HeatWave Cluster Architecture**
*   You enable HeatWave by **adding a HeatWave cluster** to a MySQL database system.
*   A **HeatWave cluster** consists of one or more **HeatWave nodes**.
    *   Each node can store up to **800 gigabytes** of data.
    *   Nodes store data **in memory** and process analytics and machine learning queries.
    *   Each node hosts an instance of the **HeatWave query processing engine**.
*   The MySQL database system includes a **HeatWave plugin** responsible for:
    *   Cluster management
    *   Query scheduling
    *   Returning query results to the MySQL database system
*   When enabled, queries meeting certain prerequisites are **automatically offloaded** from the MySQL database system to the HeatWave cluster for accelerated execution.
*   **Data Flow:**
    1.  Queries are issued from a MySQL client/application to the MySQL database system.
    2.  The MySQL database system interacts with the HeatWave cluster.
    3.  The HeatWave cluster returns results to the MySQL database system.
    4.  The MySQL database system returns results to the client/application.
*   **Data Persistence:** Data loaded into HeatWave is automatically persisted to **OCI Object Storage**, allowing for quick reloading after a cluster pause or recovery from failure.

### **4. Prerequisites for Using HeatWave**
Before using HeatWave, ensure the following are present:
*   A MySQL database system created using:
    *   **VM.Standard.E2.64**
    *   Or **MySQL HeatWave VM.Standard.E3** shape.
*   A **running compute instance** attached to a public subnet on the **same VCN** as the MySQL database system.
*   **MySQL Shell 8.0.22 or higher** installed on the compute instance.
*   In addition to mandatory MySQL policies, you or your group must have been granted the **`mysql-analytics`** policies.

### **5. Adding a HeatWave Cluster**
To add a HeatWave cluster to an existing MySQL database system:
1.  Open the navigation menu. Under **MySQL**, click **Database Systems**.
2.  Add the cluster in one of these ways:
    *   Select the database system and choose **Add HeatWave Cluster**.
    *   Open the database system and select **HeatWave Cluster**, then **Add HeatWave Cluster**.
3.  Configure the cluster:
    *   **Shape Details:** Number of OCPUs, RAM, etc.
    *   **Node Count:** Number of HeatWave nodes to create.
4.  Click **Add HeatWave Cluster** to create it.

### **6. Generating a Node Count Estimate**
*   To generate an estimate, the data intended for HeatWave **must be present** on the MySQL database system.
*   Click **Estimate Node Counts**.
*   In the dialog box, click **Generate Estimates**.
*   After completion, a table displays information about the evaluated schemas.
*   Select the schemas to include in the estimate.
*   Review the estimate details in the summary dialog box.
*   Click **Apply Node Count Estimate**.

### **7. Loading Data into HeatWave**
Loading data typically involves:
1.  Identifying tables to load.
2.  Excluding columns that are not required or supported.
3.  Encoding string columns.
4.  Defining `RAPID` as the secondary engine.
5.  Executing table load operations.
*   **Process:** Data is read from InnoDB using batched, multi-threaded reads, converted into a columnar format, sent over the network, and distributed among HeatWave nodes.
*   **Distribution:** Tables are sliced horizontally and partitioned by primary key (unless data placement keys are defined).
*   **Verification:** Verify tables are loaded by querying load status from the HeatWave performance schema tables. Loaded tables have an `AVAIL_RPDGSTABSTATE` load status of `LOADED`.

### **8. User Interaction & Query Processing**
*   Users and applications interact with HeatWave **through the MySQL database node**.
*   They connect using standard tools and standard-based ODBC or JDBC connectors.
*   **Query Offloading:**
    1.  A query is submitted to the MySQL database.
    2.  The MySQL query optimizer **transparently decides** if it should be offloaded to HeatWave.
    3.  **Decision is based on:**
        *   Whether all operators/functions are supported by HeatWave.
        *   If the estimated processing time with HeatWave is less than with MySQL.
    4.  If both conditions are met, the query is pushed to HeatWave nodes for processing.
    5.  Results are sent back to the MySQL database node and returned to the user.

### **9. Data Consistency & Real-Time Updates**
*   Data in HeatWave is persisted in MySQL InnoDB.
*   Any updates to the tables are **automatically propagated** to the memory of the HeatWave nodes **in real-time**.
*   This ensures subsequent queries always access the latest data.
*   This is done by a **lightweight change propagation algorithm** that can keep up with MySQL data update rates.

### **10. In-Database Machine Learning Example**
*   **Scenario:** An e-commerce application wanting an ML model to recommend products based on customer purchases.
*   **Solution with HeatWave:**
    *   Build and run the ML model **directly in the MySQL HeatWave database**.
    *   The system provides **real-time recommendations** as purchases are processed.
    *   In parallel, get **real-time analytics** on customer behavior.
*   **Benefits:**
    *   No need for a separate analytics database or ML solution.
    *   No need to move data (ETL).
    *   **Increased security** and compliance, as data isn't transferred between stores.
    *   More effective than using different solutions for OLTP, OLAP, and ML.

### **11. MySQL HeatWave Lakehouse**
*   Enables querying of **half a petabyte** of data in multiple formats (CSV, Parquet, Aurora/Redshift export files) in object store.
*   Allows customers to leverage HeatWave benefits even when data is **not stored inside a MySQL database**.
*   Customers can query:
    *   Transactional data in MySQL databases.
    *   Data in various formats in object storage.
    *   A **combination** of both.
*   ...using **standard SQL commands**.
*   Can query up to **500 terabytes** of data; the HeatWave cluster scales to **512 nodes**.
*   Querying data in object store is **as fast as querying the database** (an industry first).
*   Data is processed and transformed into HeatWave's in-memory format **in the object store**, not copied to the MySQL database.
*   This allows use of HeatWave for **non-MySQL workloads**.
*   Provides **one service** for transaction processing, analytics across data warehouses/lakes, and machine learning **without ETL**.

### **12. Managing the HeatWave Cluster**
**Starting, Stopping, Restarting:**
1.  Open the navigation menu. Under **MySQL**, click **Database Systems**.
2.  Choose your database system.
3.  In the resources list, select **HeatWave**.
4.  Select an action:
    *   **Start:** Starts a stopped cluster. (Stop action enabled afterward).
    *   **Stop:** Stops a running cluster. (Start action enabled afterward). ***Stops billing for the cluster.***
    *   **Restart:** Shuts down and restarts the cluster. ***You must reload data.*** Billing resumes after restart.

**Deleting a HeatWave Cluster:**
1.  Open the navigation menu. Under **MySQL**, click **Database Systems**.
2.  In the **HeatWave** filter, select **Attached** to see systems with a cluster.
3.  Open your database system and select **HeatWave** from the resources list.
4.  Click **Delete** and follow the instructions.
*   **Important:** Deleting the cluster **does not delete** the database system or its data. However, deleting the database system **also deletes** the attached HeatWave cluster.

### **13. Key Takeaways**
*   MySQL HeatWave is the only cloud service that **unifies transactions, analytics, and ML** in one MySQL database without ETL.
*   It delivers **unmatched performance and price performance**.
*   **HeatWave AutoML** enables native in-database machine learning, allowing users to build, train, deploy, and explain ML models inside MySQL without expertise.
*   **MySQL HeatWave Lakehouse** lets users query vast amounts of data in object storage in various file formats, leveraging HeatWave benefits for data stored outside MySQL.
