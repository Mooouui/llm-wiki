---
title: Govern the CMDB
tags:
  - ServiceNow
  - CMDB
  - Govern
---
## Introduction
### CMDB Governance
Effective governance of ServiceNow CMDB data is critical to ensuring high-quality data, accuracy, and reliability. Governance encompasses policies, processes, and practices to manage the lifecycle, completeness, correctness, and compliance of CMDB data. Below is a list of ServiceNow CMDB tools and features that can be used for this purpose.

#### CMDB Health Dashboard
The ServiceNow CMDB Health Dashboard is a vital tool for monitoring and managing the health of your CMDB. It provides a comprehensive view of data quality, identifying potential issues and helping ensure the CMDB remains accurate, complete, and reliable.

- **Health Scorecard**: Provides a summary that reflects the overall health of each scorecard for Completeness, Correctness, and Compliance.
- **Top 10**: Offers high-level visualizations of which classes impact the overall health of each scorecard, with the option to drill down into detailed information for specific CIs.

*Requires Paid License: No. Part of a base instance accessible from CMDB Workspace under the Management tab.*

*Additional Considerations: CMDB Health Dashboard scheduled jobs used to populate the various scorecards are not turned on by default and must be activated.*

---

#### CMDB Data Manager
ServiceNow CMDB Data Manager is a powerful tool designed to help organizations manage the lifecycle of their CMDB data. It provides capabilities for data quality, governance, and life cycle management, ensuring that CMDB data remains accurate, up-to-date, and compliant with organizational standards.

- **Data Certification**: Automatically validate CMDB data against predefined rules to ensure accuracy and completeness.
- **Life Cycle Policies**: Create clear policies for data retirement, archiving, and deletion, ensuring data consistency and accuracy.
- **Attestation Policies**: Automated task creation to check for the physical existence of IT infrastructure and applications.

*Requires Paid License: No. Accessible via the CMDB workspace.*

*Additional Considerations: Some policy types, such as the life cycle policies Retire, Archive, and Delete, require an active life cycle rule to exist for each targeted class in the policy.*

---

#### Duplicate CI Remediation Wizard
The ServiceNow Duplication CI Remediation Wizard is a powerful tool that guides users through the duplicate CI reconciliation process.

- **Automated Detection**: Automatically identifies potential duplicate CIs based on predefined rules and criteria, such as matching attributes or relationships.
- **Intuitive Interface**: Features a user-friendly interface that guides users through the de-duplication process, making it easy to identify and resolve duplicates.
- **Merge and Delete Functionality**: Provides the ability to merge duplicate records, combining relevant information from each duplicate into a single CI or delete functionality offering the option to delete duplicate records that are deemed unnecessary, ensuring that only the most accurate and complete CI remains.

*Requires Paid License: No. Part of a base instance accessible from CMDB Workspace under the Management tab.*

*Additional Considerations: Requires manual effort to resolve each de-duplication task generated.*

---

#### De-Duplication Templates
ServiceNow provides templates to assist with the de-duplication process. Templates can be pre-configured with rules and criteria that can be customized to meet specific organizational needs.

The creation of templates allows the CMDB administrator to automatically resolve duplicates in bulk versus one at a time.

- **Regular Maintenance**: De-duplication templates can be scheduled to run on a regular basis to keep the CMDB clean and up-to-date by either merging or deleting duplicate records based on pre-defined criteria.
- **Configure Matching Rules**: Configure attribute matching rules, such as class, location, manufacturer, model, etc., to associate to a de-duplication template.
- **Merge and Delete**: Provides the ability to automatically merge duplicate records, combining relevant information from each duplicate into a single CI or delete functionality offering the option to delete duplicate records that are deemed unnecessary, ensuring that only the most accurate and complete CI remains.

*Requires Paid License: No. Part of a base instance accessible from CMDB Workspace under the Management tab.*

*Additional Considerations: Duplicates are automatically handled on a scheduled basis, so in-depth testing of the de-duplication template prior to being published is highly recommended.*

---

By leveraging the various tools and features ServiceNow provides around governance, organizations can achieve the full range of benefits from the CMDB, leading to more effective IT operations, improved decision-making, and a more reliable IT environment.

---
### Summary
ServiceNow CMDB management tools offer several benefits to organizations by providing a centralized and structured approach to managing IT assets and services, including:

- Improved Visibility and Control
- Better Compliance and Audit Readiness
- Enhanced IT Service Management operations
- Improved Decision Making
- Enhanced Automation

Overall, ServiceNow CMDB management tools help organizations achieve greater efficiency, control and alignment between IT and business objectives, leading to improved service delivery and business outcomes.

## Introduction to CMDB Health

### CMDB Health
Most enterprises have gone through the effort to implement a CMDB, yet still struggle to operationalize the data. This is commonly attributed to a lack of easy visibility and control over metrics surrounding the health of their CMDB.

CMDB health issues have downstream effects that can impact the accuracy, completeness, and reliability of the Configuration Management Database (CMDB). Ensuring a healthy CMDB is crucial for maintaining effective IT operations, as it serves as the central repository of all IT assets and their relationships.

For example, from an ITSM perspective, all activities are expressed in terms of CIs. Incidents are tied to degraded CIs, problems are linked to CIs that are the root cause of an outage or are impacting a critical service, and changes are associated with CIs that have unplanned modifications affecting an application/service.

> *“You can’t manage what you can’t measure.”*  
> — Peter Drucker, Management guru

---
### Common Questions Asked on CMDB Health
Enterprises often ask how they can determine the current health state of their CMDB. For instance, they may want to know if CIs of a particular class, such as Server (`cmdb_ci_server`), are populated with the correct discoverable (i.e., serial number, RAM) and non-discoverable attributes (i.e., support group, change group, assignment group).

Additional questions enterprises ask:
- Do our CIs meet configuration standards to achieve compliance?
- Are CIs current or out of date?
- Are there duplicate CIs, and if so, how do we remediate them?
- Have we supported non-discoverable data such as support, change, and managed by groups to our CI and service data?

---

### CMDB Health Journey
When initially implementing a CMDB, organizations often choose to populate it with the best data available at the time. They then focus on improving data quality and automating maintenance through discovery tools like ServiceNow Discovery, Service Mapping, Agent Client Collector, and IntegrationHub ETL to integrate data from third-party sources such as Microsoft SCCM and Azure.

The CMDB Health Dashboard plays a key role in driving these improvements by offering identifying key issues and highlighting non-compliant configuration items (CIs), helping ensure data is accurate and ready to support business processes throughout the ServiceNow portfolio.

---
### CMDB Health Dashboard
The ServiceNow CMDB Health Dashboard is a powerful tool designed to answer common questions around CMDB health, offering a comprehensive view of your Configuration Management Database (CMDB) health. It enables administrators, IT managers, and remediation task owners to assess and maintain the quality of CMDB data, ensuring it is accurate, complete, and current.

The dashboard is crucial for effective CMDB management, helping to drive better decision-making in IT operations by providing actionable insights into data quality and compliance.

The CMDB Health Dashboard consists of the following three scorecards:
1.  **Completeness**: Offers insight into the population of required and recommended field data.
    - Are your CMDB CIs populated with all the essential data?
    - Have you populated non-discoverable data such as ownership or support group?
2.  **Compliance**: Provides visibility into how well the CMDB complies with established standards and policies known as audits.
    - Are your CMDB CIs configured correctly and aligned with desired state expectations?
3.  **Correctness**: Validates that the data within the CMDB is accurate and reflects the true state of the IT environment.
    - Are your CMDB CIs current, accurate, free of duplicates, and containing meaningful relationships?

#### How is the overall scorecard percentage calculated?
In the case of the **Correctness scorecard**, the overall percentage represents the percentage of CIs that pass **all defined metrics**, as noted in the scorecard description.

For example, even if individual metrics show passing rates of 93%, 100% and 96% respectively, the overall score may still be lower—such as 89%—because only 89% of the CIs successfully met **all metric criteria**.

---
### CMDB Health Dashboard Architecture
The overall CMDB health score is based on three Key Performance Indicators (KPIs): Correctness, Compliance, and Completeness. Each KPI includes several sub-metrics. These KPIs and metrics are evaluated through scorecards, which assess their impact on the overall CMDB health at the global, CI class, or CMDB Health Group level.

The following metrics are used to calculate overall CMDB health:
- **Completeness Scorecard**: Uses *Recommended* and *Required* metrics
- **Compliance Scorecard**: Uses *Audit* metric
- **Correctness Scorecard**: Uses *Duplicate*, *Orphan*, and *Staleness* metrics

