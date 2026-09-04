# OLAM Jira Epic Skeleton: RefRep Checks and Evidence Collection

## Status and intent

Draft for team review. This is a complete planning skeleton, not authorization
to create Jira issues or configure OLAM. The former 16 stories are parent work
packages, not a limit on the number of atomic check tasks.

```text
Epic: OLAM adoption: RefRep validation and evidence collection
├── Foundation and safety
├── Atomic read-only checks
├── Controlled evidence capture
├── RefRep prereq certification
├── Manual-runbook mining
└── Sensitive-output and remediation decisions
```

## Rules for every implementation task

- One job, one purpose, one result contract, and stated non-responsibilities.
- Pre/post is a launch context, not a reason to recreate an overloaded wrapper.
- A validation job never retrieves, displays, persists, or emails a secret.
- Capture, notification, Jira integration, remediation, and restore actions
  have separate tasks and permissions.

## Foundation tasks

| Placeholder | Task | Completion evidence |
| --- | --- | --- |
| FND-01 | Organizations, teams, and role model | Least-privilege operator, maintainer, auditor, and approver roles |
| FND-02 | Inventory and environment taxonomy | Source/target groups, labels, node ownership, production boundary |
| FND-03 | Execution environment policy | Approved runtime image, dependencies, and command policy |
| FND-04 | Credential-reference model | Non-secret reference categories and access assignment only |
| FND-05 | Result and severity schema | PASS, FAIL, WARN, UNKNOWN, BLOCKED contracts |
| FND-06 | Artifact/redaction/retention policy | Storage, retention, access, sanitization, and cleanup rules |
| FND-07 | Notification and APEX handoff policy | Routing, deduplication, callback/consumption model, no-Jira-write default |
| FND-08 | Naming and workflow-composition standard | Single-purpose names and verified dependency rules |

## Atomic node-validation tasks

**Parent: MOD-NODE-00 – Decompose `node_checks.sh` into reusable jobs.**

| Placeholder | Atomic job | Notes |
| --- | --- | --- |
| NODE-01 | Host identity and inventory membership | FQDN and expected host group |
| NODE-02 | OS and kernel inventory | Informational unless policy sets supported versions |
| NODE-03 | Uptime observation | Threshold only if separately accepted |
| NODE-04 | Oracle client version | Executable and version result |
| NODE-05 | Java version | Executable and version result |
| NODE-06 | Filesystem capacity | Confirm threshold before implementation |
| NODE-07 | CPU utilization | Confirm threshold before implementation |
| NODE-08 | Swap utilization | Confirm threshold before implementation |
| NODE-09 | MQ software version | Version/platform observation |
| NODE-10 | MQ process status | Independent service result |
| NODE-11 | MQ listener status | Expected queue-manager/listener mapping |
| NODE-12 | Cluster status | Return not-applicable where clustering is absent |
| NODE-13 | Server controller status | Process/service state |
| NODE-14 | Registry service status | Process/service state |
| NODE-15 | ESM/Sentinel status | Process/service state |
| NODE-16 | Chef run health | Define log freshness and expected completion |
| NODE-17 | Cohesity agent status | Return not-applicable where unmanaged |
| NODE-18 | Running-domain observation | Host-scoped observation only |
| NODE-19 | Netrics cache consistency | Explicit data access and drift threshold required |
| NODE-20 | Nightly-refresh cron presence | Validate schedule, not execution success |
| NODE-21 | SSH reachability | Read-only test, no key setup or host-key bypass |
| NODE-22 | ASM capacity | Target disk groups and free-space rules required |
| NODE-23 | SCP dead-server count | Structured count and severity threshold |

## Compatibility, configuration, and endpoint tasks

