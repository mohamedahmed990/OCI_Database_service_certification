### **1. Lesson Overview & Service Summary**
*   In this lesson, we will discuss key use cases, database management features, supported deployments, and pricing.
*   Let's start with a summary of the Oracle Cloud Database Management service, when and who would use it.
*   Oracle Cloud Observability and Management services, like the database management service, are designed to help customers manage cloud-native and multi-cloud environments.
*   They add value to existing on-premises-based solutions like Oracle Enterprise Manager for on-premises and hybrid database management.

### **2. What is the Oracle Cloud Observability and Management Service?**
*   It is a managed service.
*   It leverages Oracle's industry-leading performance management methods.
*   It uses OCI-native metrics for DevOps, event alarms and monitoring.
*   It provides a unified user interface to monitor Oracle databases across:
    *   The Oracle Cloud
    *   Other clouds
    *   On-premises
    *   Or a hybrid combination.

### **3. Database Management Service Capabilities & Users**
*   The database management service supports both on-premises and Oracle Cloud deployments on:
    *   Virtual machines
    *   Bare metal
    *   ExaCS (Exadata Cloud Service)
    *   ExaCC (Exadata Cloud@Customer)
    *   ADB (Autonomous Database)
*   It provides real-time SQL monitoring and the ability to search SQL and sessions.
*   It compares performance across different periods of time.
*   It has a Performance Hub with blocking session views and more.
*   It is integrated with other OCI services.
*   **Developers and DevOps** would use it to perform database administration tasks, typically for dev and test environments.
*   **DBAs** would use it to help monitor and manage databases deployed into the cloud, supporting production and development activities.

### **4. Benefits of the Service**
*   Provides latest Oracle database support.
*   Removes risk of unmanaged databases.
*   Replaces siloed third-party tools.
*   Helps recover hardware and resources to save money.
*   Provides in-depth diagnostic and SQL metric detail no other vendor can provide.
*   Allows you to create one job to run across many databases.
*   Reduces error and saves time.
*   If you are already familiar with managing Oracle databases on-premise, you can reuse your knowledge and skills.
*   You get a unified console for on-premise and cloud databases with life cycle Database management capabilities for monitoring, performance management, tuning, and administration.
*   You can use advanced database fleet diagnostics and tuning to troubleshoot issues and optimize performance.
*   You can optimize SQL with real-time monitoring and simplified database configurations.

### **5. Service Details & Functionality**
*   It's a managed cloud native service, meaning it's managed and updated by Oracle and is routinely updated with new features.
*   It enables you to perform Database Management and performance diagnostics for individual databases or for a fleet altogether.
*   It provides a single console to perform database management, administration, and performance management activities for a specific set of databases or databases altogether.
*   Use the unified cloud console to:
    *   Monitor database time and average active sessions to evaluate database performance.
    *   Monitor IO throughput and bandwidth to proactively detect throughput bottlenecks.
    *   Display system storage and user data storage broken down by usage in system tablespaces and user data.
    *   View user data storage broken down by usage in the top five user table spaces.

### **6. Configuration & Requirements**
*   When you configure the service, you create a dynamic group and set up three required OCI object storage permissions the management agent needs:
    *   Permissions to read buckets.
    *   Permissions to create objects.
    *   Permissions to inspect objects.
*   This allows the agent to store the results of a query SQL type job into an object storage bucket.
*   Database management supports Oracle Database version 11.2.0.4 and later.

### **7. Key Tasks You Can Perform**
*   Monitor the key performance and configuration metrics of your fleet of Oracle databases.
*   Compare and analyze database metrics over a selected period of time.
*   Use Performance Hub for a single pane of glass view of database performance to quickly diagnose issues.
*   Use AWR Explorer to visualize historical performance data from AWR snapshots in easy-to-interpret charts.
*   Group your critical Oracle databases (which reside across compartments) into a database group and monitor them.
*   Create and schedule SQL jobs to perform administrative operations on a single Oracle database or database group.
*   Use ASH analytics, SQL/session, and Tuning Advisor capabilities to determine a database issue root cause and then fix it.