Understanding these metrics and what they are, how to configure them, how to use them in practice, explaining when they give good but false negatives, will allow you to use them effectively and gain value from them.

---
### Health Inclusion Rules
Health Inclusion Rules are configuration settings that allow administrators to define which CI (configuration item) classes should be included in the CMDB Health Dashboard’s evaluation. These rules ensure that only relevant CI classes are considered when measuring CMDB health metrics like Correctness, Completeness, and Compliance.

Consider a customer implementing a discovery tool that populates everything it discovers into the CMDB. As you can imagine, this generates significant amounts of data, much of which may not fall under your responsibility. A best practice is to configure your CMDB Health Dashboard to only calculate metrics for the CI classes your organization is accountable for managing.

Some benefits of implementing Health Inclusion Rules are the following:
- **Selective Class Tracking**: Administrators can specify which CI classes should be tracked for health metrics, avoiding clutter on irrelevant or unused CI types. This helps focus only on and performance issues by excluding unnecessary CI classes.
- **Granular Control**: Using Health Inclusion Rules, you can apply specific filters to different metrics (e.g., you can apply the rule to Correctness but not to Completeness). This enables fine-tuned control over which classes contribute to each health score.
- **Customizable Metrics**: Health Inclusion Rules allow you to define rules based on the nature of your environment. For example, you might include network application classes while excluding network or hardware classes that don’t require active rules.
- **Operator-Based Rules**: Using operators like “is a,” you can include all Hardware classes or Applications (e.g., this helps streamline the rule creation process and ensures that extended classes are also captured).

Health inclusion rules are the first step in filtering data from the CMDB Health Dashboard rules to better see the data. Health inclusion rules allow you to filter which CIs and classes are calculated as part of the CMDB Health Dashboard.

---
### Health Group Health Dashboard
The CMDB Group Health Dashboard provides a centralized view of the aggregated health results for CMDB groups. Each dashboard displays the detailed information within the group, allowing you to drill down into metrics for specific CI classes. This dashboard eliminates the need to switch between metrics, for all CI classes in one place, streamlining the view of various classes in the CMDB Health Dashboard hierarchy.

*Example: Creating a Linux Server group configured to display only the scorecards and the overall health percentage on the health dashboard, filtered based on the group.*

---
### Checklist to Keep a Healthy CMDB
1.  **Prevent bad data** by ensuring that baseline identification rules are effective for CIs being ingested or updated in the CMDB. Regularly review all main processes involved in creating and updating CIs.
2.  **Regularly review the CMDB Health Dashboard** to identify issues such as duplicates of the misconfigured, and proactively address issues in a timely manner.
3.  **Conduct quarterly reviews** to identify issues like missing information on key fields, such as Managed By Group, Support Group, or Serial Number missing?

---
### Summary
Maintaining a healthy CMDB refers to the overall state of the Configuration Management Database (CMDB). Ensuring that the CMDB is accurate, complete, and reliable is crucial for effective IT service management, as it serves as the foundation for understanding and managing IT infrastructure, services, and their relationships.

If health issues arise, ServiceNow provides tools such as the CMDB Health Dashboard, which helps monitor and assess the CMDB’s health across various dimensions like completeness, correctness, and compliance like the audits.

Have you adopted best practices and the use of automation tools in maintaining a healthy CMDB?

## CMDB Health Dashboard – Completeness Scorecard

### Why the Completeness Scorecard Matters?
CMDB configuration data is critical for supporting configuration management processes. To be effective, the data must be accurate, up-to-date, and complete. Missing key values in configuration items (CIs) can impede other processes that depend on this data.

For example, if incidents reference a server CI with missing fields such as support group, owner, location, asset tag, cost center, or change group, it could cause delays and lead to frustration and inefficiencies for the Service Desk in resolving issues.

Customers should review their configuration items (CIs) and CMDB classes to identify the key fields that must be populated to effectively support other processes. Based on this evaluation, the ServiceNow administrator can designate certain fields as either recommended or required, then leverage the CMDB Health Dashboard to monitor which CIs are missing data. When data gaps are identified, tasks can be automatically assigned to the owner or responsible group to update the relevant CIs with the necessary data.

The ServiceNow base system does not provide predefined suggestions for required or recommended CI attributes in the CMDB. It is up to the CMDB administrator and other stakeholders to determine which fields are essential to support their specific processes.

---

### Completeness Scorecard Overview
The CMDB Health Dashboard provides a Completeness Scorecard to help ServiceNow administrators track which CIs and CI classes are missing key data.

The Completeness KPI is an aggregation of the following metrics:
- Recommended
- Required

Required and recommended metrics are very helpful in measuring the effectiveness of either manual or automated processes of populating CIs in the CMDB using ServiceNow Discovery or third-party discovery solutions such as SCCM or Altiris.

The Completeness Scorecard improves the overall health of a customer’s CMDB by providing visibility around which classes and CIs are missing required and recommended fields. Improved visibility drives adoption of improved processes to increase the overall Completeness score making the CMDB a more reliable source of truth for configuration data and the processes that rely on it.

---

### Required and Recommended Fields
The requirements vary by class, but certain decisions can be made at the base class level, which will be inherited by all subclasses.

For instance, if the `support group` field on a CI (which correlates to the `assignment group` field on an incident form or the `change group` field on a CI, which correlates to the `assignment group` field on a change form) is used to manage incident and change assignments, these fields should be considered recommended.

While it may seem logical to make them required, most discovery tools do not capture this information. This could create issues when trying to add newly discovered CI records into the CMDB. By setting these fields as recommended rather than required, you can still track which CIs are missing this data without causing complications.

Recommended fields are only used for visibility and do not impose any sort of database functionality in terms of errors when the attribute is not populated.

#### Required Fields
- Are equivalent to the fields marked as mandatory in the system dictionary.
- Should be used sparingly during the initial CMDB implementation to prevent record creation failures due to missing required field data.
- Are global and marked as mandatory wherever they appear on a form.
- Must be filled in to create a record.
- Can lead to users entering incorrect data to allow record creation if implemented.
- Ideally, it should be automatically populated by discovery tools.
- May include fields used by the Identification and Reconciliation Engine (IRE) to determine whether records should be created or updated.

*Examples of required fields might be: Serial Number, Name, MAC Address.*

#### Recommended Fields
- Measure the percentage of CIs where recommended fields are not populated.
- Should be used instead of required fields during the initial CMDB implementation to facilitate populating missing data without the complications associated with required fields.
- Are not predefined in the base system.
- Are not enforced in the CMDB, meaning fields do not need to be populated to create a new record.
- Can serve as a testing ground for fields that might become required in the future.

*Examples of recommended fields might be: Assigned To, Location, Support Group, Change Group, Managed By Group, Serial Number, Name.*

⚠️ **IMPORTANT**: Setting an attribute as “required/mandatory” can cause ServiceNow Discovery jobs or imports to fail. The system property `glide.required_attribute.enabled` is set to `true` by default in base system, enforcing that mandatory fields must be populated or errors will result.

---

### How to Configure the Completeness Scorecard
To use the Completeness Scorecard, three things should be configured:

#### 1. Required Fields
Determine what class level and which fields to mark as mandatory. Fields can be marked as mandatory within the Dictionary Entry.

1.  In CI Class Manager, select **Hierarchy**.
2.  Search for the class where the field needs to be set as mandatory.
3.  Under *Class info*, select the **Attributes** tab.
4.  Under *Column label*, open the field that needs to be set as mandatory.
5.  Select the **Mandatory** checkbox or create a dictionary override if necessary depending on which class the field belongs to.
6.  Select **Update**.

> **Dictionary Override Note**: Required attributes must be marked as required at the column level within a specific table or CI class. If a field needs to be individually required in a child class that belongs to the parent class, a dictionary override can be used to change the default setting inherited from the parent class.
> 
> For example, consider the Serial Number field. It might be necessary to make this field required for the Hardware class and all its extended classes. However, since Serial Number is defined in the base table, Configuration Items `[cmdb_ci]`, it is not configured as required by default.  
> 
   If a ServiceNow administrator wants to make this field mandatory only for the Hardware class and its extended classes, they can use a dictionary override on the Hardware class to enforce this requirement without impacting the parent classes.

#### 2. Recommended Fields
Determine what class level and which fields to mark as recommended. Fields can be marked as recommended using CI Class Manager.

