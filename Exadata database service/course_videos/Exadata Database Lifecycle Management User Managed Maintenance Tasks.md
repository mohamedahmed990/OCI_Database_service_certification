
Of course. Here is a detailed breakdown of the text into structured points, ensuring no content is removed.

### **1. Management Responsibility Matrix**
*   Managing maintenance updates for the Exadata Database Service is divided into two sections:
    1.  **Oracle-managed infrastructure maintenance updates**
    2.  **User-managed maintenance updates**

### **2. Oracle-Managed Infrastructure Maintenance**
*   **Oracle is responsible** for applying quarterly infrastructure updates to all infrastructure components, including:
    *   Physical compute servers and the root VM.
    *   Exadata storage servers.
    *   Internal switches in the Exadata secure RDMA network fabric.
    *   PDUs (Power Distribution Units).
    *   ILOM (Integrated Lights Out Manager) interfaces, firmware.
    *   Any control plane components.
*   This is referred to as **infrastructure maintenance**.

### **3. User-Managed Maintenance Tasks**
*   To maintain a secure and optimally functioning Exadata Database Service instance, users must **regularly** perform the following tasks:
    *   Patching the Oracle Grid Infrastructure software.
    *   Patching the Oracle Database software on the Exadata Database VM.
    *   Updating the operating system on the Exadata Database VM.
*   These tasks should be done **quarterly, but not to exceed 180 days** from the last applied patch.

### **4. Required Permissions for User-Managed Maintenance**
*   To perform these operations on OCI, you must be granted security access with the appropriate **IAM policies**.
*   This access is required whether using the web console, REST APIs, an SDK, or the command line interface (CLI).
*   If you receive an "unauthorized" message, verify your access with a tenancy administrator.

### **5. Best Practices Before Patching**
Before applying updates, follow these best practices to avoid failures:
*   **Always backup your database** before applying any updates to the DB Home.
*   **Consider moving the database to a new Database Home** instead of updating the existing one.
*   **Update Grid Infrastructure first**, as its patch level determines the highest database level the cluster can support.
*   **Run the pre-check operation** prior to the maintenance window to identify and resolve potential issues.
*   Ensure **all servers and database instances are up and running**.
*   Ensure **/u01** (Grid Infrastructure Home) has **at least 15 GB** of free space before a GI update.
*   Ensure **/u02** (Database Home) has **at least 15 GB** of free space before a DB Home update.
*   **Use the OCI management interfaces** (console, API) to perform update and patching operations.

### **6. Identifying Current Patch Levels & Available Updates**
*   Navigate to the **VM cluster details page**.
*   In the **Version section**, you can see:
    *   Current patch levels for the **Exadata image** and the **Grid Infrastructure**.
    *   The version of the **Database Home** in use for each created database.
*   Click the **View Updates** link in the Version section to go to the **Updates page**.
*   The Updates page is organized into three sections:
    1.  **Exadata VM cluster OS**
    2.  **Exadata VM cluster Grid Infrastructure**
    3.  **Database Home**

**Details on the Updates Page:**
*   **For OS Updates:**
    *   Lists available updates for Exadata image components (which contain the OS updates).
    *   Each update has: an update description, version, release date, and timestamp of the last successful pre-check.
*   **For Grid Infrastructure Updates:**
    *   Lists available updates for GI software components.
    *   Includes the same info as OS updates, plus a **`type`** field (patch or upgrade).
*   **For Database Home Updates:**
    *   Lists standard Oracle-provided and custom database software images.
    *   Each update has: a patch description, version, and release date.
    *   Use the scope selector on the left to list patches specific to a particular Database Home.

### **7. Update History View**
*   The **Update History page** allows you to review previous patching operations on VM cluster components and Database Homes.
*   It shows what patches have been pre-checked or applied and the timestamp of each action.
*   Each entry represents an attempted patch operation and indicates success or failure.
*   You can **retry a failed** patch operation (a new history entry will be created).
*   **Note:** The console history does *not* show updates applied via command-line tools (like `dbcli`).

### **8. Updating the Guest VM OS Image**
*   The **Exadata image update** automates updating the guest VM image on Exadata VM cluster nodes via the OCI Console/APIs.
*   It simplifies and speeds up VM cluster patching, reduces errors, and eliminates the need for Patch Manager.
*   The Exadata image contains the **virtual machine OS updates**.
*   The process includes:
    *   A **precheck** function to ensure VMs are ready.
    *   A **rollback** option in case of issues.
*   Minor and major version updates can be done from the UI and REST APIs.
*   For security, only the **four latest** Exadata image minor version updates are available in the console.

**Process to Apply an OS Image Update:**
1.  Use the **Updates page** or REST API to find available OS image updates.
2.  Choose the desired OS update version.
3.  From the **Actions** icon for the patch, you can:
    *   **Run Precheck:** Validates system readiness. *(Highly recommended to run this in advance of your maintenance window).*
    *   **Apply Exadata OS image update:** Performs a precheck and then applies the update if it passes.
4.  The **Apply** action brings up a confirmation screen. Confirm the VM cluster name and target version are correct.
5.  Click **Apply Exadata OS Image Update** to start the process.

### **9. Patching the Oracle Grid Infrastructure (GI)**
*   Use the **Updates page** or REST API to find and apply available GI patches.
*   Choose the desired GI version to apply.
*   From the **Actions** icon, you can:
    *   **Run Precheck:** Validates system readiness. *(Recommended to run in advance).*
    *   **Apply Grid Infrastructure Patch:** Performs a precheck and applies the update if it passes.