### **8. Fleet Summary & Monitoring**
*   Using the service, you get a unified view of your fleet of databases.
*   The Fleet summary enables monitoring of multiple Oracle database services deployed across OCI compartments or groups from a single screen.
*   The Members tab of the Database Management Fleet Summary page displays a list view by default, and the table option lists in a tabular format.
*   In the fleet summary, you can:
    *   View the status of databases.
    *   Compare database performance metrics over time.
    *   View database current resource usage like a summary of the fleet CPU utilization and fleet storage utilization.
*   In the Resource Usage section, you can obtain:
    *   A summary of overall CPU storage allocation and utilization.
    *   A change percentage of resource usage between the selected and comparison time for databases within a compartment and across compartments.

### **9. Performance Diagnostics & OCI Integration**
*   The Performance tab displays a tree map of the performance of your Oracle databases against various database metrics.
*   As an OCI native service, it is integrated with the OCI control panel with access to metrics natively from OCI object storage, compute, network, and more.
*   It can utilize OCI monitoring and notification services to notify those in development, DevOps, and IT ops roles.

### **10. Database Groups & Job Automation**
*   Create groups of Oracle databases for monitoring and managing them together, simplifying oversight.
*   Using database groups, you can execute a SQL query for the databases in the group.
*   You can view, monitor, and obtain insights, such as the inventory or the number of Oracle databases across a compartment or group.
*   Group databases by their purpose (e.g., group by container databases and pluggable databases spanning compartments).
*   Then use bulk SQL operations to automate life cycle operations.
*   The service can be used to perform routine database administration tasks, schema updates, and storage changes.
*   Job automation abilities can be used to automate routine tasks by defining database jobs that can run against a set of databases on a schedule.
*   SQL scripts can be packaged into templates to run in bulk across databases in a group to automate scheduled database maintenance tasks.
*   You can create templates to address needs across compartments within a group.
*   You can apply jobs as templates to run your own SQL scripts against a single database or a group.

### **11. Monitoring Autonomous Databases**
*   You can use database management to monitor a single autonomous database, or a fleet of autonomous databases.
*   You can view details such as:
    *   The database type and version
    *   Deployment type
    *   Compartment name and ID
*   You can monitor database performance attributes for the time period selected in the time period menu ("Last 60 minutes" is the default).
*   The visual representations or charts in the summary section provide quick insight into the health of your database during the selected time period and enable you to analyze data better.
*   You can also filter the data displayed in the charts by clicking the dimensions displayed in the legend.

### **12. Enablement Options for Cloud Databases**
*   **Basic Management:**
    *   Performance Hub offers only ASH analytics and SQL monitoring tabs for the container database (CDB) resources.
    *   Only 14 metrics for the container databases are viewable within the metric's explorer application on the Resource home page.
    *   Pluggable database (PDB) level monitoring and metrics are not supported.
*   **Full Management:**
    *   Full feature enablement for container databases (CDBs) and pluggable databases (PDBs).
    *   Resources with full option will show in the fleet overview with an individual resource home page with summary.
    *   All applications in Performance Hub will be available.
    *   Exadata and RAC monitoring will be available.
    *   Additional features such as SQL Tuning Advisor, optimizer statistics, and SQL plan management will be available.
    *   It includes pluggable database (PDB) resource enablement.

### **13. Supported Deployments & Use Cases**
*   The service supports databases deployed anywhere: on-premise, Oracle Cloud, or a third-party cloud provider.
*   For external environments, monitoring capabilities extend to database system monitoring and Exadata infrastructure monitoring.
*   Use cases for the service include:
    *   Replacing an old tool that doesn't support databases in the cloud/hybrid environments or the latest Oracle database version.
    *   Being used by development and DevOps while DBAs continue to use Oracle Enterprise Manager on-premise.
*   It supports external databases (on your own site, on-premise), for example:
    *   An external Oracle database deployed on an Oracle Exadata database machine.
    *   An external Oracle database deployed by enterprise manager in your own private cloud.

### **14. Important Note on Functionality**
*   Functionality is always subject to change, and this is just an example at the time it was published.
*   Monthly, the database management is enhanced with new features and support.
*   Be sure to check the documentation online for the very latest information.