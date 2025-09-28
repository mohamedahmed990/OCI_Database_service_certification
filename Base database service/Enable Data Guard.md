**Part 1: Introduction to Data Guard**

1.  Enable Data Guard-- Oracle Data Guard is a central component of an integrated Oracle Database high-availability solution set that helps organizations ensure business continuity by minimizing the various kinds of planned and unplanned downtime that can affect their businesses.
2.  Data Guard automates the process of maintaining a copy of an Oracle primary database, called a standby database, that can be used if the primary database is taken offline for routine maintenance or becomes damaged.

**Part 2: Data Guard Roles and Licensing**

3.  With Data Guard, a database operates in one of two mutually exclusive roles-- Primary or Standby.
4.  In a Data Guard configuration, a production database is referred to as a primary database.
5.  A standby database is a synchronized copy of the primary database.
6.  The standby databases together with the primary database make up a Data Guard configuration.
7.  Your Oracle Enterprise Edition license includes the right to use Oracle Data Guard to create your physical standby database, which is in a mounted state in Active Recovery mode.
8.  Data Guard is not supported with Oracle Database Standard Edition.
9.  Oracle Active Data Guard is a licensed database feature that enables a physical standby database to receive and apply Redo while it is open in Read Only mode.
10. This feature allows for the offloading of activities such as recording and backups, and requires the use of the Enterprise Edition Extreme Performance license tier.
11. Active Data Guard provides additional features including Real-Time Query and DML Offload, Automatic Block Repair, Standby Block Change Tracking, Far Sync, Global Data Services, and Application Continuity.

**Part 3: Configuration and Network Topology**

12. In the cloud, the Base Database Service UI and APIs allow you to configure one standby database per database.
13. When needed, you can manually create multiple standby databases to meet your business needs.
14. Let's take a look at the Oracle Cloud Network topology with Data Guard.
15. To set up Oracle Data Guard within a single region, the primary and standby DB systems of the Base Database Service must use the same VCN.
16. The primary and standby databases should be on separate availability domains, which are independent data centers with low latency between them that allow for SYNC Data Guard replication.
17. The database on the primary and standby can have the same name but must have a different database unique name.
18. If you want to configure Oracle Data Guard across regions, then you must configure Remote Virtual Cloud Network VCN Peering between the primary and standby databases.
19. The selected regions that will host your Base Database Service instance should have comparable latency from the applications and the Customer Data Center to meet any required business continuity or disaster recovery needs.
20. You will need to configure the security list ingress and egress rules for the subnets of the primary and standby DB systems in the Data Guard association to enable TCP traffic to move between the application ports.
21. You can choose regions in the same country or areas-- for example, Ashburn and Phoenix-- to provide comparable latency from customer on-premises applications that are suitable for business continuity and disaster recovery.
22. You could also choose regions in different areas-- for example, cross-country or cross-continent-- that are suitable for disaster recovery or customers with global on-premises locations.
23. It leverages VCN Peering with ASYNC replication to accommodate for latency due to distance.

**Part 4: Benefits of Data Guard and Active Data Guard**

24. Continuous service-- with the use of switchover and failover between systems, your business does not need to halt because of a disaster at one location.
25. Data protection-- Data Guard guarantees that there is no data loss and provides a safeguard against physical data corruption and user errors.
26. Reading data is validated when applied to the standby database.
27. Elimination of idle standby systems, flexible configurations-- you can use Data Guard to configure the system to your needs by using the protection modes and tunable parameters.
28. And centralized management-- you can use the Control Plane using UI or API to create and manage all Data Guard associations and configurations.
29. Active Data Guard provides all of the benefits of Data Guard plus the following additional benefits.
30. Elimination of idle standby systems by providing read-only, real-time data access-- standby databases can be used for reporting and A-D H-O-C queries, in addition to providing a safeguard for disaster recovery.
31. Providing elimination of idle standby systems-- ability to offload reporting queries to standby, ability to offload backups to standby, ability to leverage the Snapshot Standby functionality.

**Part 5: Role Transitions: Switchover, Failover, and Reinstate**