1.  From CI Class Manager, select **Hierarchy**.
2.  Search for the class where the field needs to be set as recommended.
3.  Under *Health*, select **Completeness**.
4.  From the *Recommended Fields* tab, select and move all desired fields to the right to mark them as recommended.

#### 3. Completeness Score Calculation Job
From the CMDB Health Dashboard, select **CMDB Health > Scheduled Jobs**. From here open the *CMDB Health Dashboard - Completeness Score Calculation* job and either schedule it to run on a regular basis, or select **Execute Now** to run it immediately.

Job status after executing the job can be viewed by navigating to this form: `cmdb_health_metric_status.list`

---

### Considerations for Required Fields
It is advisable to start with **Recommended fields** to highlight missing data without causing disruptions. While making fields required is a data-fixing issue, it can create issues during integrations, especially when native data is missing.

For instance, if the `Support Group` field is set as mandatory and Discovery discovers a new server that is not assigned to a support group, the insert will fail if the `Support Group` is not populated by the Discovery.

If a field must be marked as mandatory and an integration using the ServiceNow Reconciliation system engine (IRE) has data missing to resolve this issue, follow these steps to override the default behavior:

1.  Navigate to **Configuration > CMDB > Identification/Reconciliation**.
2.  Search for the property named *Enforce the rule that required entities cannot be identified and reconciled*.
3.  Deselect the checkbox to set the property to false.
4.  Select **Save**.

Alternatively, navigate to `sys_properties.list` and set the property `glide.required_attribute.enabled` to `false`.

---

### Summary
Configuring and leveraging the Completeness Scorecard takes advantage of several benefits aimed at recognizing the value that the CMDB provides. Utilizing the Completeness scorecard can be summed up by providing the following:

- **Improved Data Quality**: The scorecard evaluates whether critical fields in the CMDB are populated, helping to ensure that the data is complete, accurate, and reliable for decision-making.
- **Proactive Issue Identification**: The scorecard highlights incomplete data in CIs before they impact other processes like incident, change, or asset management.
- **Enhanced Visibility**: The scorecard provides clear visibility into the completeness of the CMDB, enabling IT managers to monitor the health of processes at a glance.
- **Process Efficiency**: By ensuring that key data is complete, the scorecard improves the workflows and service management tasks.
- **Better Compliance**: With complete and accurate data in the CMDB, the scorecard helps organizations track and manage compliance with regulations that require accurate and up-to-date configuration data.
- **Governance Practices**: By ensuring key fields are completed, fostering a more structured and reliable CMDB.

## CMDB Health Dashboard – Compliance Scorecard

### CMDB Compliance Scorecard Overview
The Compliance Scorecard is based on audit results, which are derived from customer needs and how they want their CIs configured or what should be installed on them.

#### Examples of Compliance Audits:
- All workstations must have antivirus software installed.
- All Linux servers must be on the latest patch.
- All production servers must have a support group and managed by group assigned.

A common use case for the Compliance Scorecard is managing system upgrades. Audits can be performed to identify which devices do not meet the minimum hardware requirements—such as free disk space, RAM, and processor capacity—for upgrading to the next version of an operating system. The Compliance Scorecard allows customers to quickly determine which servers fall short of these requirements.

Audits compare the actual values of specific fields against the expected values defined in templates or scripted audits. For a CI to pass the CMDB Health audit test, it must comply with all applicable audits.

The CMDB Health Dashboard uses the most recent audit run dates to identify the latest complete audit results, which are then displayed on the Compliance Scorecard for visibility.

---

### Compliance Scorecard Configuration
To use the Compliance Scorecard, four key components must be configured:

#### 1. Certification Filter
A certification filter defines the scope of the audit, typically targeting configuration items (CIs) of a certain type.

**Steps to configure:**
1.  From CI Class Manager, under **Hierarchy**, choose the appropriate class to open.
2.  Under **Health**, select **Compliance**.
3.  Under *Certification Filter*, select an existing filter or select **New**.
4.  Configure the Certification Filter as needed and save the record.

*Examples: All UNIX servers in a specific datacenter, all databases, all Windows computers.*

> **Note**: Certification Filters can also be viewed and configured by navigating to **Compliance > Filters**.

---

#### 2. Certification Template
A certification template defines the conditions that must be met to pass the audit. The conditions can be set on attributes, relationships, and reference field values that indicate what a record is expected to contain. The template references the certification filter to determine the scope of the audit.

**Steps to configure:**
1.  From CI Class Manager, under **Hierarchy**, choose the appropriate class to open.
2.  Under **Health**, select **Compliance**.
3.  Under *Certificate Template*, select an existing template or select **New**.
4.  Configure the template as needed, verify *Audit type* is set to **Desired State**, and save the record.

*Examples: Servers not running anti-virus software, Critical application services with no owner, Windows computer minimum statistics.*

⚠️ **IMPORTANT**: To ensure an audit is included in the CMDB Health Dashboard, its type must be set to "Desired State". Audit types like "Compliance" and "Compliance Architecture" are not included in the CMDB Health Dashboard and are used for other ServiceNow products.

If the certification conditions for a Desired State audit are not specific enough, Scripted Audits can be used as an alternative. With these audits, certification criteria are written in scripts rather than configured. Scripted Audits are also included in the CMDB Health Dashboard.

> **Note**: All Certification Templates can also be viewed and configured by navigating to **Compliance > Templates**.

---

#### 3. Audit
A certification audit compares the actual attributes of certain ServiceNow records. The audit utilizes the filter against the expected attributes, relationships, and related record values defined by a certification template.

**Steps to configure:**
1.  From CI Class Manager, under **Hierarchy**, choose the appropriate class to open.
2.  Under **Health**, select **Compliance**.
3.  Under *Audit*, select an existing audit or select **New**.
4.  Configure the Audit as needed and save the record.

*Examples: UNIX Server Baseline, Windows Computer Minimum Statistics.*

> **Note**: You can configure the audit to create and assign follow-on tasks to remediate any discrepancies when the audit finds an audit records use standard ServiceNow scheduler in related lists of the audit record.
> All Audit records can also be viewed and configured by navigating to **Compliance > Audits**.

---

#### 4. Compliance Score Calculation Job
After the audit is configured and executed, the compliance scorecard scheduled job needs to be executed. It executes a job script for calculating the Compliance KPI for CMDB health.

**Steps to configure:**
1.  Navigate to **Configuration > Health Preferences**.
2.  Select **Scheduled Jobs**.
3.  Search for and open the *CMDB Health Dashboard - Compliance Score Calculation* scheduled job.
4.  Select **Activate**.
5.  Configure the schedule as needed.
6.  Select **Execute Now** to return results immediately.

> **Note**: After executing the job, the status can be viewed from `cmdb_health_metric_status.list`.
> Jobs should be executed with a user that has the admin role. If jobs are run by a non-admin user, results may reflect inaccurately due to limited user rights.

---

### Demo
You can access videos demonstrating the configuration and results of the Compliance Scorecard:
- *CMDB Health Dashboard Compliance Scorecard Configuration Demo*
- *CMDB Health Dashboard Compliance Scorecard Results Demo*

> **Note:** The CMDB Data Manager on the ServiceNow AI Platform allows administrators to create certification policies. While these policies may be confused with CMDB > Health Desired State audits, they serve a distinct purpose. Certification policies are particularly useful when manual certification of attributes is necessary.
>
> Due to regulatory or procedural requirements, information in the CMDB must be regularly checked for accuracy and certified. Certification policies enable the responsible person or team to define which data needs verification and establish a verification schedule. This schedule generates a checklist to guide the verification process. Those assigned to certification tasks then answer a series of questions to confirm the accuracy of the data.
>
> Certification policies are commonly used to verify attributes that are not automatically gathered by discovery tools, such as owner, support group, or change group information.
>
> Example:
> - Use **Data Manager** certification policies to manually verify that Joe Smith is the designated owner of ServerXYZ and that the Infrastructure team is assigned as the correct support group.
> - Use **CMDB Health Dashboard Compliance Desired State** audits to automatically check that ServerXYZ has an owner and support group assigned, ensuring that these fields are not left empty.
>
> Data Manager is covered in more detail later in the module.

---

### Scripted Audits
A scripted audit enables users with the certification admin role to conduct an audit from a script rather than using template conditions, which may be too restrictive.

A scripted audit uses a certification filter to select the records to audit and then creates standard follow-on tasks for remediation of any discrepancies. Use this type of audit to query for any values or states that a script can define.

