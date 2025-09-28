Of course. Here is the transcript broken down into clear points, preserving every single word as requested.

**Part 1: Starting, Stopping, and Rebooting DB System Nodes**

1.  Start, stop, reboot system nodes-- To use the console to start, stop, and reboot a virtual machine DB system.
2.  Find the DB system you want to stop, start or reboot the VM node for.
3.  On the left side of the DB Systems Detail page, under Resources, you will find the link to display the DB system VM nodes.
4.  In the list of nodes displayed, click the Actions icon, which is the three dots on the far right for the desired node, and then select one of the following options.
5.  Start, start restarts a stop node.
6.  After the node is restarted, the Stop action is enabled.
7.  Stop shuts down the node and after the node is powered off, the Start action is enabled.
8.  Reboot shuts down the node and then restarts it.
9.  Note that for two-node rack DB systems you must start, stop, and reboot each node individually.

**Part 2: Introduction to PDB Management**

10. So far, we have been dealing with things at the DB system in the container database level.
11. In this section, we will be going over PDB management tasks.
12. With the base database service DB system deployment, a single CDB with a single PDB is created by default when a DB system is created.
13. After a DB system is created with a container database, you can use the console or APIs for PDB lifecycle management.
14. From within the existing container database, you can create and delete a PDB.
15. You can also conduct other lifecycle tasks like start, stop, and clone a new PDB into an existing CDB.

**Part 3: Creating a New Pluggable Database (PDB)**

16. To create another PDB in an existing DB system, CDB, find the DB system in which you want to create the PDB.
17. Click the database name to display details about it.
18. On the left side, under Resources of the Database Details page, click Pluggable Databases.
19. Click Create Pluggable Database and enter the following inputs into the dialog box.
20. Enter your desired PDB name and the admin password, and click Create Pluggable Database to proceed.
21. After the new PDB is provisioned, it will be displayed in the list of available PDBs as shown.

**Part 4: PDB Details Page and Cloning a PDB**

22. From the Pluggable Database Details page, you can perform the following.
23. You can easily launch the SQL worksheet to work with your application data.
24. You can also open the Performance Hub to check on the performance of your application SQLs.
25. If you need another copy of your database, the base database service makes it very easy to clone your PDB.
26. If you click the Clone tab on the Pluggable Database Details page, it will launch the Clone Pluggable Database page where you can enter the information required to build the clone you need.
27. From the Clone Pluggable Database page, you are presented with options for the type of clone that you can create to meet your requirements.
28. You can create a local PDB clone, which creates a PDB within the same container database as the source PDB.
29. You can also create a remote PDB clone, which creates a PDB in a different container database than the source PDB.
30. And you can also create a refreshable PDB clone, which creates a PDB in a different container database than the source PDB, whose data can easily be refreshed using the Refresh function found under the More Actions tab.
31. Once you have selected the type of clone you need, select the DB system and database for the clone destination and enter the remaining information requested to configure the new pluggable database.

**Part 5: Using the More Actions Tab for PDB Lifecycle Tasks**

32. The More Actions tab allows you to be able to conduct additional PDB lifecycle and operational tasks.
33. From the More Actions tab, you can conduct tasks like start and stop a PDB.
34. Clicking Start or Stop from the More Actions tab, launches the dialog box to confirm that you want to proceed with the action, or cancel the operation requested.
35. You can also relocate and restore a PDB.
36. To relocate a PDB, in the More Actions tab, choose Relocate, which will launch the Relocate Pluggable Database page.
37. In the Relocate Pluggable Database page, enter the name of the destination DB system and the new PDB name and password and click Relocate Pluggable Database to proceed.
38. Note that you can use the same PDB name or change it as part of the relocate PDB process.
39. To restore a PDB, in the More Actions tab of the PDB you want to restore, choose Restore.
40. In the Restore PDB dialog box that is displayed, choose if you want to restore the PDB to the latest backup or to a specific point in time.
41. And then click Restore to proceed.
42. Deleting a PDB is also a simple operation that can be done from the More Actions tab.
43. Just choose Delete.
44. And in the dialog box displayed, confirm that you want to proceed with the action or cancel the Delete PDB request.

**Part 6: Terminating a DB System**

45. Terminate DB system-- When terminating a VM database system, it is important to note that the database data will be lost when the system is terminated.
46. Oracle recommends that you back up any data in the virtual machine DB system prior to terminating it.
47. Terminating a DB system removes all automatic incremental backups of the system from Oracle Cloud Infrastructure object storage.
48. Full on-demand backups remain in object storage as standalone backups.
49. Another important thing to be aware of is that you cannot terminate a primary database that has an Oracle Data Guard association with a pure standby database.
50. You must first remove the standby database association by terminating the standby database before you can terminate the primary database.
51. Alternatively, you can switch over the primary database to the standby role and then terminate it.
52. To terminate a VM database system, in the list of DB systems, find the DB system you want to terminate.
53. Click the Actions icon, the three dots, and then click Terminate.
54. Confirm when prompted.
55. The DB systems icon now indicates a status of terminating.
56. At this point, you cannot connect to the system.
57. And any open connections will be terminated.

**Part 7: Lesson Summary**

58. In this lesson, you should have learned how to display Base Database Service DB system and database details, scale OCPUs and storage resources, create database from backup, clone a Base Database Service DB system, enabled Data Guard, start, stop, and reboot a Base Database Service DB system node, manage PDB on Base Database Service, and terminate a Base Database Service DB system.
