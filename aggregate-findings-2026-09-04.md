# RefRep Aggregate Findings

Reporting interval: 2025-09-04 (inclusive) through 2026-09-04 (exclusive)

## KPI summary

| Metric | Value |
| --- | --- |
| Projects | 670 |
| Timing events | 8580 |
| Failed events | 3164 |
| Failed-event rate | 36.9% |
| Recognized taxonomy matches | 2986 |
| Taxonomy coverage | 94.4% |
| Unmapped failure events | 178 |
| Total failed-step runtime | 3506:50:38 |
| Median completed-project elapsed | 61:12:10 |
| P90 completed-project elapsed | 217:30:48 |
| Failure runtime / completed-project elapsed | 6.6% |
| Workflow-deviation rate | 94.7% |
| Unclassified inter-step elapsed | 60196:07:17 |

## Top error codes by failed runtime

| Category | Description | Failed event count | Failed runtime |
| --- | --- | ---: | ---: |
| RR-1006 | CCL-E-284 ORA-00942 Table or view does not exist | 35 | 1566:51:54 |
| RR-1056 | Errors encountered during remote export/import operations | 767 | 1297:00:59 |
| RR-9999 | Unmapped failed-event message; requires taxonomy review | 178 | 266:12:59 |
| RR-1090 | One or more errors were encountered executing DDL. | 251 | 225:56:21 |
| RR-1113 | SCP Unabel to start server or server failed to start. | 391 | 72:10:54 |

## Top error codes by occurrence

| Category | Description | Failed event count | Failed runtime |
| --- | --- | ---: | ---: |
| RR-1056 | Errors encountered during remote export/import operations | 767 | 1297:00:59 |
| RR-1113 | SCP Unabel to start server or server failed to start. | 391 | 72:10:54 |
| RR-1068 | Error during database shell creation. | 260 | 03:27:39 |
| RR-1090 | One or more errors were encountered executing DDL. | 251 | 225:56:21 |
| RR-1067 | Error occurred during execution of dm2_expimp_setup.ksh on remote Target database node | 225 | 00:41:08 |

## Lifecycle counts

| Lifecycle state | Project count |
| --- | ---: |
| COMPLETED | 504 |
| IN_FLIGHT | 1 |
| REVIEW_REQUIRED | 165 |

## Workflow assessment counts

| Workflow assessment state | Project count |
| --- | ---: |
| ASSESSED | 548 |
| UNASSESSED | 122 |

## Workflow-deviation counts

| Workflow deviation kind | Finding count |
| --- | ---: |
| MISSING_REQUIRED_ORDERED_STEP | 414 |
| OUT_OF_ORDER_EXPECTED_STEP | 59 |
| REPEATED_NON_REPEATABLE_ORDERED_STEP | 2214 |

## Failure-duration rollups