Scripted audits and desired state audits are the only two types of audits that are calculated on the Compliance Scorecard.

To create a scripted audit, an administrator must navigate to **Compliance > Scripted Audits > Audits**. 

---

### Summary
The ServiceNow CMDB Health Dashboard and Compliance Scorecard are essential tools for ensuring the CMDB remains a reliable source of configuration data. These tools enable IT teams to manage system upgrades, enforce governance policies, and support operational efficiency.

By using these tools, organizations can minimize risks, optimize configuration, and make more informed business decisions based on accurate configuration data.


## CMDB Health Dashboard — Correctness Scorecard

### Correctness Scorecard Overview
A CMDB containing duplicate data, outdated CIs, and CIs without relationships can erode users' trust in its information. Fortunately, the CMDB Health Dashboard offers a Correctness Scorecard, which assesses compliance with the following metrics: Duplicate, Orphan, Stale.

> The CI Class Manager is used to configure the Correctness Scorecard based on class definitions.

---

### Duplicates Metric
One of the more difficult tasks in maintaining the CMDB is managing duplicates. The Correctness Scorecard offering insight into duplicates across your environment, from the top-level CMDB class structure down to specific classes like Windows or Linux Servers.

CIs identified as duplicates—either through Discovery or the execution of the CMDB Correctness job—are factored into the Duplicate metric on the CMDB Correctness Scorecard. This metric measures the percentage of duplicate CIs in the CMDB using predefined identification rules.

Once CIs are flagged as duplicates, a de-duplication task is generated, and duplicates are included as part of the Correctness Scorecard calculations.

In addition, after the Correctness Score Calculation job runs, the oldest CI record based on the creation date is considered the non-duplicate by default. Newer CI records are flagged as duplicates of the oldest CI in the Duplicate Of field. The following example illustrates this process.

Windows Server records illustrating duplicate records.

### CMDB Correctness Scorecard — Duplicate Metric
The CMDB Health Dashboard provides a view into which classes have the most duplicates and then lets you drill in to determine the specific CIs identified as duplicates.

Additionally, administrators can identify which discovery sources or owners are contributing the most to duplicate records in the CMDB, aiding in root cause analysis.

> Important: Only independent CIs are evaluated for duplication, (e.g., non-application CIs such as hardware records)

---

### Orphan Metric
Orphan CIs are flagged when they no longer maintain required relationships with other CIs. It's important to note that there are no base system orphan rules, which is evident when viewing the CMDB Health Dashboard Correctness Scorecard after the Correctness Score Calculation scheduled job is first executed.

To track orphan CIs, you can create orphan rules that calculate the percentage of orphaned CIs in the CMDB. This percentage is then aggregated into the overall Correctness Scorecard.

Orphan rules are configured by class, with only one orphan rule allowed per class. Examples of orphan rules include:
- Applications with no relationship to a server
- Tomcat applications with no relationship to a war file
- Hardware device has no owner
- Virtual machine has no relationship to an ESX server

Orphan Rule Example:
The orphan rule is configured so that an Application CI (or any of its child classes) is classified as an orphan if it lacks a Runs on:Runs relationship to a Server CI (or a child class of a server).

---

### Staleness Metric
Staleness occurs when a CI has not been updated in the CMDB for a specified period. This can happen if the CI is no longer detectable on the network and cannot be scanned by discovery tools, or if the discovery process has changed and the CI is no longer included in the scope for automatic scanning. Since infrastructure and applications frequently change, having stale CIs can adversely affect the overall health of the CMDB.

#### Base System Staleness Rule
In a base system, only one staleness rule is defined at the base CI class level, Configuration Item (`cmdb_ci`), and it applies to all extended child classes in the CMDB. This rule indicates that a CI is considered stale if it has not been updated for 60 days.

An update is determined by the `sys_updated_on` field. Even if a CI is discovered by ServiceNow Discovery or a third-party discovery tool without any attribute changes, the `sys_updated_on` field will reflect the updated timestamp of the last scan.

Some considerations around when and why to make additional rules on more granular class levels are as follows:
- How are you populating the CMDB? Is it ServiceNow Discovery, Service Graph Connectors, IntegrationHub ETL, or API via third-party?
- What frequency is discovery executed?
- Is the frequency of discovery different from class to class?

Based on responses to questions like these, you may choose to configure additional staleness rules. For instance, if network devices are scanned every 14 days, you might want to set the staleness rule for this class to 21 days.

If servers are discovered daily and you wish to allow for a buffer, you can set the staleness rule for the server class to 7 days.

Regardless of the specific staleness policy that suits your environment, staleness is a crucial metric that should influence lifecycle management. You want to avoid using CIs in their processes if they no longer exist in the environment or if their attributes are outdated.

---

### Summary
The CMDB Health Dashboard Correctness Scorecard is a feature in ServiceNow that measures the correctness or accuracy of the Configuration Management Database (CMDB). It focuses on measuring how correct or accurate the configuration items (CIs) are by assessing various metrics related to the completeness and consistency of the CMDB data.

Specifically, the Correctness Scorecard provides visibility into duplicate, stale, and orphan CIs in the CMDB. The scorecard visualizes the CIs to analyze the configuration metrics when it detects issues like duplicate, orphan, or stale relationships. This helps users trust in its information. Discovering missing or incorrect relationships or if the data in the results is fragmented.

Overall, the CMDB Health Dashboard Correctness Scorecard provides a health score based on duplicate, stale, and orphan data in the CMDB.

In summary, the Correctness Scorecard is a crucial tool for maintaining a high-quality, reliable CMDB by continuously monitoring and improving the accuracy of configuration items.


## Manage Duplicates

### Introduction to Duplicate CIs
Duplicate configuration items (CIs) records are unfortunately common in many CMDBs. In ServiceNow, duplicate CIs in the Configuration Management Database (CMDB) can lead to significant data integrity issues, affecting everything from reporting to incident resolution and change management.

Duplicate configuration items (CIs) in the ServiceNow CMDB can be created through several processes, including:
- **Automated Discovery Tools**: When multiple discovery tools scan the same environment, they might identify the same CI differently, leading to duplicate records.
- **Import Sets**: When data is imported into the CMDB from external sources without proper identification and reconciliation rules, it can result in duplicate CIs.
- **Third-Party Integrations**: Integrating data from external systems via REST, SOAP, or other APIs without proper identification logic can introduce duplicate CIs.
- **Manual Entry**: Users manually entering CI data into the CMDB may inadvertently create duplicates if there is a lack of governance and they do not follow established naming conventions or identification rules.
- **Incomplete or Incorrect Identification Rules**: If the identification and reconciliation rules in ServiceNow are not properly configured, the system may fail to recognize existing CIs and create duplicates instead.
- **Lack of Governance**: Without strict governance or policies around CI creation and management, different teams or processes might unknowingly create duplicate records.

---

### How Are Duplicates Determined?
Duplicate Records are determined when the IRE finds two or more CIs that match based on the identification rules that exist for the class that the CI belongs to. Also, during a ServiceNow Discovery if duplicate CIs are found in the CMDB, ServiceNow Discovery will update the oldest CI determined by the creation date. In addition, a de-duplication task is created which can be viewed from the CMDB Workspace.

> **IMPORTANT**: If two or more CIs in the CMDB are duplicates and have a populated Discovery Source field, the CMDB Health Dashboard Correctness scorecard will not flag them as duplicates. This is because the Identification and Reconciliation Engine (IRE) assumes they’ve already been processed by the IRE. However, if these CIs are rediscovered and reprocessed by the IRE at a later date, they will then be flagged as duplicates, and a de-duplication task will be generated.

---

### Managing Duplicate CIs
ServiceNow provides tools and processes to manage and resolve duplicate configuration items (CIs) in the Configuration Management Database (CMDB) through de-duplication tasks. Here’s an overview of how de-duplication works:

#### Identification and Reconciliation Engine (IRE)
The Identification and Reconciliation Engine (IRE) is central to preventing and resolving duplicate CIs. It uses identification rules to recognize whether a CI already exists in the CMDB and reconciliation rules to determine how data should be updated or merged. Properly configured IRE rules help minimize the creation of duplicates during data imports, integrations, and discovery processes. However, if the IRE identifies two or more identical CIs in the CMDB, a de-duplication task is generated.