32. Data Guard enables you to change the role of a database.
33. It supports two role transition operations.
34. The Switchover operation is used for planned role reversal and enables you to switch the role of the primary database to one of the available standby databases.
35. The chosen standby database becomes the primary database, and the original primary database then becomes a standby database.
36. This feature is used to reduce downtime from planned operations such as OS or hardware maintenance and database software patching.
37. The Failover operation is used for unplanned role reversal.
38. You invoke a failover operation when a catastrophic failure occurs on the primary database.
39. During a failover operation, the failed primary database is removed from the Data Guard environment, and a standby database assumes the primary database role.
40. You invoke the failover operation on the standby database that you want to fail over to the primary role.
41. You can also manually configure fast-start failover, which allows Data Guard to automatically and quickly fail over to a previously chosen synchronized standby database.
42. The Reinstate operation is used to return a failed database into service as standby in the Oracle Data Guard association after correcting the cause of failure.

**Part 6: Data Guard Protection Modes**

43. Data Guard provides high-level modes of data protection that you can configure to balance cost, availability, performance, and transaction protection.
44. You can configure the Data Guard environment to maximize data protection, availability, or performance.
45. You can configure the Data Guard environment to maximize data protection, availability, or performance.
46. Maximum performance-- default.
47. The default protection mode provides the highest possible level of data protection without affecting the performance of the primary database.
48. This is accomplished by allowing a transaction to commit as soon as the redo data needed to recover that transaction is written to the local online redo log.
49. Redo data is also written to the standby database asynchronously so that the primary database's performance is unaffected by the time required to transmit redo data and receive acknowledgment from the standby database.
50. When you select Maximum Availability protection mode, this protection mode provides the highest possible level of data protection without compromising the availability of the primary database.
51. If the primary database does not receive acknowledgment from at least one synchronized standby that has received the standby redo, then it operates as if it were in maximum performance mode to preserve the primary database availability.

**Part 7: Synchronous Redo Transport and Data Loss Scenarios**

52. Synchronous Redo Transport is used with the Maximum Availability protection mode.
53. If the primary database fails, the amount of data loss depends on the Redo Transport configuration.
54. In the Maximum Availability mode, under normal operations, transactions do not commit until all redo data needed to recover those transactions has been written to the online redo log, and based on user configuration for Log_Archive_Dest, one of the following is true-- redo has been received at the standby, input/output to the standby redo log has been initiated and acknowledgment sent back to the primary, redo has been received and written to standby redo log at the standby and acknowledgment sent back to primary.
55. When a transport is performed using SYNC/AFFIRM, the primary performs write operations and waits for acknowledgment that the redo has been transmitted synchronously to the physical standby and written to disk.
56. A SYNC/AFFIRM transport provides an additional protection benefit at the expense of a performance impact caused by the time required to complete the input/output to the standby redo log.
57. When a transport is performed using SYNC/NOAFFIRM, the primary performs write operations and waits only for acknowledgment that the data has been received on the standby, not that it has been written to disk.
58. The SYNC/NOAFFIRM transport can provide a performance benefit at the expense of potential exposure to data loss in a special case of multiple simultaneous failures.
59. With those definitions in mind, suppose you experience a catastrophic failure at the primary site at the same time that power is lost at the standby site.
60. Whether data is lost, it depends on the transport mode being used.
61. In the case of SYNC/AFFIRM, in which there is a check to confirm that data is written to disk on the standby, there would be no data loss, because the data would be available on the standby when the system was recovered.
62. In the case of SYNC/NOAFFIRM, in which there is no check that data has been written to disk on the standby, there may be some data loss.

**Part 8: Enabling Data Guard via Cloud Automation**

63. Enabling Oracle Data Guard on a DB system using the cloud automation from the UI or API is a very simple process.
64. When you enable Oracle Data Guard for the DB system, a Data Guard association is created for the primary and the standby databases.
65. Creating a Data Guard will create a new DB system for the standby database.
66. Using the UI console, navigate to the DB system's page, and select the DB system you want to create a Data Guard for.
67. Click the name of the database, which will display the Database Details page, as shown here.
68. In the database information, you will find a Data Guard section.
69. Note that the current status for this database says Not Enabled.
70. On the left side, under Resources, you will find the Data Guard Associations link.
71. If the database had a Data Guard already, it would show a count of 1.
72. If you click Data Guard Associations, you will be shown the Enable Data Guard button.
73. Simply select this button to start the Enable Data Guard workflow, where you will enter the details required to create the peer DB system that will host the standby database.