| Category | Description | Lifecycle state | Failed event count | Failed runtime |
| --- | --- | --- | ---: | ---: |
| RR-1000 | General error - no event message available | COMPLETED | 5 | 00:12:20 |
| RR-1001 | Value specified in tnsnames.ora does not match target TNS entry | COMPLETED | 2 | 00:00:04 |
| RR-1006 | CCL-E-284 ORA-00942 Table or view does not exist | COMPLETED | 11 | 00:13:12 |
| RR-1007 | CCL-E-284 ORA-01017 Invalid username/password; logon denied | COMPLETED | 4 | 00:03:08 |
| RR-1011 | CCL-E-284 ORA-02019 Connection description for remote database not found | COMPLETED | 39 | 00:01:40 |
| RR-1031 | CCL-E-288 ORA-00001 unique constraint violated | COMPLETED | 3 | 00:06:15 |
| RR-1039 | CCL-E-49 This user already exists | COMPLETED | 34 | 00:27:48 |
| RR-1040 | CCL-E-55 This user-authorization-file cannot be found in the dictionary | COMPLETED | 1 | 00:00:51 |
| RR-1043 | Cannot start process from beginning, operations still in RUNNING status | COMPLETED | 17 | 03:21:38 |
| RR-1044 | CCL security login failed | COMPLETED | 6 | 00:00:18 |
| RR-1045 | CCLDIR should be set to point to CCLDIR1 directory | COMPLETED | 2 | 00:01:03 |
| RR-1046 | CCLDIRACCESS should be set to 1WRITE | COMPLETED | 1 | 00:00:17 |
| RR-1052 | Copy error. No space left on device. | COMPLETED | 18 | 00:14:58 |
| RR-1056 | Errors encountered during remote export/import operations | COMPLETED | 682 | 1173:20:57 |
| RR-1058 | Expected files to backup not found | COMPLETED | 11 | 04:29:22 |
| RR-1060 | Failed to modify Server property | COMPLETED | 141 | 07:33:11 |
| RR-1061 | Unable to open shared memory section hnam_domain_table | COMPLETED | 14 | 02:30:41 |
| RR-1062 | FTP connection error. Host key verification failed. Connection reset by peer. | COMPLETED | 65 | 00:06:03 |
| RR-1063 | Error exporting TARGET server definitions. Server definitions export does not exist. | COMPLETED | 35 | 01:34:58 |
| RR-1066 | Error occurred during execution of dm2_expimp_cleanup.ksh on remote Target database node | COMPLETED | 116 | 00:10:51 |
| RR-1067 | Error occurred during execution of dm2_expimp_setup.ksh on remote Target database node | COMPLETED | 202 | 00:38:11 |
| RR-1079 | History found for Target environment/id. Defined environment cannot be used for TARGET environment. | COMPLETED | 2 | 00:00:06 |
| RR-1080 | Host does not exist in Target Node List | COMPLETED | 4 | 00:09:52 |
| RR-1082 | Incorrect SCP export file layout. | COMPLETED | 10 | 00:47:00 |
| RR-1090 | One or more errors were encountered executing DDL. | COMPLETED | 196 | 217:18:00 |
| RR-1094 | RDBMS Password property not found with the associated RDBMS User Name property. | COMPLETED | 8 | 02:59:44 |
| RR-1098 | SCP Server differences exist between SOURCE and TARGET. | COMPLETED | 25 | 01:17:36 |
| RR-1102 | Unable to perform SCP command. Authorize server is not running. | COMPLETED | 113 | 09:10:03 |
| RR-1103 | Authorize server is not running. | COMPLETED | 17 | 01:21:55 |
| RR-1104 | Unable to perform Server Controller Viwer command. | COMPLETED | 42 | 05:54:14 |
| RR-1106 | SOURCE database node temporary directory not found on SOURCE database node. | COMPLETED | 14 | 00:01:45 |
| RR-1108 | SOURCE host does not have a corresponding target mapped node in response file. | COMPLETED | 1 | 00:00:01 |
| RR-1113 | SCP Unabel to start server or server failed to start. | COMPLETED | 353 | 65:11:45 |
| RR-1115 | Unable to untar warehouse. No space left on device. | COMPLETED | 16 | 04:17:06 |
| RR-1119 | The account provided does not have required privileges. | COMPLETED | 32 | 01:23:28 |
| RR-1125 | Unable to assign server numbers for all OpsExec control groups | COMPLETED | 5 | 00:17:35 |
| RR-1128 | Unable to obtain environment_id. | COMPLETED | 7 | 00:00:35 |
| RR-1129 | V500 user is currently connected. | COMPLETED | 23 | 03:50:03 |
| RR-9999 | Unmapped failed-event message; requires taxonomy review | COMPLETED | 135 | 08:10:32 |
| RR-1001 | Value specified in tnsnames.ora does not match target TNS entry | REVIEW_REQUIRED | 7 | 00:01:18 |
| RR-1006 | CCL-E-284 ORA-00942 Table or view does not exist | REVIEW_REQUIRED | 24 | 1566:38:42 |
| RR-1032 | CCL-E-296 Query interrupted by control-c or timeout of 0 seconds | REVIEW_REQUIRED | 10 | 00:06:55 |
| RR-1040 | CCL-E-55 This user-authorization-file cannot be found in the dictionary | REVIEW_REQUIRED | 4 | 00:03:20 |
| RR-1051 | Could not detect o/s via ssh 'uname' command or value returned invalid. | REVIEW_REQUIRED | 2 | 00:00:03 |
| RR-1056 | Errors encountered during remote export/import operations | REVIEW_REQUIRED | 85 | 123:40:02 |
| RR-1061 | Unable to open shared memory section hnam_domain_table | REVIEW_REQUIRED | 3 | 00:33:39 |
| RR-1062 | FTP connection error. Host key verification failed. Connection reset by peer. | REVIEW_REQUIRED | 4 | 00:00:13 |
| RR-1067 | Error occurred during execution of dm2_expimp_setup.ksh on remote Target database node | REVIEW_REQUIRED | 23 | 00:02:57 |
| RR-1068 | Error during database shell creation. | REVIEW_REQUIRED | 260 | 03:27:39 |
| RR-1088 | Failed to connect to database | REVIEW_REQUIRED | 82 | 08:34:58 |
| RR-1089 | Connected to database node, but database name/host name not as expected. | REVIEW_REQUIRED | 13 | 00:00:27 |
| RR-1090 | One or more errors were encountered executing DDL. | REVIEW_REQUIRED | 55 | 08:38:21 |
| RR-1099 | SCP SOURCE node list count does not match node count in response file. | REVIEW_REQUIRED | 1 | 00:00:25 |
| RR-1103 | Authorize server is not running. | REVIEW_REQUIRED | 1 | 00:05:01 |
| RR-1106 | SOURCE database node temporary directory not found on SOURCE database node. | REVIEW_REQUIRED | 18 | 00:08:06 |
| RR-1107 | SOURCE environment history summary files could not be found in temporary directory provided. | REVIEW_REQUIRED | 1 | 00:00:03 |
| RR-1111 | SSH command did not return the expected node. | REVIEW_REQUIRED | 9 | 00:00:21 |
| RR-1113 | SCP Unabel to start server or server failed to start. | REVIEW_REQUIRED | 38 | 06:59:09 |
| RR-1115 | Unable to untar warehouse. No space left on device. | REVIEW_REQUIRED | 17 | 01:33:55 |
| RR-1117 | TARGET database node temporary directory not found on TARGET database node. | REVIEW_REQUIRED | 2 | 00:00:04 |
| RR-1119 | The account provided does not have required privileges. | REVIEW_REQUIRED | 5 | 00:04:25 |
| RR-1121 | Unable to validate managed acccount provided. | REVIEW_REQUIRED | 3 | 00:00:51 |
| RR-1126 | Unable to find checkpoint file. | REVIEW_REQUIRED | 5 | 00:00:55 |
| RR-1132 | Unable to verify successful execution of script. | REVIEW_REQUIRED | 37 | 10:47:16 |
| RR-9999 | Unmapped failed-event message; requires taxonomy review | REVIEW_REQUIRED | 43 | 258:02:27 |
