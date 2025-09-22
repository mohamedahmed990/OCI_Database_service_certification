
### **1. Module & Lesson Overview**
*   This module shows how to operate a MySQL HeatWave system using the OCI Console.
*   This lesson focuses on **migrating data from an on-premise database to MySQL HeatWave Database Service**.
*   The process will be covered in phases:
    *   Overview
    *   Plan
    *   Export
    *   Import

### **2. On-Premises MySQL vs. MySQL HeatWave**
**On-Premises MySQL Database:**
*   Installed on your own hardware and operating system.
*   Requires management of:
    *   Data center (space, power, cooling, disaster recovery).
    *   Infrastructure (purchase/maintenance of servers, storage).
    *   Operating System (installation, patching, upgrades).
    *   Database (provisioning, configuration, backup, high availability, patching, security).
*   All this requires continuous time, funding, and management.

**MySQL HeatWave Database Service (Advantages):**
*   A **fully managed** database service on OCI.
*   Instantly provision MySQL instances; connect to a production-ready, pre-configured MySQL database on OCI, AWS, and Azure.
*   Easy to add capacity for workload requirements.
*   Automatically keep databases up-to-date with the latest MySQL Enterprise Edition during a user-defined maintenance window.
*   Manual upgrades are also possible via console or CLI.
*   Supports **full and incremental backups**; automated backups occur daily during a user-defined period.
*   **High Availability** delivers 99.99% uptime with zero data loss tolerance.
*   **Advanced security** features (data-at-rest encryption, data masking, de-identification).
*   Combines **transactions, analytics, and machine learning** in one MySQL database without ETL complexity, latency, and cost.

### **3. Prerequisites for a Successful Migration**
To complete the migration, you must be able to:
*   Log in to your account using the OCI Console.
*   Create and manage a MySQL HeatWave system with the correct compartment and VCN configuration.
*   Create a compute instance and object storage to connect to the MySQL system and data.

### **4. Migration Planning Phase**
*   **Consider downtime** and limit customer impact.
*   **Collect key metrics:**
    *   Size of the database.
    *   Version of the source database.
*   **Recommended Tool:** Use the **MySQL Shell dump and load utility** for best results.

### **5. Tools for Migration**
**MySQL Shell:**
*   An advanced command-line client and code editor for MySQL.
*   Offers scripting capabilities for JavaScript and Python in addition to SQL.

**MySQL Shell Upgrade Checker Utility:**
*   A script that checks a MySQL instance for compatibility errors and issues with upgrading.
*   **Important:** It only **checks** for issues; it does **not fix** them. Fixes are the DBA's responsibility (or with assistance).
*   Simplifies the pre-check process for upgrades, e.g., from MySQL 5.7 to 8.0, reducing the room for error (though reading release notes is still necessary).

### **6. Assess Databases for Migration**
Before starting, assess:
*   Data compatibility.
*   The on-premise MySQL version and hardware.
*   **Use tools** like MySQL Workbench or Oracle SQL Developer to compare schemas, tables, columns, indexes, and triggers between source and target.
*   **Identify and document** potential data conversion issues:
    *   Incompatible data types.
    *   Format differences (character sets, date/time formats).
    *   Null value handling.
*   **Estimate** the amount of data to be migrated and the expected migration time.
*   **Determine** the required storage and memory for the migration compute instance.

### **7. Preparing the Migration Environment**
1.  Log in to OCI and select the correct **compartment**.
2.  Create an **object storage bucket** to store the exported data.
3.  Add an **API key** in OCI (instead of a config file) on the on-premise MySQL client machine.

### **8. Export Phase**
*   Export the on-premise MySQL instance to the OCI object storage bucket using the **MySQL Shell `util.dumpInstance` utility**.
*   This utility:
    *   Exports all compatible schemas to an object storage bucket or local files.
    *   By default, exports users, events, routines, and triggers.
    *   Performs compatibility checks on the schemas during export.
*   **If issues are found:** The dump utility aborts and produces a detailed list of issues with suggested corrective steps.
*   **Important Note:** If the connection is interrupted during export, you must **rerun the dump utility**. You cannot pause and resume the export.

### **9. Import Phase (Recommended Method)**
*   After export, use the **data import feature** to import data from the object storage bucket to a standalone HeatWave database system.
*   **It is recommended to import using the console's data import feature** because it is managed by the MySQL HeatWave service and optimized for fast import processing.

**Steps for Recommended Import:**
1.  Open the navigation menu and select **Databases**.
2.  Under **MySQL HeatWave**, click **Database Systems**.
3.  Click **Create DB System**.
4.  Configure the DB system, then click **Show Advanced options**.
5.  Click the **Data Import** tab and provide the required information:
    *   If you have a Pre-Authenticated Request (PAR) URL, specify the PAR URL for the bucket or bucket prefix.
    *   Otherwise, create one.
6.  Click **Create**.
7.  The system will then **provision the HeatWave database** and **load the data** from the object storage bucket into the new database.

### **10. Post-Migration Verification**
Once the database creation and load process is complete:
1.  **Verify the results** by reviewing logs.
2.  **Check the DB system** to view all migrated tables, users, etc.
3.  **Run queries** and validate the results.
4.  Ensure the new database performs the same as or better than the on-premise system.

### **11. Process Summary**
The migration process summary:
1.  **On-Prem Setup:** Client setup, OCI API key configuration.
2.  **Export:** Export the MySQL instance to OCI Object Storage.
3.  **OCI Import:** Create a MySQL HeatWave DB instance and configure the data import feature to load data from object storage.
4.  **Verification:** Verify the migration results.

### **12. Module Conclusion**
*   In this module, you learned the essential activities for managing, monitoring, backing up, optimizing performance, and maintaining your MySQL HeatWave system to keep it secure and operating at peak efficiency.
