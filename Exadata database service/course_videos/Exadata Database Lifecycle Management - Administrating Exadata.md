### **1. Introduction & Lesson Objectives**
*   Hello, and welcome. My name is Eddie Ambler from Oracle Product Management.
*   Over the next few minutes, we're going to discuss the Exadata Database Service and highlight the core database lifecycle management functionalities that are built into the service.
*   After completing this lesson, you should be able to:
    *   Create custom database and grid infrastructure images.
    *   Create a Database Home.
    *   Create a database.
    *   Perform pluggable database (PDB) management.
    *   Enable Data Guard.
    *   Perform user-managed maintenance updates and upgrades.
*   You can use the console to perform most of these activities.
*   You can also use the API, CLI, or SDKs to perform these operations.

### **2. Creating Custom Software Images**
*   Custom database and grid infrastructure software images establish standard-based solutions that can be incorporated into cloud automation workflows and Terraform-based deployments.
*   They allow your organization to create an approved "gold image" for developers and DBAs to use.
*   Custom software images give you the ability to create customized Oracle Database software configurations that include:
    *   Your chosen Grid Infrastructure and database versions.
    *   Release Updates (RUs).
    *   One-off patches.
    *   The contents of an existing Database Home patch inventory.
*   Custom images are resources within your tenancy that you create *prior* to provisioning or patching an Exadata DB Service instance, Grid Infrastructure Home, or Database Home.
*   You can create custom software images for different types; ensure you select the correct **image type** and **service type** before creation.
*   Custom software images are automatically stored in Oracle-managed object storage and can be viewed and managed in the OCI Console.
*   **How to Create a Custom Image:**
    1.  Click on the **Create Software Image** button.
    2.  Choose to create a **database** or **grid infrastructure** software image.
    3.  Provide a friendly **display name** for the image.
    4.  Select the **compartment** to store the image in (can be different from your current compartment).
    5.  **For a Database Image:**
        *   Select the desired database release.
        *   Choose a Release Update, Proactive Bundle Patch, or one-off patch to include.
        *   You can also upload an Oracle Home inventory to use as the source for required patches.
    6.  **For a Grid Infrastructure Image:**
        *   Select the desired Grid Infrastructure release.
        *   Choose a Release Update, Proactive Bundle Patch, or one-off patches to include.
        *   You can also upload a Grid Infrastructure home inventory.
*   You can create custom images with any Oracle Database or Grid Infrastructure software version and update that is supported in Oracle Cloud.
*   Click **Create Software Image** to complete the process.
*   Once created, custom images are listed on the software images screen, showing the image type, service, and version.

### **3. Creating a Database Home**
*   Prerequisite: The Exadata infrastructure and VM cluster resources must already be created.
*   **How to Create a Database Home:**
    1.  Navigate to the Exadata VM cluster.
    2.  Under **Resources**, click **Database Homes**.
    3.  Click **Create Database Home**.
    4.  Enter a **Database Home display name**.
    5.  Select a **database image**.
        *   You can change from the default by selecting **Change Database Image**.
        *   You can select an Oracle-provided image or a custom database software image.
    6.  Click **Create**.

### **4. Creating a Database**
*   **How to Create a Database:**
    1.  From the Exadata VM Cluster details page, click **Create Database**.
    2.  Enter basic information:
        *   Database name.
        *   Desired database version.
        *   Optional pluggable database (PDB) name.
    3.  Specify the **Database Home** to use (select an existing one or create a new one).
    4.  Provide the **administrator credentials** for the SYS user.
    5.  Configure **database backup** details (destination and schedule).
    6.  In the **advanced options**, choose encryption:
        *   **Oracle-managed keys:** Data is encrypted with a key Oracle maintains.
        *   **Customer-managed keys:** Data is encrypted using a master encryption key from your selected Vault service.
    7.  Click **Create** to start the database creation workflow.