| Placeholder | Parent or atomic task | Source | Boundary |
| --- | --- | --- | --- |
| MOD-COMP-00 | Parent: source/target compatibility | `packg_check.sh` | Comparison-only module |
| COMP-01 | Millennium version comparison | `packg_check.sh` | Mismatch severity defined |
| COMP-02 | Install Tools release comparison | `packg_check.sh` | Mismatch severity defined |
| COMP-03 | Install Tools package comparison | `packg_check.sh` | Mismatch severity defined |
| COMP-04 | Domain Management release comparison | `packg_check.sh` | Mismatch severity defined |
| COMP-05 | Domain Management package comparison | `packg_check.sh` | Mismatch severity defined |
| MOD-URL-00 | Parent: application URL validation | CCL/SCP and postcheck sources | Sanitized output only |
| URL-01 | MPage configured domain check | `check_mpage_url.sh` | Expected-domain contract |
| URL-02 | MPage HTTP reachability | `check_mpage_url.sh` | Accepted response/TLS policy |
| URL-03 | CAMM URL configuration | `ccl_scp_checks.sh` | Redacted configuration value |
| URL-04 | Service and XR URL configuration | `ccl_scp_checks.sh` | Redacted configuration value |
| URL-05 | Orion embedded URL configuration | `ccl_scp_checks.sh` | Redacted configuration value |
| URL-06 | Content-service URL configuration | `ccl_scp_checks.sh` | Redacted configuration value |
| MOD-LDAP-00 | Parent: LDAP/security-hosting validation | `check_ldap.sh` | Reusable pre/post components |
| LDAP-01 | Security-service model detection | `check_ldap.sh` | Classification result |
| LDAP-02 | LDAP enabled-state validation | `check_ldap.sh` | Expected state per environment |
| LDAP-03 | LDAP SRV resolution | `check_ldap.sh` | DNS protocol/port result |
| LDAP-04 | LDAP audit URL/port agreement | `check_ldap.sh` | No sensitive audit output retained |
| LDAP-05 | LDAP referral setting | `check_ldap.sh` | Explicit policy needed |
| LDAP-06 | Pre/post security-hosting comparison | `check_ldap.sh` | Sanitized pre-evidence required |

## Evidence, comparison, and TNS tasks

| Placeholder | Parent or atomic task | Source | Boundary |
| --- | --- | --- | --- |
| MOD-EVID-00 | Parent: paired evidence | `get_inst_cnt.sh` | Capture and compare remain separate |
| EVID-01 | Pre-refresh SCP instance-count capture | `get_inst_cnt.sh` | Immutable evidence key |
| EVID-02 | Post-refresh SCP instance-count capture | `get_inst_cnt.sh` | Same schema as pre-capture |
| EVID-03 | SCP instance-count comparison | `get_inst_cnt.sh` | Missing-precondition/tolerance policy |
| EVID-04 | QC/difference report | `qc_diff_report.sh` | Artifact and human-review rule |
| EVID-05 | Direct-messaging configuration state | `direct_msg_chk.sh` | Only after CCL-output redaction |
| MOD-TNS-00 | Parent: TNS file validation | `tns_validator.sh` | Explicit file path; no modification |
| TNS-01 | Ownership and permission check | `tns_validator.sh` | Owner/group policy optional |
| TNS-02 | Text integrity check | `tns_validator.sh` | Empty/binary/corruption result |
| TNS-03 | Duplicate alias detection | `tns_validator.sh` | Case-insensitive semantics |
| TNS-04 | Parenthesis syntax check | `tns_validator.sh` | Fail on unmatched delimiters |
| TNS-05 | Formatting warning report | `tns_validator.sh` | Warning unless policy changes |
| TNS-06 | Alias reachability | `tns_validator.sh` | Bounded/redacted `tnsping` result |

## Controlled-capture tasks

These are not validation checks. Do not implement before FND-06 is accepted.

| Placeholder | Capture task | Source | Required decision |
| --- | --- | --- | --- |
| CAP-01 | Database schema/interface export | `db_schema_exp*.sh` | Classification, storage, capacity, retention, rerun |
| CAP-02 | Printer/forms configuration capture | `printers_backup.sh` | Artifact allowlist and host-file handling |
| CAP-03 | OEN domain capture | `oen_domain_save.sh` | Output/restore relationship and ownership |
| CAP-04 | Sanitized SCP configuration capture | `ccl_scp_checks.sh` | Redaction before persistence |
| CAP-05 | Sanitized application URL/configuration capture | `ccl_scp_checks.sh` | Field allowlist and redaction test |

## RefRep prereq certification tasks

**Parent: PREREQ-00 – Recover the current external `refrep_prereq` contract.**
The RefRep archive parses the executable's check table but does not prove which
bundled scripts are active. Each row below is therefore a discovery/certification
task, not an OLAM configuration task.