#### De-duplication Tasks
ServiceNow can automatically create de-duplication tasks when potential duplicate CIs are identified. These tasks allow users to review and take action on duplicate records.
- **Identification of Duplicates**: The system identifies potential duplicates based on matching attributes, such as serial numbers, IP addresses, or other unique identifiers.
- **Task Creation**: When a duplicate is detected, a de-duplication task is generated, assigning it to the appropriate team or individual for review.
- **Review and Resolution**: The assigned user reviews the duplicate CIs and decides the appropriate action—whether to merge records, update information, or delete unnecessary duplicates.

In legacy instances, the de-duplication tasks were accessible only through the De-duplication Tasks module. With the introduction of CMDB Workspace, de-duplication tasks can now be viewed and resolved directly from the workspace.

---

### System Properties to Manage Duplicates
The handling of duplicate CIs through the IRE is governed by the following system properties:
- `glide.identification_engine.skip_duplicates` (set to true by default)
- `glide.identification_engine.skip_duplicates.threshold` (set to 5 by default)

> If the `glide.identification_engine.skip_duplicates` is true and the number of duplicate CIs identified exceeds the threshold defined in `glide.identification_engine.skip_duplicates.threshold`, then the oldest of the duplicate CIs is picked by setting the Duplicate of field. During rest of the updates to the duplicate records as duplicates are identified by matching the Duplicate of field, the identification engine filters out any CIs in which the Duplicate of field is populated.

---

### Summary
To prevent duplicate records in your CMDB, it’s crucial to focus on identification rules, utilize the ServiceNow IRE during imports and third-party integrations, and establish governance for managing creation of CIs and their configuration options. However, even with strict governance, ServiceNow offers a variety of tools and configuration options to efficiently manage and resolve them.

## Remediate Duplicates

### Importance of Handling Duplicates
Handling duplicate Configuration Items (CIs) in the ServiceNow CMDB is crucial for several reasons:

- **Data Integrity and Accuracy**: Duplicate CIs can lead to inconsistencies in your CMDB, making it difficult to trust the data. Accurate data is essential for making informed decisions, managing assets, and ensuring that IT operations run smoothly.
- **Improved IT Operations**: Duplicate records can cause confusion and errors in processes such as incident management, change management, and problem resolution. Ensuring each CI is unique and correctly represented helps streamline these processes and reduces the risk of operational disruptions.
- **Enhanced Reporting and Compliance**: Accurate reporting is essential for compliance with regulatory requirements and for providing stakeholders with reliable data. Duplicate CIs can distort reports, making it challenging to maintain compliance and demonstrate accountability.
- **Better Decision-Making**: Accurate and unique CI records allow for better analysis, forecasting, and decision-making across IT and business operations. With reliable data, organizations can more effectively plan for future needs and mitigate risks.

---

### Terminology
Select each item to review a short definition.

- **Duplicate CI Remediator**
  The Duplicate CI Remediation is a wizard-driven user interface that guides administrators through the process of reconciling duplicate CIs or enables them to apply a custom workflow to resolve duplicates in the CMDB.

- **De-Duplication Templates**
  De-duplication templates can be used to remediate duplicates in bulk by applying pre-configured and consistent remediation to de-duplication tasks.

- **Main CI**
  The Main CI (previously referred to as the Master CI) is the duplicate CI that an administrator chooses to keep as the active record while potentially retiring or deleting the other duplicates. The recommended Main CI is typically the one that is the oldest, has the most relationships, and has been most recently updated.

- **Duplicate Of Field**
  Formerly, the Discovery source field provided visibility to duplicate records in the CMDB. In recent releases, the *Duplicate Of* field is used to indicate that a CI is a duplicate of another CI. It helps track which records are considered duplicates and links them to the original CI.

- **Merge**
  Merging involves combining multiple duplicate CI records into a single record. This process often includes selecting which attributes from each record should be retained to create a unified and accurate CI.

---

### Duplicate CI Remediator
From a de-duplication task, an administrator can run the Duplicate CI Remediator wizard.

The ServiceNow Duplicate CI Remediator is a wizard-like tool designed to help administrators efficiently manage and resolve duplicate Configuration Items (CIs) within the CMDB. It provides a systematic approach to identifying, reconciling, and merging duplicate records, ensuring data accuracy and consistency. The tool allows administrators to review potential duplicates, select a main CI to retain, and merge relevant data from the duplicates, all while maintaining an audit trail for compliance and traceability. By automating much of the de-duplication process, the De-duplication Remediator helps maintain the health and reliability of the CMDB.

In legacy instances, the CI Remediator was accessible only through the De-duplication Tasks module by navigating to one of the de-duplication task records. With the introduction of CMDB Workspace, de-duplication tasks can now be viewed and resolved directly from the workspace.

---

### De-Duplication Templates
As opposed to remediating duplicates one at a time using the Duplicate CI Remediator, de-duplication templates can be created to apply pre-configured and consistent remediation to de-duplication tasks, in bulk and per class.

The De-duplication dashboard in CMDB Workspace can be used to gain insights about duplicate CIs in your CMDB. The De-duplication dashboard lets you create de-duplication templates and organize these templates into libraries. You can also examine open de-duplication tasks and run a pre-configured template to remedy multiple de-duplication tasks in a single operation.

Select the play button to access the following video on remediating duplicate CIs.

---

### Now Assist for CMDB – Automated Duplicate CI Management
Now Assist for CMDB brings the power of generative AI to CMDB management, enabling faster and more accurate de-duplication. With AI-driven insights, automated data remediation, and real-time intelligence, Now Assist for CMDB helps admins to reduce manual effort, eliminate duplicate records, and enhance data reliability.

By automating CI summarization and duplicate CI management, Now Assist accelerates decision-making, improves service visibility, and ensures data integrity. The tool learns from previous de-duplication tasks, with efforts using pre-configured templates to remedy multiple de-duplication tasks in a single operation.

Leveraging de-duplication templates, automated duplicate CI management ensures clean and accurate CMDB data with AI-driven duplicate CI detection resolution steps. This reduces CI clutter, improves change tracking, and strengthens IT governance.

> For practical hands-on experience using Now Assist for CMDB, attend the CMDB and De-duplication templates Q&A session.

---

### Summary
In summary, effectively managing and eliminating duplicate CIs in the ServiceNow CMDB is vital for maintaining data integrity and optimizing operations. By ensuring that the organization can rely on its CMDB as a single source of truth, service delivery and business outcomes are positively impacted.

> **IMPORTANT UPDATE**: Recent releases of ServiceNow leverage a new field called *Duplicate of* to display visibility to duplicate CIs. The Discovery source field is no longer used to provide duplicates. The new field described in this lesson is exactly the same with the change from Discovery source to the Duplicate of field.
> The reason behind this change is to preserve the Discovery source field value with the last Discovery source that updated the record.


## CI Reclassification

### Reclassification Overview
Customers bring data into the CMDB from multiple sources. In some cases, the CI data imported or manually entered is populated into the wrong table. ServiceNow has an effective way of handling this scenario with a feature called reclassification.

During the CI identification process, ServiceNow has the ability to reclassify a CI from one class to another. By default, CIs are reclassified automatically. If automatic reclassification is disabled, then a CI is not automatically reclassified and the system generates a reclassification task for review with the option to manually reclassify the CI at a later time.

---

### Reclassification Scenario
A ServiceNow administrator imports 300 server records directly into the `Server [cmdb_ci_server]` table. However, these server records are comprised of both Linux and Windows Servers and more appropriately should reside in the `Linux Server [cmdb_ci_linux_server]` table and the `Windows Server [cmdb_ci_win_server]` table. Both are extended or child classes of the `Server [cmdb_ci_server]` table.

#### Reclassification Automated Process
In two weeks, the ServiceNow administrator implements ServiceNow Discovery which finds these same devices and classifies them as Windows and Linux Servers. When Discovery passes these CIs through the IRE, the CI records are automatically upgraded and reclassified from the `Server [cmdb_ci_server]` table to the `Windows Server [cmdb_ci_win_server]` and `Linux Server [cmdb_ci_linux_server]` tables.

---

### Reclassification Terminology
During reclassification, a CI can be upgraded to a higher class, downgraded to a lower class, or switched to a different branch in the class hierarchy.

- **Upgrade**
  The CI class is updated to a class that is lower in the class hierarchy, and the newly assigned class is a derived child of the current class and has additional attributes. For example, reclassifying a CI from the `Server [cmdb_ci_server]` class to the `Windows Server [cmdb_ci_win_server]` class.