*   The GI update is performed in a **rolling fashion**, one node at a time.
*   **Note:** The database instance on the VM undergoing a GI update will **not be available** during its update cycle.

### **10. Updating the Oracle Database Home**
*   Customers can use an **Oracle-provided** database software image or a **custom** image.
*   **Two Paths to Update:**
    1.  **Update an existing Database Home** to the desired patch level (updates *all* databases using that Home).
    2.  **Create a new Database Home** with the desired patch level and **move a database** to it. *(This is the quickest way to patch a single database and reduce downtime).*

**Process to Apply a Database Home Update:**
1.  Use the **Updates page** or REST API to find available updates (from Oracle standard or custom images).
2.  Choose the desired patch version.
3.  From the **Actions** icon, you can:
    *   **Run Precheck:** Validates system readiness. *(Highly recommended to run in advance).*
    *   **Apply:** Performs a precheck and applies the update if it passes.
*   Database Home updates are delivered in a **rolling manner** across RAC database instances.
*   This procedure updates the Oracle Database software for **all databases** in that Database Home.
*   To patch an **individual database**, move it to another Database Home with the desired patch level (the preferred, less disruptive approach).

**Updating with a Custom Database Software Image: Two Paths:**
1.  **Create a new Database Home** with the custom image and move the database to it.
2.  **Update the existing Database Home** with the custom image (updates *all* databases using that Home simultaneously).

### **11. How to Move a Database to a New Home**
1.  From the **database details page**, click the **Move to Another Database Home** tab.
2.  This opens the **Move Database** screen.
3.  Select the **target Database Home** (with the desired patch level).
4.  Click the **Move Database** button.
*   **During the move:** The database and the source/target Database Home status displays as **Updating**.
*   **If unsuccessful:** The database status is **Failed**, and the Database Home field provides the reason for failure.

### **12. Impact of Update Operations & Achieving Zero Downtime**
*   Wherever possible, GI and DB Home maintenance is done to **preserve service availability**.
*   With RAC database **rolling updates**, you can achieve **zero database service downtime**.
*   During the update, maximum compute performance/throughput are **temporarily reduced** while RAC instances restart.
*   To achieve **zero downtime for applications**, follow the **Exadata Cloud Maximum Availability Architecture (MAA)** best practices documentation.

### **13. Upgrading the Grid Infrastructure**
*   This process upgrades the GI on an Exadata cloud VM cluster using the OCI Console or APIs.
*   Upgrading GI allows you to provision Database Homes and databases using the **most current** Oracle Database software version.
*   The upgrade is performed on **all compute nodes** in the cluster in a **rolling fashion** (one node at a time).
*   Database instances on a node undergoing upgrade will **not be available** for workloads.
*   Monitor progress by viewing the associated **work requests**.

**Important Notes on GI Upgrade:**
*   **Run an upgrade precheck** prior to the maintenance window.
*   The GI upgrade feature is **not available** if an Exadata infrastructure maintenance operation is scheduled to start within **24 hours**.
*   The following **Data Guard operations are not allowed** on a VM cluster undergoing a GI upgrade:
    *   Enable Data Guard.
    *   Conduct a switchover or failover *to* a database on this cluster.
    *   Perform management operations (start, stop, reboot nodes, scale CPUs).
    *   Provision or manage Database Homes or databases.
    *   Restore a database.
    *   Edit the IORM (I/O Resource Management) settings.

### **14. Upgrading a Database**
**Preparation:**
*   **Back up the database.**
*   **Test the new database software version** on a test system first.
*   **Run an upgrade precheck** before the maintenance window to discover and fix issues.
*   **Create an Oracle Database Home** that contains the **target database software version** (using Oracle-published or custom images).
*   Ensure **all pluggable databases (PDBs)** in the container database (CDB) **can be opened** (cannot-be-opened PDBs can cause upgrade failure).
*   **Disable automatic backups** and perform an **on-demand full backup** before starting (upgrades cannot run during an automatic backup).
*   **Note:** After upgrade, you *cannot* use automatic backups taken *before* the upgrade to restore to an earlier point in time.

**Automatic Steps During Database Upgrade:**
1.  An **automatic precheck** is conducted to identify issues and potentially stop the operation.
2.  A **guaranteed restore point** is set, enabling a flashback in case of failure.
3.  The database is **moved** to a user-specified Database Home with the target software version.
4.  The **Database Upgrade Assistant (DBUA)** software is used to perform the upgrade.

**Process to Conduct a Database Upgrade:**
1.  Navigate to the **database details page** for the database to upgrade.
2.  In the **database version section**, see the current Database Home and version.
3.  Select the **More Actions** tab and choose **Upgrade**.
4.  In the **Upgrade Database** screen:
    *   Select the **Oracle Database version** to upgrade to.
    *   Select the **target Database Home** to use.
    *   **Run the precheck** and troubleshoot any issues.
    *   Once the precheck passes, click **Upgrade Database**.

**Upgrading Databases with Data Guard:**
*   You can upgrade the **primary** or the **standby** first.
*   **Standby-first** patching and upgrades are **recommended**.
*   Upgrading a primary or standby will **disable redo apply** during the operation.
*   **Oracle recommends** checking the redo apply and open mode configuration **after** the upgrade process.

### **15. Lesson Summary**
In this lesson, you should have learned how to:
*   Create custom database and Grid Infrastructure images.
*   Create a Database Home.
*   Create a database.
*   Perform pluggable database (PDB) management.
*   Enable Data Guard.
*   Perform user-managed maintenance updates and upgrades.