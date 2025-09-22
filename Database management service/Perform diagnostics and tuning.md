Of course. Here is the text broken down into structured points without any content removed.

### **1. Lesson Overview**
*   In this lesson, we will discuss:
    *   Performance monitoring.
    *   The AWR Explorer feature.
    *   SQL tuning.
    *   SQL plan management.

### **2. Performance Hub**
*   Performance Hub can analyze and tune the performance of:
    *   Oracle Cloud Infrastructure shared and dedicated autonomous databases.
    *   Virtual machine, bare metal, and Oracle Exadata Cloud Service (ExaCS) databases.
    *   External Oracle Databases.
*   With this tool, you can view real-time and historical performance data.
*   The number of tabs displayed in Performance Hub depends on the database management option enabled:
    *   **Basic Management:** Only the **ASH Analytics** and **SQL Monitoring** tabs are displayed.
    *   **Full Management:** All Performance Hub tabs are displayed.

### **3. Real-Time SQL Monitoring**
*   With real-time SQL monitoring, you can perform complex runtime application SQL analysis.
*   It helps identify and guide optimization of application calls in the data tier.
*   Capabilities include:
    *   Observing and analyzing important SQL executions in progress (parallel and long-running queries).
    *   Performing detailed and comprehensive execution analysis.
    *   Visualizing query plans interactively.
    *   Performing real-time and historical analysis.

### **4. Exadata Tab in Performance Hub**
*   The Exadata tab allows in-depth analysis of your Exadata environment without extensive overhead.
*   It eliminates the need to generate multiple AWR reports and manually search for outliers.
*   Visualizations of metrics are provided to quickly assess the overall health of your Exadata system.
*   You can:
    *   Check I/O metrics for read and writes on cells or individual disks.
    *   Identify top consumers (databases that might be monopolizing Exadata resources).
    *   View the configuration of your storage servers and ASM disk groups.

### **5. Top Activity Lite**
*   Top Activity Lite provides a less resource-intensive view of real-time activity.
*   It allows quicker refreshes of current performance, even during heavy application workloads.
*   You can adjust the data source between:
    *   Database memory.
    *   Memory and AWR data.
*   The refresh interval can be toggled and adjusted (15, 30, or 60 seconds).
*   You can drill down on specific sessions or SQL statements for detailed investigation and root cause analysis.
*   SQL monitoring is available from within Top Activity Lite.
*   You can invoke the SQL Tuning Advisor to run against a selected SQL statement within the console.

### **6. Database & AWR Monitoring**
*   Using the Database Management Service, you can monitor:
    *   Single instance and RAC databases.
    *   Container databases (CDBs), pluggable databases (PDBs), and non-container databases.
*   ==AWR (Automatic Workload Repository) is a built-in repository in the Oracle Database.==
*   ==It collects, processes, and maintains performance statistics.==
*   ==**AWR Explorer** in the Database Management Service consists of performance and data visualization tools.==
*   It displays historical performance data from AWR snapshots in easy-to-interpret charts.
*   It enables you to:
    *   Visualize AWR data in a single interface.
    *   Analyze performance trends and detect issues.
*   ==Using AWR Explorer, you can:==
    *   ==Explore and analyze AWR data for a managed database.==
    *   ==Import data from other databases to a managed database using `awrload.sql`.==
    *   ==Analyze the data and generate/download various reports from the database.==

### **7. SQL Tuning Advisor**
*   SQL Tuning Advisor is a mechanism for resolving problems related to suboptimally performing SQL statements.
*   It takes one or more SQL statements as input and invokes the Automatic Tuning Optimizer to analyze them.
*   The output is in the form of:
    *   Findings and recommendations.
    *   Rationale for each recommendation.
    *   Expected benefit.
*   **Tuning recommendations include:**
    *   Collection of object statistics.
    *   Creation of indexes.
    *   Rewriting SQL statements.
    *   Creation of SQL profiles.
    *   Creation of SQL plan baselines.
    *   And more.
*   You can choose to accept the recommendations to complete the tuning.
*   **Prerequisites:**
    *   Oracle Database administrative privileges are needed.
    *   The following must be assigned:
        *   `SELECT_CATALOG_ROLE` role.
        *   Specific privileges to the admin user.

### **8. SQL Plan Management (SPM)**
*   SQL Plan Management (SPM) allows users to maintain stable yet optimal performance for a set of SQL statements.
*   You can manage and configure SPM functionality to improve overall database performance.
*   The SPM feature in Database Management (DBM) allows visualization and deeper insights into SQL plan usage.
*   **Capabilities on the database resource homepage include:**
    *   Overview of SQL plan baselines in your database.
    *   Filter SQL plans by usage or statistics.
    *   Search based on SQL text, plan name, or origin (auto-capture or manual capture).
    *   Configure retention and storage budgets for SQL plans.
    *   Enable automatic SQL plan capture with filters based on:
        *   SQL actions.
        *   Modules.
        *   Parsing schema.
        *   SQL text.
    *   Enable and configure automatic SPM Evolve Advisor tasks.