- **Downgrade**
  The CI class is updated to a class that is higher in class hierarchy, and the newly assigned class is a parent of the current class and has fewer attributes than the current class. For example, reclassifying a CI from the `Windows Server [cmdb_ci_win_server]` class to the `Server [cmdb_ci_server]` class.
  The `Windows Server [cmdb_ci_win_server]` class has attributes that the `Server [cmdb_ci_server]` class does not have. During the downgrade, these attributes and their respective values are not included in the new CI record that is inserted into the `Server [cmdb_ci_server]` class.

- **Switch**
  The newly assigned class is in a different branch in the class hierarchy and has a different set of attributes than the current class. For example, reclassifying a CI from the `Linux Server [cmdb_ci_linux_server]` class to the `Windows Server [cmdb_ci_win_server]` class.
  During a switch, any data contained in attributes not available in the switched class are lost.

---

### Base Reclassification System Properties
The following system properties control the automation or manual requirement around reclassification of a CI.

When these system properties are set to true, reclassification automatically takes place:
- `glide.class.upgrade.enabled`
- `glide.class.downgrade.enabled`
- `glide.class.switch.enabled`

> ⚠️ **IMPORTANT**: When automatic CI reclassification is enabled (which is the default), be aware that CI class downgrade and CI class switch operations can lead to data loss.

When automatic CI reclassification is disabled, reclassification tasks are created for CIs that are not automatically reclassified during the identification process. The assigned ServiceNow administrator must then review these tasks to locate the CIs and decide if the CI should be reclassified.

> ⚠️ **IMPORTANT**: Additional system properties exist to control CI Reclassification behavior.
> These system properties include:
> - `glide.identification_engine.update_without_switch_enabled`
> - `glide.identification_engine.update_without_downgrade_enabled`
> - `glide.identification_engine.update_without_upgrade_enabled`
> 
> The functionality of CI reclassification works as described in this lesson, however these additional properties provide the CMDB administrator more granular control over how CI Reclassification works.
> Refer to the next lesson for a deeper understanding of these properties.

---

### Summary
Reclassification is the process of a CI being moved from one class to another in the form of an upgrade, downgrade, or switch. In a ServiceNow base system, reclassification is automatically enabled, however a ServiceNow CMDB administrator has the ability to turn off automatic reclassification and instead generate reclassification tasks that can be manually managed.


## Restriction Rules

### Advanced Reclassification System Properties
To disable any automatic reclassification updates, setting the respective properties to false, as described in the previous lesson, rejects the returned payload with any reclassification updates and creates a reclassification task instead. Basically, the CI record is not updated or reclassified, and only a CI reclassification task is created.

The following additional global system properties are available as a more granular approach to reclassification, so that it is not just an all-or-none behavior:
- `glide.identification_engine.update_without_switch_enabled`
- `glide.identification_engine.update_without_downgrade_enabled`
- `glide.identification_engine.update_without_upgrade_enabled`

These properties are set to false in a base system, which results in the same behavior as described in the previous lesson.

However, if these properties are set to true, the IRE processes CI updates, but the respective CI reclassification update does not take place. Basically these new global properties take precedence over the legacy global properties and allow for an update of a CI even if the CI is not reclassified.

For example, if the following properties are set:
- `glide.class.downgrade.enabled = true`
- `glide.identification_engine.update_without_downgrade_enabled = true`

If a Linux Server CI is discovered to be a Server CI, the Linux Server **WOULD NOT** be reclassified as a Server CI, however any updated attributes found for the Linux Server CI would be applied to the record.

---

### Reclassification Restriction Rules
These reclassification global properties are an enhancement from the baseline set of properties providing a more granular level of working with reclassification. However, because they are global properties, it is an all-or-none proposition.

To provide greater control at the class level, reclassification restriction rules are also available. These rules allow administrators to restrict downgrade and switch reclassification between specific classes, while still permitting updates to CI attributes.

The rules can be used to reduce data loss during IRE processing by preventing a CI class change from a specific source to target class. A reclassification restriction rule affects only the reclassification update and does not prevent the update to the rest of the CI attributes.

> Reclassification restriction rules can be configured by navigating to `cmdb_ire_reclassification_restriction.list`

---

### Reclassification Restriction Rule Examples
#### Example 1
Assuming the baseline global property, `glide.class.switch.enabled`, is set to true and the reclassification restriction rules in this example are configured as follows:
- Class switch is not allowed between Linux Server and Windows Server classes.
- Only an update to the Linux or Windows CI attributes is allowed.

> **NOTE**: In this example, the Source and Target Inheritance fields are set to false, indicating that no extended classes are affected by the rule.

#### Example 1 Resulting Behaviour:
If `glide.identification_engine.update_without_switch_enabled` is set to true, then no class switches between any classes are allowed. Setting this property to false, and configuring the reclassification restriction rule as described in example 1, allows for class switches for all classes except between Linux and Windows. Reclassification restriction rules provide more granular control.

#### Example 2
Assuming the baseline global property, `glide.class.downgrade.enabled`, is set to true and the reclassification restriction rule in this example is configured:
- Class downgrade is not allowed between the Server class and its extended classes to the Computer class.
- Only an update to server records and those in extended classes is allowed.

> **NOTE**: Source inheritance is set to true for Server `[cmdb_ci_server]` which in this example signifies that all extended classes of Server `[cmdb_ci_server]` are affected by this rule.

#### Example 2 Resulting Behaviour:
If `glide.identification_engine.update_without_downgrade_enabled` is set to true, then no class downgrades between any classes are allowed. Setting this property to false, and configuring the reclassification restriction rule as described in example 2, allows for class downgrade for all classes except for the Server class and its extended classes (due to the Source inheritance value set to true) to the Computer class. Reclassification restriction rules provide more granular control.

---

### Review
#### Question 1
The following reclassification properties are configured:
- `glide.class.downgrade.enabled=true`
- `glide.identification_engine.update_without_downgrade_enabled=true`

Which of the following will occur due to the configuration? (Select two)
- [ ] A Windows Server is allowed to be downgraded to a Server record
- [ ] A Windows Server is NOT allowed to be downgraded to a Server record
- [ ] The Windows Server CI attributes CAN be updated
- [ ] The Windows Server CI attributes CANNOT be updated

#### Question 2
The following reclassification properties are configured:
- `glide.class.downgrade.enabled=true`
- `glide.identification_engine.update_without_downgrade_enabled=false`
- Reclassification Restriction Rule:
  - Type: Downgrade
  - Source table: Server
  - Source inheritance: true
  - Target table: Computer
  - Target inheritance: false

Which of the following will occur due to the configuration? (Select two)
- [ ] A Windows Server is allowed to be downgraded to a Computer record
- [ ] A Windows Server is NOT allowed to be downgraded to a Computer record
- [ ] The Windows Server CI attributes CAN be updated
- [ ] The Windows Server CI attributes CANNOT be updated

#### Question 3
The following reclassification properties are configured:
- `glide.class.downgrade.enabled=true`
- `glide.identification_engine.update_without_downgrade_enabled=false`
- Reclassification Restriction Rule:
  - Type: Downgrade
  - Source table: Server
  - Source inheritance: true
  - Target table: Computer
  - Target inheritance: false

Which of the following will occur due to the configuration? (Select two)
- [ ] An IP Router is allowed to be downgraded to a Network Gear record
- [ ] An IP Router is NOT allowed to be downgraded to a Network Gear record
- [ ] The IP Router CI attributes CAN be updated
- [ ] The IP Router CI attributes CANNOT be updated


## Remediation Capabilities

### Remediation Capabilities
The CMDB Health Dashboard offers an intuitive way to visualize, investigate, and resolve issues such as duplicate, stale, and orphan configuration items (CIs).

You can configure the dashboard to automatically create health remediation tasks whenever a CI fails health test rules. These tasks can be linked to either automatically or manually to execute workflows that address the issues.

For example, if a CI is identified as stale, a remediation task can trigger a workflow that runs a discovery process on the stale CI. This process updates the CI based on the discovery results, thereby removing it from the staleness metric the next time the scorecard scheduled job is executed.

---

### CMDB Health Dashboard Metrics Review
The CMDB Health Dashboard provides several key metrics. For each failing metric, a remediation task can be automatically generated and assigned to an individual or group. ServiceNow recommends using the managed by group field to assign these tasks. In an earlier lesson, we covered how to auto-populate and maintain this group field, which can then support and streamline the remediation process.