*   **For Exadata Cloud@Customer:** You can integrate your on-premise Oracle Key Vault (OKV) to secure critical data on-premises.
    *   OKV provides complete control of your encryption keys on an external, centralized key management device.
    *   It is optimized for Oracle wallets, Java keystores, and Oracle Advanced Security (including TDE master keys).

### **5. Pluggable Database (PDB) Management**
*   When you create a database, a single Container Database (CDB) with one Pluggable Database (PDB) is created by default.
*   You can use the console or APIs to conduct PDB lifecycle management tasks.
*   **Creating a PDB:**
    1.  From the **Database Details** page, click **Create Pluggable Database**.
    2.  Enter the desired **PDB name** and **admin password**.
    3.  Click **Create Pluggable Database**.
*   **Connecting to a PDB:** From the **Pluggable Database Details** page, you can connect via separate connection strings (Easy Connect or Long Connect) and open Performance Hub.
*   **Cloning a PDB:**
    1.  Click the **Clone** tab on the PDB Details page.
    2.  Choose the clone type:
        *   **Local Clone:** Creates a PDB within the same CDB as the source.
        *   **Remote Clone:** Creates a PDB in a different CDB (can be across VM clusters in the same availability domain).
        *   **Refreshable Clone:** Creates a PDB in a different CDB whose data can be refreshed via the **More Actions** tab.
    3.  Select the clone destination and enter the required information.
    4.  Click **Clone Pluggable Database**.
*   **More Actions Tab:** Allows additional PDB lifecycle tasks:
    *   **Start/Stop:** Launch dialog to confirm the operation.
    *   **Relocate:**
        *   Choose **Relocate** from the More Actions tab.
        *   Enter the destination DB system, new PDB name, and password.
        *   Click **Relocate Pluggable Database**.
    *   **Restore:**
        *   Choose **Restore**.
        *   Choose to restore to the latest backup or a specific point in time.
        *   Click **Restore**.
    *   **Delete:**
        *   Choose **Delete**.
        *   Confirm the action in the dialog box.

### **6. Enabling Data Guard**
*   Data Guard provides real-time disaster protection and is a key component of a maximum availability architecture.
*   It ensures business continuity, allows planned maintenance with minimal interruption, and supports failover in a disaster.
*   **How to Enable Data Guard:**
    1.  Select the peer VM cluster where the standby will reside (can be in another region or availability domain).
    2.  Select the **Data Guard type**:
        *   **Data Guard**
        *   **Active Data Guard:** Extends capabilities for data protection, availability, and offloading read-only workloads. It is included with the Exadata Database Service (license included). *Note:* For hybrid configurations, Active Data Guard must also be licensed for the on-premise system.
    3.  Choose to use an existing **Database Home** or create a new one.
    4.  Provide a **database unique name** for the standby.
    5.  Provide the **standby database admin password** (must match the primary database admin password).
    6.  Click **Enable Data Guard**.
*   **Data Guard Role Management:**
    *   **Switchover:** Planned role reversal. Switches the primary and standby roles. Used for OS/hardware maintenance and patching.
    *   **Failover:** Unplanned role reversal. Used when a catastrophic failure occurs on the primary. The failed primary is removed, and a standby becomes the primary.
    *   **Fast Start Failover:** Can be configured to automatically and quickly failover to a synchronized standby.
    *   **Reinstate:** Returns a failed database to service as a standby after correcting the failure cause.
*   **Data Guard Requirements:**
    *   Both DB systems must be in the **same compartment**.
    *   If in the same region, both must use the **same Virtual Cloud Network (VCN)**.
    *   If in different regions, you must **peer the VCNs** for each database.
    *   Database versions must be the **same**.
    *   Each database must have a **unique DB unique name** (but can have the same database name).
    *   Configure **security list ingress and egress rules** for the subnets of both DB systems to enable TCP traffic between the applicable ports (rules must be stateful).
    *   The minimum requirement is to enable egress for TCP traffic for the SCAN listener port (default **1521**).