| Placeholder | Candidate script | Functional group |
| --- | --- | --- |
| PREREQ-01 | `checkDBArchiveMode.ksh` | Database configuration |
| PREREQ-02 | `checkOEMinstalled.ksh` | Database tooling |
| PREREQ-03 | `checkPSUVersion.ksh` | Database patch/version |
| PREREQ-04 | `checkSchedulerJob.ksh` | Database scheduler |
| PREREQ-05 | `checkTempfileInTablespace.ksh` | Database capacity |
| PREREQ-06 | `checkUndoTableSpace.sh` | Database capacity |
| PREREQ-07 | `checkasmfreespace.sh` | ASM capacity |
| PREREQ-08 | `checkbackupconfig.ksh` | Backup configuration |
| PREREQ-09 | `checkdbcopied.ksh` | Database state |
| PREREQ-10 | `checkdbhugepages.ksh` | Database host configuration |
| PREREQ-11 | `checkdbreadwrite.ksh` | Database state |
| PREREQ-12 | `checkdbredolog.ksh` | Database configuration |
| PREREQ-13 | `checkbeaccounts.ksh` | Backend accounts |
| PREREQ-14 | `checkcbo.ksh` | CBO configuration |
| PREREQ-15 | `checkcboenabled.ksh` | CBO state |
| PREREQ-16 | `checkcbostatusviachef.ksh` | CBO/Chef state |
| PREREQ-17 | `checkcodecache.ksh` | Application runtime |
| PREREQ-18 | `checkdm.ksh` | Deployment Manager |
| PREREQ-19 | `checkdmserversynced.ksh` | Deployment Manager synchronization |
| PREREQ-20 | `checkibus.ksh` | iBus |
| PREREQ-21 | `checkinterfacedefs.ksh` | Interface configuration |
| PREREQ-22 | `checkmillcred.ksh` | Credential-related; security review |
| PREREQ-23 | `checkmqssaudit.ksh` | MQSS audit |
| PREREQ-24 | `checkolympusconfig.ksh` | Olympus configuration |
| PREREQ-25 | `checkoscred.ksh` | Credential-related; security review |
| PREREQ-26 | `checkp2sentinel.ksh` | P2 Sentinel |
| PREREQ-27 | `checkprocess.ksh` | Process health |
| PREREQ-28 | `checkschedtemplates.ksh` | Scheduling templates |
| PREREQ-29 | `checkscp.ksh` | SCP configuration |
| PREREQ-30 | `checkscpserver.ksh` | SCP server state |
| PREREQ-31 | `checkukspine.ksh` | UK Spine |
| PREREQ-32 | `checkv500accpasswd.ksh` | Credential-related; security review |
| PREREQ-33 | `checkcmsftplinks.ps1` | Windows CMS/FTP links |
| PREREQ-34 | `checkdomainup.ps1` | Windows domain health |
| PREREQ-35 | `checkloginsenabled.ps1` | Windows login policy |
| PREREQ-36 | `checkolympuslinks.ps1` | Windows Olympus links |
| PREREQ-37 | `checkputtylinks.ps1` | Windows tool/link configuration |
| PREREQ-38 | `check_functions.ksh` | Shared helper; only configure if proven standalone |

Each certification task must establish active use, host scope, privilege,
read/write behavior, result name, exit semantics, output redaction, and an
owner before creating a check implementation task.

## Manual-runbook and future-data tasks

| Placeholder | Task | Completion evidence |
| --- | --- | --- |
| MAN-01 | Inventory every manual procedure | Source/owner/classification recorded |
| MAN-02 | Identify uncovered read-only checks | Deduplicated candidate list |
| MAN-03 | Identify uncovered controlled captures | Artifact/security ownership decision |
| MAN-04 | Classify remediation/restoration procedures | Explicit out-of-scope or separate-governance decision |
| MAN-05 | Classify client/region exceptions | Applicability rule and named owner |
| DATA-01 | Inventory dynamic response-input candidates | Field/source/freshness/provenance/override rule |
| DATA-02 | Select opt-in dynamic-data pilots | Small approved scope; no response-generation change |

## Explicit exclusions

Do not create initial check-implementation tasks for `oen_clear_scp.sh`,
`direct_msg_imp.sh`, Jira scripts, repository/bootstrap scripts, SSH setup,
package installation, email delivery, credential retrieval, database mutation,
or source-to-target restore/copy actions. If later wanted, they require a
separate change-workflow Epic with approval, rollback, and execution ownership.

## Team review gates

1. Confirm which modules are first-release candidates.
2. Confirm that atomic node checks receive separate Jira subtasks.
3. Assign artifact-security and `refrep_prereq` executable owners.
4. Decide whether failed checks notify, block APEX progression, or both.