- **Duplicates**: Duplicate CIs are identified during the identification and reconciliation process. When reviews are detected, they are grouped into de-duplication tasks for review and remediation. ServiceNow provides a built-in tool called the *Duplicate CI Remediator*, which offers a step-by-step process to resolve duplicate CIs individually. Alternatively, organizations can configure de-duplication templates to handle and resolve duplicate CIs in bulk, streamlining the process for more efficient management.
- **Staleness**: Stale CIs refer to configuration items (CIs) that have not been updated within a specified timeframe, which increases the likelihood that their data may no longer be accurate. Given the fast-paced nature of infrastructure and application environments, stale CIs are considered unreliable, and efforts should be made to investigate and update them to ensure the accuracy of the CMDB.
- **Orphans**: To classify a CI as an orphan, you must define specific attributes the CI should have or relationships it should maintain, or both. In terms of relationships, you can specify that the CI either lacks any relationships or is missing certain required ones. For example, an orphan rule might state that a CI is considered an orphan if it does not have an assigned owner or associated asset. This ensures that CIs without critical relationships or attributes are flagged for further review.
  Examples:
  - Applications should have a relationship to a host
	  - Example: Microsoft SQL Database should have a Runs::Runs On relationship to a Windows Server
  - Virtual Servers should have a relationship to virtual machines
- **Recommended & Required fields**: 
	**Recommended fields** are fields that are beneficial to be populated by a data source like Discovery or may include fields that contain foundational data that is not discoverable, such as "support" or "change" groups. These fields are not mandatory but can provide valuable information, such as additional data useful for diagnostics or incident routing.
	
	**Required fields** are mandatory fields that must be populated, and the CMDB health system checks for their completion. However, it is recommended to use required fields sparingly to avoid complicating data entry processes. Setting non-discoverable fields, such as the "managed by group", as required can lead to errors during CI creation, particularly when using integrations or automated discovery tools. These tools may encounter issues if required fields are not automatically populated, disrupting the flow of data into the CMDB.

---

### Now on Now—Value and Cost Savings Example
ServiceNow as a company implements its own products in-house. This initiative is known as Now on Now. Over the past year, there has been a big push to improve the overall health of the CMDB. The following is a summary of the Now on Now initiative relating to CMDB.

- Annual time spent on CMDB manual audit was approximately 1 Full Time Employee (FTE) - 2080 hours.
- Estimated time to be saved from this CMDB audit automation is approximately 1252 hours/year (spread across CMDB, Discovery & SRT/Engineering teams).
- This represents a 60% improvement for the CMDB audit over 12 months.

**Intangible values:**
- More up-to-date configuration items. For example, in today’s process, due to the configuration effort each CI class only gets audited once a year. (each quarter different CI classes get audited), so one of the intangible benefits is to get CI information up-to-date in weeks instead of quarters or even years.
- Audits are mostly self-service based, instead of relying on the CMDB team to coordinate/perform them.
- Introduces more audit metrics/attributes for duplicates, staleness, and compliance than the previous process.

*—ServiceNow IT Operations*

---

### Remediation Visual Flow
Below is the basic flow to generate remediation tasks, build flow logic using workflow, configure a remediation rule that references the workflow, and then initiate the workflow from a remediation task in order to perform some sort of remediation action.

Steps in the process flow:
1.  **Enable Task**: Configure health metrics to generate remediation tasks.
2.  **Workflow**: Build the workflow to perform the remediation action.
3.  **CMDB Remediation Rule**: Link the workflow to the remediation rule.
4.  **Remediation Task**: Execute the workflow from the remediation task.

> **Note regarding Duplicate CIs and Audit Tasks:**
> - De-duplication tasks are generated automatically, with no configuration required as illustrated in the flow diagram above. Remediation is handled through the Duplicate CI Remediator.
> - Similarly, compliance audit tasks do not adhere to the process shown in the flow diagram. Instead, health settings are configured through the Compliance Manager by selecting a class and adjusting Health settings under the Compliance section.

---

### Use Case: Remediating Stale CIs
**SCENARIO:**
Cloud Dimensions discovered they have a large number of stale CIs in their CMDB by looking at the CMDB Correctness Scorecard and the Staleness metric in the CMDB Health Dashboard. They have an initiative to remediate the stale CIs by validating that the CIs still discovered, and if not, update the status of the stale CI to Non-Operational and Retired.

**REQUIREMENT**
As the Cloud Dimensions CMDB administrator, configure ServiceNow to meet the following requirements:
1.  Configure the CMDB Health Metrics so that stale CIs will trigger a task.
2.  Build a workflow that does the following:
    - Execute discovery against the stale CI
    - If the discovery is successful, the CI is no longer stale
      - Add comments to the stale CI record
      - Close the Stale CI record
    - If the discovery is not successful
      - Add comments to the Stale CI record
      - Change the state of the Stale CI record to Work in Progress
      - Set the assignment group to Hardware
      - Set the Operational Status to Non-Operational and Install Status to Retired in the CI record
3.  Configure a CMDB Remediation Rule that executes the workflow

> This is just an example of how stale CIs might be resolved. The workflow can be adjusted to perform different actions based on specific business requirements and needs.

---

### Demo Steps
1.  **Step 1 - Build Workflow**: Build a workflow to remediate stale CIs.
2.  **Step 2 - Build a CMDB Remediation Rule**: Configure a CMDB remediation rule.
3.  **Step 3 - Remediation Testing**: Test the remediation rule and workflow.

> **IMPORTANT UPDATE**: The ServiceNow Common Service Data Model (CSDM) provides pre-defined values for the `Operational Status` and `Install Status` attributes. In the previous CSDM versions, you may find the `Install Status` of Retired in some CI records.

---

### Summary
Maintaining a healthy CMDB, ServiceNow offers both manual and automated solutions to help remediate CIs that fail CMDB health tests.

This lesson provided detailed explanation and demonstration of how to address problems by configuring and defining remediation workflows, covering generic health checks, setting up CMDB remediation rules, and executing remediation workflows from those tasks.


## Life Cycle Management

### Life Cycle Management
ServiceNow CMDB life cycle management involves overseeing the complete life cycle of configuration items (CIs) within the Configuration Management Database (CMDB) to ensure data accuracy, consistency, and relevance. It includes managing the transition of CIs through the different life cycle stages, such as operational, retired, archived, and deleted.

Key aspects of CMDB lifecycle management include:
- **Retire**: Define policies for retiring CIs that are no longer in use
- **Archive**: Archive CIs that are no longer needed for active use but must be retained for historical or compliance reasons
- **Delete**: Permanently delete obsolete CIs in accordance with data retention policies and compliance requirements
- **Attest**: Conduct regular attestation processes to validate the correctness and completeness of CI data
- **Certify**: Implement policies to periodically certify CI data, ensuring it meets required standards.

---

### Life Cycle Flow
ServiceNow recommends managing the CMDB data lifecycle to ensure accuracy and relevance. For short-lived data like containers, which are relevant for only a few days to a week, archiving or deleting them after termination prevents clutter. Data Manager policies can automate this process, archiving or purging terminated containers while maintaining an audit trail to keep the CMDB organized.

Key steps for effective data life cycle management include:
- **Understand Life Cycle Requirements**: Recognize that different data types have different life cycles. For instance, container data has a short lifecycle, while server data, tied to asset records, has a longer one.
- **Identify Data Owners**: Assign responsible groups to CIs by leveraging the Managed By Group, and assign policy tasks to these groups.
- **Set Up Life Cycle Fields**: Implement life cycle stages and statuses in the CMDB to track and manage the life cycle of CIs accurately.
- **Create Life Cycle Policies**: Use Data Manager to create life cycle policies and generate tasks on a scheduled basis to ensure ongoing and automated life cycle management.

The life cycle flow process:
1.  Identify data life cycle requirements (Retire, Archive, Delete)
2.  Identify data owners (Managed by Group)
3.  Configure CI life cycle fields (Life Cycle Mapping)
4.  Create life cycle policies (Data Manager Policies)
5.  Monitor and remediate as required (Data Manager Tasks)

---

### Summary
Adhering to this lesson’s guidance makes CMDB life cycle management more manageable, efficient, and automated, maintaining data integrity and relevance with little manual effort.

---
## Life Cycle Field Synchronization

### Shared and Life Cycle Fields
CIs and assets share common fields, such as serial number, model, and ownership details. These shared fields ensure consistent and up-to-date information across both records.

Besides shared fields, there are several fields that indicate the status of a CI or asset record, such as `Install Status`, `Hardware Status`, and `State`. Although often called legacy life cycle fields, they remain widely used by many companies, and the base system includes automation to keep these legacy fields synchronized.

