Of course. Here is the text broken down into structured points without any content removed.

### **1. Introduction & Lesson Objectives**
*   Hello, and welcome. My name is Eddie Ambler.
*   This session continues the discussion on the Exadata Database Service.
*   Focus: Core functionality required to manage the Exadata infrastructure and VM cluster, which form the foundation of the service.
*   After completing this lesson, you should be able to:
    *   Describe the Exadata Database Service management roles and responsibilities.
    *   Describe and schedule Oracle-managed infrastructure maintenance.
    *   Scale Exadata Cloud Infrastructure, VM cluster, and VM cluster resources.
    *   Manage the VM cluster.

### **2. Managing Cloud Exadata Infrastructure: Overview**
*   Management is done at the **infrastructure** and **VM cluster** level.
*   Prerequisite: You must first create the **Exadata infrastructure resource** and the **Exadata VM cluster resource**.
*   Management operations can be run from:
    *   The web console.
    *   REST API.
    *   SDK.
    *   Command-line interface (CLI).
    *   Other tools.
*   **Security:** Access must be granted via an IAM policy by an administrator in the correct compartment.
    *   If you encounter permission errors, validate that the compartment you are working in is set correctly.

### **3. Resource Models**
*   For **X8, X8M, and X9M** instances: Most management operations occur at the **Exadata VM cluster resource** level.
*   For **older Exadata Cloud shapes** using the **DB System Resource model**: All operations take place on the **system resource**.
*   Existing Exadata Cloud shapes using the old DB System Resource model **can be switched** to the new resource model and APIs.

### **4. Management Roles & Responsibilities**
*   Exadata Database Service follows a simple cloud management model.
*   **Oracle owns and manages the infrastructure**, including:
    *   Database servers.
    *   Storage servers.
    *   Internal network fabric.
*   Customers are **not authorized to access the Oracle infrastructure**.
*   You can **schedule a maintenance window** for Oracle to perform infrastructure maintenance that aligns with your business needs.
*   **Customers are responsible** for managing everything that runs **inside the guest VMs** on the Exadata Database servers, which includes:
    *   The virtual machine OS.
    *   The Grid Infrastructure software.
    *   The Database Home layer (database software, customer data, encryption keys).
*   The guest VM runs all supported Oracle Database versions.
*   Customers can install and manage additional software in the guest VM but are **not allowed to modify the kernel RPMs**.
*   Customers are in control of **who can access the guest VM**. Oracle staff is **not authorized** to access the customer's guest VM.

### **5. Cloud Automation Tools**
*   The service provides a powerful set of **cloud automation tools** that give you complete control over the components you need to manage.
*   **Cloud automation UIs and APIs** enable customers to manage VMs and databases.
*   **Cloud automation functions** enable customers to:
    *   Create and delete resources.
    *   Patch resources.
    *   Backup resources.
    *   Scale resources up and down.
    *   Perform other tasks.
*   The efficiency of these tools **frees DBAs** from the burden of traditional Database Management tasks.

### **6. Maintenance Updates: Division of Responsibility**
*   Managing maintenance updates is divided into two sections:
    1.  **Oracle-managed infrastructure maintenance updates**
    2.  **User-managed maintenance updates**

### **7. Oracle-Managed Infrastructure Maintenance**
*   **Oracle is responsible** for applying **quarterly infrastructure updates** to all infrastructure components, including:
    *   Physical compute servers and the root VM.
    *   Exadata storage servers.
    *   Internal switches in the Exadata Secure RDMA Network Fabric.
    *   PDUs (Power Distribution Units).
    *   ILOM (Integrated Lights Out Manager) interfaces, firmware.
    *   Any control plane components.
*   This is referred to as **infrastructure maintenance**.

### **8. User-Managed Maintenance Updates**
*   Maintaining a secure and optimally functioning instance requires you to perform these tasks **regularly**:
    *   Patching the Oracle Grid Infrastructure software.
    *   Patching the Oracle Database software on the Exadata Database VM.
    *   Updating the operating system on the Exadata Database VM.
*   These tasks should be done **quarterly, but not to exceed 180 days** from the last applied patch.
*   To perform these operations, you must be granted security access with the appropriate **IAM policies**.
*   This access is required for all interfaces: web console, REST API, SDK, CLI, or other tools.
*   If you get a permission error, verify your access with a tenancy administrator.

### **9. IAM (Identity and Access Management) Overview**
*   IAM services let you control:
    *   **Who** can access your account.
    *   **What** services and resources they can use.
    *   **How** they can use these resources.
*   A **resource** is an object you create (e.g., a DB system, block storage volume).
*   Five key concepts in IAM:
    1.  **Principles**
    2.  **Users**
    3.  **Groups**
    4.  **Policies**
    5.  **Compartments**
*   **Compartments** are a unique OCI feature used to organize and control access to your resources.
    *   A compartment is a collection of related resources (e.g., cloud networks, DB systems, block volumes).
    *   Access is granted only to groups that have been given permission by an administrator.

### **10. IAM Policies for Management Operations**
*   Proper IAM policies are needed for all management operations discussed in this course.
*   This applies to all OCI management interfaces: console, REST API, SDK, or CLI.
*   Defining IAM policies is intuitive, following a syntax pattern:
    *   **Subject:** Define *who* the policy is for.
    *   **Verb:** Specify *what* they can do.
    *   **Resource Type:** Provide the scope for *where* the permission applies.
*   Using **`database-family`** as an aggregate resource type in a policy grants permissions on **all classes** of databases in OCI, including:
    *   Autonomous Database.
    *   VM DB systems.
    *   The Exadata Database Service (public cloud).
    *   Cloud@Customer.
*   The individual resource types shown are a sample of the **granularity** you can apply to permissions.
