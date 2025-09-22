### **1. Module Overview: Getting Started with MySQL HeatWave**
*   We describe how to get started with MySQL HeatWave.
*   We will start with an overview of what is required for a working MySQL HeatWave system.
*   We will go over the steps and reasons for creating the database system.
*   We will finish by going over the methods for connecting and using the new MySQL HeatWave system.

### **2. Oracle Cloud Infrastructure (OCI) & MySQL HeatWave**
*   Oracle Cloud Infrastructure is a set of complementary cloud services.
*   It makes it easy for you to build and run a wide range of applications and services in a highly available hosted environment.
*   MySQL HeatWave relies on several of those services.
*   You can create and access Oracle Cloud Infrastructure MySQL HeatWave using:
    *   The console (browser-based interface).
    *   The REST API.
*   This presentation focuses on the console method.

### **3. Prerequisites for Creating a MySQL HeatWave System**
*   You need an Oracle Cloud account and an OCI cloud tenancy.
*   From the OCI tenancy, you should be able to sign in to the OCI console with a valid user account.
*   ==You need to have a compartment to store the database system resources.==
*   ==Your user account must belong to a group that has been granted mandatory policies for MySQL HeatWave.==
*   ==You need to set up the virtual cloud network (VCN) for your database system.==
*   **Next Step:** Create a virtual cloud network by using the VCN Wizard.

### **4. Database System Components**
*   A database system is a logical container for the MySQL HeatWave instance.
*   It provides an interface-enabling management of tasks (provisioning, backup and restore, monitoring, etc.).
*   It provides a read-write endpoint for connecting to the MySQL instance using standard protocols.
*   A MySQL HeatWave database system consists of:
    *   A compute instance.
    *   An Oracle Linux operating system.
    *   The latest version of MySQL Server Enterprise Edition.
    *   A virtual network interface card (attaches the DB system to a VCN subnet).
    *   A network-attached higher performance block storage.

### **5. System Framework Diagram Description**
*   The framework is inside an Oracle Cloud Infrastructure region (e.g., Tokyo).
*   The system is in one data center, called an Availability Domain.
*   It uses one Virtual Cloud Network (VCN).
*   The VCN is divided into two subnets: a public subnet and a private subnet.
*   The Oracle Linux computer is on the public subnet.
*   The MySQL HeatWave instance is on the private subnet.
*   The user accesses MySQL HeatWave with SSH via the Linux computer.

### **6. Provisioning Your MDS DB System: Three Major Tasks**
After logging into the OCI console, you need to:
1.  Access your database system basics.
2.  Create your MySQL database instance.
3.  Create your compute instance.

### **7. Database System Basics**
*   **Compartment:** A compartment to store your resources should be created. Find it under **OCI Identity > Compartments**.
*   **Policies:** MySQL policies should be created to control access. Find them under **OCI Identity > Policies** (typically on the root compartment).
*   **VCN:** A Virtual Cloud Network for the system should be created. Find it under **OCI Networking > Virtual Cloud Networks**.

### **8. Creating a Standalone Database System: Step-by-Step**
1.  Use the console menu to go to **MySQL Database Systems**.
2.  Click the **Create Database System** button.
3.  On the create page, select the **Development or Testing** option.
4.  **Provide Basic Information:**
    *   **Compartment:** Select the compartment from the dropdown list.
    *   **Name:** Enter a user-friendly display name (does not need to be unique; an OCID uniquely identifies it).
    *   **Description:** Enter a description of the database system and its purpose.
5.  **Select Deployment Type:** Select the **Standalone** option for a single instance.
6.  **Enable** Configure MySQL HeatWave.
7.  **Create Administrator Credentials:**
    *   Enter a username for the administrator user (do not use reserved names like `mysql.sys`).
    *   Enter and confirm a valid password.
8.  **Configure Networking:**
    *   Select the required VCN.
    *   Select the **private subnet** of the selected VCN.
9.  **Configure Placement:**
    *   Keep **Availability Domain** selected.
    *   Do *not* select "Choose a fault domain."
10. **Configure Hardware:**
    *   Select a shape (determines allocated resources). Keep the default for now.
    *   Set the **Data Storage Size** (amount of block storage in GB). Keep the default.
11. **Configure Backups:**
    *   Select to **Enable scheduled backups** (strongly recommended).
    *   Set the **Retention period** (how long to retain backups in days). Default is 7.
    *   Select a **Backup window** (time when backup is initiated). Select the default.
12. Click the **Create** button.
13. The state will show as **Creating** (yellow icon) and then change to **Active** (green icon) when ready.

### **9. Creating a Client Compute Instance**
*   To launch a Linux compute instance, go to **Compute > Instances**.
*   Click **Create Instance**.
*   Enter an instance name and ensure the correct compartment is selected.
*   Keep the default **Oracle Linux** image.
*   For placement and hardware, keep the default Availability Domain and instance shape.
*   For the VCN, select the **same VCN** as the MySQL database system.
*   Set **Assign a public IP address** to **Yes**.
*   Generate an SSH key or add your existing SSH key.
*   Click **Create**.
*   The instance state **Running** (green) indicates it is ready.

### **10. Connecting to the MySQL Database**
**Required Steps:**
1.  Set up VCN access for MySQL port 3306.
2.  Connect to MDS using MySQL client tools.
3.  Alternatively, connect using MySQL Workbench.
4.  Load data into the MySQL database.

**Step 1: Configure Network Security Rules**
*   Use the console menu to go to **Networking > Virtual Cloud Networks**.
*   Click on the VCN you are using.
*   Select **Security Lists** from the Resources section.
*   Click **Add Ingress Rules**.
*   Configure the ingress rule:
    *   **Stateless:** Do *not* select.
    *   **Source Type:** CIDR.
    *   **Source CIDR:** The CIDR of the public subnet (can be narrowed to specific IPs).
    *   **IP Protocol:** TCP.
    *   **Source Port Range:** (Leave blank).
    *   **Destination Port Range:** 3306 (for MySQL classic) or 33060 (for MySQL X protocol).

**Step 2: Connect via MySQL Client**
*   From a terminal, connect to the compute instance via SSH.
*   Install the MySQL client package and MySQL Shell on the client instance.
*   From the compute instance, connect to MySQL using MySQL Shell.
    *   The endpoint IP address is found on the MySQL DB System Details page under **Endpoints > Resource Address**.

**Step 3: Connect via MySQL Workbench (from local machine)**
*   Configure a connection using **Standard TCP/IP over SSH**.
*   **SSH Connection Details:**
    *   **SSH Hostname:** Public IP address of the client (compute) instance.
    *   **SSH Username:** `opc`
    *   **SSH Key File:** Path to your SSH private key.
*   **MySQL Connection Details:**
    *   **MySQL Hostname:** IP address of the MySQL endpoint.
    *   **MySQL Server Port:** Port the MySQL endpoint is listening on (e.g., 3306).
    *   **Username & Password:** The administrator credentials defined during DB system creation.
*   Click **Test Connection** to validate.

### **11. Testing the System**
*   Download and import the `Sakila` sample database to test features like views, stored procedures, and triggers.
*   Check the **Oracle Cloud Infrastructure MySQL HeatWave documentation site** to learn more.
### **12. Summary**
*   In this module, we configured a Virtual Cloud Network (VCN).
*   We created a compute instance to be used as a bastion host.
*   We created the DB system.
*   We looked at several ways to connect to the newly created system.