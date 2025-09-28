Of course. Here is the transcript broken down into clear points, preserving every single word as requested.

**Part 1: Introduction and Lesson Objectives**

1.  Hello, this is Tammy Bednar from Oracle.
2.  Today, we're going to take a look at the Oracle Base Database Service Backup and Recovery.
3.  Over the next few minutes, we will review how to make backups, but more importantly, how to restore and recover those backups when it's required.
4.  After completing this lesson, you should be able to describe backup types, describe backup destination choices, configure automatic backups for new and existing databases, list available backups, create on-demand backup, describe database restore options, and understand backup and restore capabilities from standby.

**Part 2: Backup Types**

5.  There are two types of backups available when using the cloud automation for the base database service.
6.  They are the automatic backup and the on-demand backups.
7.  Automatic backups are taken if you select this option for your database.
8.  For this backup type, Oracle automatically takes any required full and weekly backups and sweeps the archive logs to the backup destination every 30 minutes.
9.  Note that if you terminate your database, you can specify how long the backups should be maintained.
10. On-demand backups that are initiated by the end user will persist until they are deleted.

**Part 3: Automation and Capabilities**

11. Oracle Base Database Service provides automatic database backup facilities that use Oracle Recovery Manager or RMAN.
12. The provided cloud automation can be utilized from the UI console or the APIs.
13. You can create a database with automatic backups defined during the Database Create workflow.
14. You can edit backup settings once the database has been created.
15. You can view a list of all available backups.
16. You can create on-demand backups even if you are using automatic backups.
17. And you can create a database from a backup.
18. But more importantly, you can easily use the cloud automation to restore your database as required.

**Part 4: Backup Destination Choices**

19. For the base database service, you have two choices for the backup destination.
20. You can choose from the recovery service or from object storage.
21. The recovery service is the default selection.
22. It offers the same cost point as object storage but has more features and provides restore performance advantages.

**Part 5: Recovery Service Details**

23. The recovery service, whose full name is Zero Data Loss Autonomous Recovery Service, allows OCI customers to automate backups and enable immutability.
24. With the recovery service, the backups are stored outside the customer tenancy.
25. This safeguards against deletion or tampering.
26. Private endpoints are used for connectivity, which establishes secure communication between the recovery service and the database.
27. Our main configurations for backups and restores are automated, ensuring best practices are followed.
28. Backups are always replicated to another availability domain in order to provide high availability.
29. The real-time protection option helps to reduce data loss.
30. And the recovery service also provides a simple automated RMAN restore, which eliminates manual RMAN scripting and DB backup scheduling.

**Part 6: Backup Retention Periods**

31. Backup retention periods are an important part of controlling backup costs and ensuring that you can meet your recovery needs.
32. The default backup retention period varies by the chosen backup destination.
33. For backups to object storage, there is a default of 30 days and a max of 60 days for the retention period.
34. For the recovery service, the assigned backup policy will determine the retention period with a max value of 95 days.
35. For long-term retention backup with recovery service, the retention period should be a minimum of 90 days and a maximum of 3,650 days or 10 years for when the backup was created.
36. Regardless of the backup destination that you choose, backups of data in Oracle cloud databases are encrypted by default.

**Part 7: Backup Scheduling and Strategy**

37. When you choose object storage destination, there is a seven-day database backup cycle.
38. The backup cycle begins with a full backup that is repeated once weekly and daily incremental backups.
39. When you choose recovery service for the backup destination, the need for full backups is eliminated, as it uses an incremental forever strategy.
40. Archived redo log files are backed up every 30 minutes for base DB.

**Part 8: Configuring Automatic Backups**

41. Automatic backups can be defined during or after database creation.
42. Your options for backup destinations, retention period, and the backup scheduling window will be the same as if you enabled it during the database creation workflow.
43. To enable automatic backups for an existing database, you simply need to click the Configure Automatic Backups tab on the Database Details page.
44. Once you select the checkbox to enable database automatic backups, you can then select the desired backup destination.

**Part 9: Configuring with Recovery Service**