To standardize these values across different products on the ServiceNow AI Platform, ServiceNow introduced additional life cycle fields: `Life Cycle Stage` and `Life Cycle Stage Status`. These fields are recommended for companies aiming to align more closely with CSDM (Common Service Data Model) best practices.

#### Shared Fields
- Asset tag
- Department
- Location
- Support Group
- Company
- Serial Number
- Model ID
- Assigned to

> **NOTE**: For a full list of shared fields, refer to the ServiceNow documentation.

#### Configuration Item Legacy Status Fields
- Operational status
- Install Status
- Hardware Status
- Substatus

#### New CSDM Life Cycle Fields (CI)
- Life Cycle Stage
- Life Cycle Stage Status

> ⚠️ It is not recommended to manage all life cycle status fields. For instance, if using legacy status fields, choose between `Install Status` and `Hardware Status`, but do not use both unless you have a good business justification.

#### Asset Legacy Status Fields
- State
- Substate

#### New CSDM Life Cycle Fields (Asset)
- Life Cycle Stage
- Life Cycle Stage Status

> **NOTE**: The computer CI and asset forms are personalized to display the legacy and life cycle fields for the computer CI and asset record.

---

### CI and Asset Shared Field Synchronization
ServiceNow offers mechanisms to ensure that CIs and assets remain synchronized in a base system, typically when they represent the same physical or virtual item. This is important to avoid data duplication and inconsistencies between the IT operations and finance teams.

- **Automatic Creation**: When a new asset is added into ServiceNow, a corresponding CI can be automatically created in the CMDB, and vice versa. This ensures that the same item is tracked both from a technical and a financial perspective.
- **Shared Fields**: CIs and assets share common fields, such as serial number, model, and ownership details. These shared fields ensure consistent and up-to-date information across both records.
- **Legacy Life Cycle Field Synchronization**: The synchronization keeps the life cycle stages aligned. For example, when an asset reaches the end of its lifecycle (e.g., Retired), the corresponding CI in the CMDB can also be automatically updated to reflect this change.

In a base instance, an `Asset CI Field Mappings` table is used to track all fields that need to be synchronized between assets and configuration items. This table can be customized to include additional field mappings as needed. For example, a new mapping can be added to sync the `Comments` field from the asset record with the `Short description` field in the CI record.

The synchronization works in both directions.

---

### CI and Asset Life Cycle Field Synchronization
Synchronizing legacy life cycle fields ensures status remain consistent. For instance, when an asset reaches the end of its life cycle (e.g., Retired), the related CI in the CMDB is automatically updated accordingly.

The synchronization between asset and CI legacy life cycle fields:
- Asset `State` ↔ CI `Install Status` (two-way sync)
- Asset `Sub-state` ↔ CI `Substatus` (two-way sync)
- CI `Hardware Status` is **not** synced with the asset.

---

### CSDM Life Cycle Mapping Table
To normalize the multitude of legacy life cycle fields, ServiceNow introduced additional life cycle fields: `Life Cycle Stage` and `Life Cycle Stage Status`. These fields are recommended for companies aiming to align more closely with CSDM best practices.

In a base system, a `Life cycle mapping` (`life_cycle_mapping`) table provides pre-populated mappings between widely used legacy status values and the required CSDM life cycle stage and life cycle stage status values. Each record in the table (called a mapping rule) specifies how to map a legacy status value, based on its table, to the best fit CSDM life cycle value pair.

To leverage these mappings, you must select the **Enable Life Cycle Sync** button, which then performs a one-time sync between the legacy status values and the mapped CSDM life cycle values.

> **NOTE**: After selecting Enable Life Cycle Sync, you are presented with a discrepancy report to resolve status fields that do not have a mapping to the new CSDM life cycle fields.

---

### CI and Asset CSDM Life Cycle Field Synchronization
After enabling the CSDM life cycle sync, the one-time sync of all legacy status values is mapped to the CSDM life cycle fields.

From this point forward, all legacy status fields and the new CSDM life cycle fields will be synchronized. Additionally, the CSDM life cycle fields of the related asset install base item (IBI) will also be kept in sync, providing an added benefit.

The sync process:
1. The life cycle stage and life cycle stage status values of the CI are directly synced with the associated asset record.
2. These fields values, there are several fields that indicate the status values of a CI or the mapped fields use the life cycle values from the CI record.
3. The legacy status values of the asset are then synced with the associated CI legacy status values.
4. The CSDM life cycle values of IBI are synced with the asset through the CSDM life cycle pairs.

---

### Summary
The automated synchronization of Asset and Configuration Item (CI) life cycles ensures the status of related Asset and Configuration Item records stay in sync. This maintains consistency between the physical or contracted assets (tracked in Asset Management) and their corresponding CIs (tracked in CMDB).


## Data Manager

### Data Manager Overview
CMDB Data Manager is a policy-driven framework for bulk management of configuration item (CI) end of life operations and certification such as:
- Retire, Archive, and Delete (End of Life policies)
- Attestation
- Certification

This comprehensive and integrated solution is scalable for large CMDBs and adaptable to the rapid changes in a cloud-based environment.

Over time, large CMDBs can accumulate a significant amount of stale CIs, which can negatively impact overall performance. Developing and maintaining custom solutions to address this issue can be challenging and error prone.

CMDB Data Manager provides the capability to create, publish, and manage policies that automate and govern CI life cycle operations, ensuring the CMDB remains in a healthy and efficient operational state.

---

### Use Cases
CMDB Data Manager can be utilized in various scenarios to streamline and automate the management of configuration items (CIs) within an organization's CMDB. Data Manager can be used for data archiving, data deletion, regular attestation and certification, and lifecycle management by automating the transition of CIs through different stages of their lifecycle, such as from active to retired status.

Data Manager sample use cases include:
- **Retire Policy Type**: Retire all computers without owners, which were created more than a year ago
- **Archive Policy Type**: Archive all Linux servers in the Seattle data center that haven't been updated for six months
- **Delete Policy Type**: Delete all containers, which haven't been discovered in the past week
- **Attestation Policy Type**: Attest all the server records in a specified location, meaning verify the actual existence of the IT infrastructure
- **Certification Policy Type**: Certify application services have the correct owner assigned

---

### Legacy Data Manager
The legacy Data Manager, available by navigating to **Configuration > CMDB Data Manager**, will be deprecated by the Yokohama release, and users will be forced to utilize the new and improved Data Manager, now available as part of CMDB Workspace.

---

### Data Manager Accessible from CMDB Workspace
Data Manager, accessible through CMDB Workspace and designed with UI Builder, offers baseline analytics for CMDB admins to gain a high-level overview of Data Manager operations. The new Data Manager enhances the end-user experience by introducing a workflow-based interface, replacing the single UI16 page approach.

Policies created with the legacy Data Manager are fully compatible with the new Data Manager in CMDB Workspace. Additionally, any new policy types introduced in future releases will be supported by the new UI.

As of CMDB Workspace version 6.0.1, the Data Manager now supports certification policies, along with the existing retirement, archiving, deletion, and attestation policies.

---

### Before Using CMDB Data Manager
CMDB Configuration Manager follows the Common Service Data Model (CSDM) life cycle states and standards, which basically places the CI in an end of life status. Following CSDM standards, a CI progresses from the state of retired, to archived or deleted. For example, a CI must be retired and be in an end of life stage before it can be archived or deleted.

#### Review and Activate Life Cycle Mappings
Before activating lifecycle policies, review the pre-populated entries in the `Life cycle mappings` list:
- Adjust and add mappings as needed to fit your environment.
- Review mappings for any custom legacy lifecycle values; these mappings are incomplete and require you to specify the appropriate standard lifecycle control.
- Ensure all mappings are configured with a standard lifecycle control.
- Make sure all mappings are activated.

#### Managed By Group
To ensure Data Manager policy tasks are correctly assigned, it's recommended to leverage the `Managed By Group` associated with the respective CIs.

As mentioned in a previous lesson, this attribute value isn't automatically discovered by ServiceNow Discovery or Service Mapping. However, you can simplify and maintain this attribute by using technical service offerings and dynamic CI groups or secondly leveraging CI Class Manager.

---

### Data Manager Roles
In order to use this feature, appropriate CMDB admins and users can be assigned one of these roles:
- `data_manager_admin`
- `data_manager_user`

---

### Summary
By following the guidance provided in this lesson, CMDB life cycle management becomes much simpler and more streamlined, with minimal manual intervention, ensuring CMDB data integrity and relevance.