45. For the base database service, we are offered a choice of using object storage or the recovery service for a backup destination.
46. If you choose the recovery service for the backup destination, then you will next select the desired protection policy that will define the recovery window that the backup will provide.
47. You can also select the checkbox for real-time data protection if you want to include redo log shipping to the recovery appliance to enable a zero data loss backup service.
48. Note that the real-time data protection option has an additional cost associated to it.
49. You will then select what to do with the database backups once the database is terminated, with the option being to follow the retention period or only keep them for 72 hours after database deletion.
50. Next, you will select a time for your daily incremental backups and choose if you want to immediately take the initial full backup or wait until the defined full backup date and the time comes around.
51. Note that the recovery service initiates one full backup.
52. And after that, only incremental backups are made.

**Part 10: Configuring with Object Storage**

53. Check Enable automatic backups.
54. Choose the object storage for backup destination.
55. Then you will next select the desired backup retention period, which ranges from 7 to 60 days with a 30-day default.
56. If the database is terminated, you have the option to retain the backups based on the retention period or delete them after 72 hours.
57. Next, we will select a day and time for a weekly full backups, followed by a time for the daily incremental backups.
58. Note that just like with recovery service choice, you can choose to immediately take the initial full backup or wait until the defined full backup date and time comes around.
59. During the database creation process, you will be presented with the same choices for enabling automatic backups as we just reviewed.

**Part 11: Listing Available Backups**

60. The OCI Console allows the ability to view all of the automatic and on-demand backups that were taken via the control plane.
61. On the left hand side of the Database Details page under Resources, click Backups, which displays a list of available backups.
62. And you can tell if the backup is an automatic backup or an on-demand backup by looking at its type.

**Part 12: Creating an On-Demand Backup**

63. Let's take a look at how to create an on-demand backup from the UI console.
64. Click the Create Backup button, which will launch the Create Backup dialog box.
65. This is where you can provide the desired name for your backup.
66. And then click on Create Backup button to proceed.
67. These backups will show up in the UI console with the other automatic backups taken.
68. Note how our backup shows up in the backup list with our chosen name and has a state of creating while the backup is in progress.
69. Once the backup completes, the state of the database goes back to Available.
70. And state of the backup will show as Active.
71. Remember that on-demand backups will need to be removed manually if you terminate your database.

**Part 13: Restoring a Database**

72. When you need to restore a base database service instance from a backup, cloud automation makes this a very easy task.
73. From the Database Details page, click Restore.
74. In the Restore Database dialog box that is displayed, you can select one of the following options.
75. Restore to the latest, which restores the database to the last known good state with the least possible amount of data loss.
76. Or we can select Restore to the timestamp, which restores the database to the timestamp specified.
77. Or we can select Restore to a system change number, which restores the database using the SCN specified.
78. You can determine the SCN number to use either by accessing and querying your database or by accessing any online or archived logs.
79. Once you have selected your restore point, then simply click the Restore Database button to proceed.

**Part 14: Backup and Restore from a Standby Database**

80. You can back up and restore from a standby database in a Data Guard association.
81. By using this function, you can offload backups to the standby database in a Data Guard association, thereby freeing up resources in the production database environment.
82. Schedule automatic backups on the standby database in a Data Guard association.
83. And configure retention periods and backup schedules.
84. Create a database in another availability domain within the same region or a different region from a backup of the standby database.
85. Restore and recover a standby database using a backup of the standby database.
86. Take backups only on the primary database, only the standby database, or both primary and standby databases.
87. Enable or disable backup on the standby database only if the backup destination of the primary database is object storage.

**Part 15: Restrictions and Limitations for Standby**

88. In restrictions and limitations, the backup destination of the primary database and standby database in a Data Guard association must be the same.
89. To change the backup destination of the primary database to Autonomous Recovery service, first disable backup on the standby database.
90. For backups in the recovery service, the primary database can be restored or recovered from the backups of either the standby database or the primary database.
91. So similarly, the standby database can be restored or recovered from the backups of either the primary database or the standby database.
92. For backups in object storage, the primary database and standby database can be restored or recovered from their respective backups only.

**Part 16: Conclusion and Review**

93. As you can see from our list, the base database service delivers a full suite of backup and restore features.
94. In this lesson, you should have learned to describe backup types, describe backup destination choices, configure automatic backups for new and existing databases, list available backups, create on-demand backups, describe database restore options, and understand backup and restore capabilities from standby.
