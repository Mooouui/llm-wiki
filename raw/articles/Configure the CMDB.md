---
title: Configure the CMDB
tags:
  - ServiceNow
  - CMDB
---
Maintaining the integrity of your CMDB during implementation is crucial, and leveraging proven tools and processes is key. One essential tool is the *CI Class Manager*, which provides a centralized view for creating and editing class definitions and managing settings related to identification, reconciliation, and CMDB health.

Another critical process is the Identification and Reconciliation module, offering a unified framework for identifying and reconciling data from various sources. This module is vital for preserving CMDB integrity, especially when CI records are populated and updated by multiple sources like Discovery, import sets, and third-party tools.

With multiple data sources, the risk of inconsistencies and duplicate records increases. The Identification and Reconciliation module helps prevent duplication, reconcile CI attributes, reclassify CIs, and ensure that only authoritative sources update the CMDB.

Lastly, the CMDB 360/Multi-source CMDB can be used to track how different discovery sources populate the CMDB at the CI attribute level.
## CI Class Manager
### Overview

The CI Class Manager offers several benefits for managing configuration items (CIs) and their classes within the Configuration Management Database (CMDB). Here are some key benefits:

- Centralized Management: The CI Class Manager provides a centralized place to view and manage the CMDB class hierarchy in a tree-view format. This allows for easy navigation and management of CI classes
- Class Definitions and Settings: Allows you to view, create, or edit basic class definitions and class settings for identification rules, reconciliation rules, and CMDB Health.
- Hierarchy and Relationships: You can view the hierarchy of CI classes and their parent-child relationships. This helps in understanding the structure and dependencies of different CIs.
- Attributes and Rules Management: The CI Class Manager enables you to manage attributes, identification rules, reconciliation rules, suggested relationships, and all relationships of a CI class.
- Health and Compliance: It helps in maintaining the health of the CMDB by allowing you to create compliance audits, certification filters, and templates. You can also set CI fields to be recommended or mandatory.
- Extensibility: The CI Class Manager supports the creation of new child classes or updating existing classes.
- Improved Data Accuracy: By managing identification and reconciliation rules, the CI Class Manager helps in ensuring data accuracy and consistency within the CMDB

**IMPORTANT**: While it is possible to create new CMDB classes using the CI Class Manager in ServiceNow, this should be done with caution. There are potential license, governance, and insight implications, and you might inadvertently duplicate existing classes.

By avoiding the creation of new CMDB classes, you can maintain standardization, simplify maintenance and upgrades, ensure interoperability, preserve data quality and integrity, and take advantage of available support and community resources. This approach ultimately leads to a more efficient, reliable, and cost-effective CMDB.

Consulting the ServiceNow documentation and engaging with the ServiceNow Community can provide valuable guidance to achieve the best outcomes.

If a new class is needed, before creating a new class, be sure to first install the ServiceNow [CMDB CI Class Models(opens in a new tab)](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ae99d84b2320330006c0110d96bf65b3/1.59.1?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%25253Bgenerative_ai%25253Bsnow_solution%26q%3Dci%2520class%2520model&sl=sh) store application which provides lots of additional classes that have been prescribed by ServiceNow. It is very possible that a base system class exists that your organization can leverage. If not, it is recommended to extend an existing class with the new class.

Be aware that only users with the following roles can create new classes:

- sn_cmdb_admin and personalize_dictionary
- admin

If you are planning to eliminate technical debt and want to remove a custom class, it recommended to do the following:

- Utilize CI Class Manager to identify a baseline class that a custom class can be moved into.
- Move CIs from custom classes to standard ServiceNow classes, mapping attributes correctly.

### Basic Info and Attributes

Leading Practices: Building a comprehensive CMDB immediately is a common mistake. Instead, begin with a simple approach and make incremental improvements as your configuration management capabilities grow. Leverage the Principal Class feature to identify the CI classes and attributes necessary to meet the data requirements of your defined use cases.

Fields:
- **Managed By Group** - Please note that the Managed By Group can also be configured through a technical service offering. If set there, it will take precedence over the value set in the CI Class Manager.

### Identification Rule and Dependent Relationships
Key Features of Dependent Relationships:

1. **Dependency Mapping**: Identifies how one CI depends on another. For example, an application might depend on a server to function.
2. **Impact Analysis**: Helps in assessing the impact of changes or outages. If a server goes down, you can quickly see which applications are affected.
3. **Lifecycle Management**: Ensures that changes to a CI’s lifecycle (e.g., decommissioning) are appropriately managed for all dependent CIs.

### Reconciliation Rules and Suggested Relationships

## IRM(Identification & Reconciliation Engine)
The Identification and Reconciliation Engine, also known as the IRE, is a framework that processes payloads in order to maintain the Configuration Management Database (CMDB). This would include the creation of new configuration items (CIs) and updates to existing CIs. In addition, data collected from many different sources (e.g., Discovery, AWS, SCCM) can be ingested into the CMDB, causing data attributes to flop back and forth between various sources depending on which source did the last update.

The IRE is crucial and a central component to ingesting healthy data into the CMDB. It ensures accurate and consistent data by identifying and reconciling configuration items (CIs) from multiple data sources. The IRE helps maintain the integrity of the CMDB by reducing duplicate CIs and controlling updates to CIs when multiple data sources, such as Discovery, Service Mapping, Service Graph Connectors, and REST integrations are used to create and update CI records.

### Features
#### Identification
Process of uniquely identifying CIs to determine if the CI already exists in the CMDB or if it is a newly discovered CI that must be added. The identification process relies on identification rules to uniquely identify CIs based on their attributes, ensuring that each CI is accurately recognized across different data sources.
#### Reconciliation
Process of reconciling CIs and CI attributes by allowing only designated authoritative data sources to update records in the CMDB at the CI table and attribute level. The reconciliation process relies on reconciliation rules and data refresh rules. These rules define how data from multiple sources is merged and prioritized, ensuring that the most accurate and up-to-date information is retained in the CMDB.
#### Deduplication
When CIs are ingested into the CMDB and the IRE encounters duplicate CIs during the Identification and Reconciliation process, it groups each set of duplicate CIs into a de-duplication task. Duplicates can then be reviewed to determine their origin, and management tools such as the de-duplication wizard and de-duplication templates can be used to assist in the remediation process.
#### Reclassification
During the CI identification process, a matched CI might need to be upgraded, downgraded, or switched to another CI class. If automatic reclassification is disabled, then the system generates a reclassification task. Review the information in these tasks, and decide whether a manual reclassification of the CI is appropriate.
### Data Ingestion via the IRE
The IRE provides a centralized set of APIs compatible with various discovery and integration tools, such as Discovery, Service Graph Connectors, or IntegrationHub ETL. It enforces the IRE process before data is stored in the CMDB, ensuring that data sources do not write directly to the CMDB. Instead, these sources call the APIs first to prevent inconsistencies, such as duplicate CIs or updates from unauthorized data sources.

### Overall IRE Process Flow

![[ire-process.png]]

## Identification Rules
### Overview
ServiceNow identification rules play a critical role in ensuring the integrity and accuracy of the Configuration Management Database (CMDB). They are used to uniquely identify configuration items (CIs) and prevent the creation of duplicate records.

Identification rules are designed with a unique identifier for CIs using a set of defined attributes. When a CI is discovered or imported into the CMDB, these rules help determine whether the CI already exists in the database or if it should be created as a new record.

The most efficient way to populate the CMDB is through automated discovery tools, such as ServiceNow Discovery or third-party tools like System Center Configuration Manager (SCCM). However, many CMDBs struggle with inaccurate data. When the enterprise CMDB data is inaccurate, the reports and processes that rely on it can fail, putting the organization at risk. Leveraging identification rules that are part of the IRE process helps ensure data in the CMDB is more accurate with less duplicates.
### Why Configure Identification Rules?
- **Data Integrity**: Prevents duplicate CIs, ensuring that each CI in the CMDB is unique and accurately represented.
- **Consistency**: Provides a centralized method for identifying CIs across different data sources and discovery methods.
- **Efficiency**: Automates the process of CI identification, reducing manual effort and errors.
- **Improved Data Quality**: Ensures that the CMDB contains accurate and up-to-date information, thereby enhancing the effectiveness of other ServiceNow products that depend on this data to make better decisions.

### Identification Process
The identification process is part of the overall IRE process flow. The identification process happens before a CI is updated in the CMDB and includes the following areas.

- **Data Ingestion:**
    - Data is ingested from various discovery tools, integrations, and data sources.
    - When data is ingested into the CMDB, it is processed by the Identification and Reconciliation Engine (IRE). The IRE uses the identification rules to determine if an incoming CI matches an existing record in the CMDB.
- **Attribute Matching:**
    - The IRE compares the attributes of the incoming data, as defined in the identification rules, with the same attributes of CIs in the CMDB. If a match is found, the existing CI is updated. If no match is found, a new CI record is created.
- **Duplicate Prevention:**
    - By using identification rules, ServiceNow ensures that duplicate CIs are not created. This maintains the integrity and accuracy of the CMDB.

### Identification Rules
Identification rules help manage all hardware and applications that are inserted or updated in the CMDB by using specific hardware and application rules.  

Both of the problems listed below can occur when the attributes used to identify configuration items do not properly represent the unique identity of a CI.  

- **Duplicate CIs:** Occur when duplicate CIs are in the CMDB that represent a single CI. This situation may occur if the identification rules for CIs do not ensure that each CI is uniquely expressed with identifier entries that do not change.
- **Overloaded CIs:** an opposite problem to duplicate CIs, overloaded CIs are when different CIs are identified as the same CI and one CI is created when several CIs should have been created.

Identification rules can be viewed or configured from the left navigation pane under the CI Identifiers module or via CI Class Manager from the Identification Rule tab within any class. ServiceNow provides hundreds of rules out-of-the-box to assist with the identification process.
### Choosing the Correct Identification Method
Just as a driver’s license or passport uniquely identifies and differentiates individuals, configuration items (CIs) in a CMDB require their own unique identifiers. Identification rules consist of identifier entries that include criterion attributes specific to each configuration item.

For an identification rule to be effective, it must satisfy two criteria:
1. The identifier entry criterion attributes must be unique to that configuration item (i.e., serial number, host name, install directory, config file path).
2. The identifier entry criterion attributes must not change for the life of the configuration item (i.e., Serial number as IP address may change over time for the same CI and is not considered a solid choice).

### Optional IRE Condition
In ServiceNow, the Identification and Reconciliation Engine (IRE) is responsible for identifying and reconciling configuration items (CIs) within the CMDB. An optional IRE condition allows for the addition of extra criteria to fine-tune the identification and reconciliation process.

By default, optional conditions can be applied to any lookup-type field when creating identifier entries. However, to extend these optional conditions to non-lookup type fields, you must enable the following system property by setting it to **true**.

### IRE Support for  Non-CMDB Tables
Many non-CMDB tables struggle with poor data quality because they lack mechanisms to enforce quality rules during data import, manual entry, and updates. The Identification and Reconciliation Engine (IRE) supports some non-CMDB tables. This allows customers to apply IRE processes to these tables, enhancing data integrity and overall health.

Only non-CMDB tables that are preset in the base system are supported.
- Location `[cmn_location]`
- Department `[cmn_department]`
- Cost Center `[cmn_cost_center]`
- Building `[cmn_building]`
- User `[sys_user]`
- Group `[sys_user_group]`

The CI Class Manager cannot be used to manage any IRE-related rules for non-CMDB tables. Instead, you must work directly with the respective tables in list views to create and manage those rules as described.

## Reconciliation Rules
### Overview
ServiceNow Reconciliation rules are used by the Identification and Reconciliation Engine (IRE) to determine how to merge and update configuration item (CI) classes and attributes when data is ingested from multiple sources into the Configuration Management Database (CMDB). These rules help ensure that the most accurate and authoritative data is retained in the CMDB.

ServiceNow does not provide any reconciliation rules in a baseline instance, as the configuration of rules is very specific to customer environments and the classes customers plan to manage. As a good practice, ServiceNow encourages customers to ensure they configure reconciliation rules for each data source that is authorized to update CIs in the CMDB.

When properly configured, reconciliation rules can manage 90% of the process to determine which data sources are trusted and identify the ultimate authoritative source of truth for a specific class, set of classes, and/or CI attributes.

### Why Configure Reconciliation Rules?
Understanding and controlling which data sources are updating CMDB data is crucial to trusting the data in the CMDB.

- **Data Accuracy:** Ensure the CMDB contains the most reliable and up-to-date data.
- **Conflict Resolution**: Resolve conflicts between data from different sources.
- **Data Prioritization**: Determine which data source should take precedence when multiple sources provide information for the same CI class and/or attributes.

### Reconciliation Process
The reconciliation process is part of the overall IRE process flow. The reconciliation process follows the identification process before a CI is updated in the CMDB. Note that the reconciliation process is not part of the creation process of a CI.

- **Data Ingestion:**
    - Data is ingested from various discovery tools, integrations, and data sources.
    - The Identification and Reconciliation Engine (IRE) processes this incoming data.
- **Identification Process:**
    - Before reconciliation, CIs are identified using identification rules to ensure that each CI is uniquely recognized.
- **Reconciliation Process:**
    - Reconciliation rules are applied to determine how and if the incoming data should update the existing CIs in the CMDB.

**How to Prevent Inserts?**  
Reconciliation rules help prevent updates from unauthorized sources or lower-priority sources from overwriting data provided by higher-priority sources, focusing specifically on updates. To further refine control and block inserts from a specific data source, a CMDB administrator can configure IRE Data Source Rules by navigating to: **Configuration > Identification/Reconciliation > IRE Data Source Rules.**

The **Data Source Histories `[cmdb_datasource_last_update]`** table in ServiceNow is used to track the last update time for each data source that contributes data to the Configuration Management Database (CMDB). This table is populated only after reconciliation rules are configured for a specific class and data is ingested into that class.

### Data Refresh Rules
ServiceNow Data Refresh Rules are designed to manage how and when data is refreshed in the Configuration Management Database (CMDB). These rules help ensure that the CMDB remains up-to-date with the latest information from various data sources while maintaining data accuracy and integrity. 

Within CI Class Manager, for a specific class, under the Reconciliation Rules tab, there is an optional configuration to define a data refresh rule. This rule allows an administrator to configure a time interval during which a class must be updated by a higher-priority data source. If the higher-priority data source does not perform an update within the given interval, ServiceNow will then allow any lower-priority data source(s) to perform the update.

## CMDB 360/Multisource CMDB
### Overview
CMDB 360/Multisource CMDB  retains complete history about discovery sources and proposed values, involved in updates of CI attributes.

The advantage of using CMDB 360/Multisource CMDB data is to:
- Track how the CMDB is populated by various discovery sources at the CI attribute level 
- Revert CI updates from a specific discovery source
- Recompute attribute values using updated reconciliation rules

When multiple discovery sources attempt to update the same CI attribute, the Identification and Reconciliation Engine (IRE) uses reconciliation rules to select a single discovery source for the update. Without a CMDB 360/Multisource CMDB, details about the lower-priority discovery sources whose values were rejected, are discarded and lost therefore making it practically impossible to identify CI attribute values that come in from lower priority data sources.

With CMDB 360/Multisource CMDB, the raw details for every discovery source are retained, both for discovery sources that were selected for an update and all others that were not. 

CMDB 360/Multisource CMDB, consisting of records from each discovery source is stored in the **CMDB MultiSource Data `[cmdb_multisource_data]`** table. CMDB administrators can examine, query, and report on this CMDB 360/Multisource CMDB data store to fully understand how and where the CI data came from and what other data values have been rejected for specific attributes of a CI record.

### Multisource CMDB Use Cases
Prior to the Paris release, when reconciliation rules are configured, the ServiceNow CMDB only had a method to track the last data source that updated a record and its CI attributes. This information is stored in the **Data Source Histories [cmdb_datasource_last_update]** table. 

Having the ability to easily answer the following questions was very difficult:

- What are all my discovery sources for backup servers?
- Show me all servers where the reported RAM is different between SCCM and ServiceNow Discovery
- How can I check for data gaps between my discovery sources?
- Refine reconciliation rules according to the reported quality of updates from specific discovery sources?
- How many data sources do I have that collect the same data on my Linux servers?

With the Paris release, the **CMDB MultiSource Data `[cmdb_multisource_data]`** table was introduced to track all CI records and their attributes, including the data sources that last updated the record or were rejected due to reconciliation rules. This multisource data can be accessed from a CI record, CI Class Manager, and CMDB Workspace.

**CMDB 360/Multisource CMDB solves the following:**
- Inability to store all CI data ingested by various discovery sources
- Inability to find the reported value from multiple discovery sources
- Inability to remove and replace data from an incorrect discovery source
- Inability to modify reconciliation rules and recompute the data immediately

### Activating CMDB 360/Multisource CMDB
Activating the ServiceNow CMDB 360/Multisource CMDB involves several steps to ensure that the plugin is properly configured and that data from multiple sources can be integrated seamlessly. Here’s a guide to help you activate and configure the CMDB 360/Multisource CMDB in ServiceNow:

- Activate ITOM Discovery License `(com.snc.itom.vis.license)` plugin  
    - Navigate to **System Applications > All Available Applications > All**.  
    - Search for and install the **ITOM Discovery License** plugin.
- Configure the System Property:  
    - Navigate to **System Properties > All Properties**.  
    - Set **`glide.identification_engine.multisource_enabled`** to **true**.  

Other useful system properties that can be leveraged include:

- **`glide.cmdb.logger.source.cmdb_multisource`**: Enables logging for CMDB 360
- **`glide.identification_engine.multisource.recompute.max.ci.limit`**: Maximum number of CIs that can be included in a CMDB 360 recompute operation
- **`glide.identification_engine.multisource_cmdb_ci_enabled`**: Enables capturing CMDB 360 data for CIs from CMDB classes (derived from the `cmdb_ci` class)

By following these steps, you can activate and configure the ServiceNow CMDB 360/Multisource CMDB to effectively integrate and manage data from multiple sources.

### Visibility to CMDB 360/Multisource CMDB Data
After CMDB 360 is enabled and data is populated in the CMDB 360/Multisource CMDB data table, visibility and insight into the data can be performed from multiple areas of the platform including:

- CI Class Manager
- CMDB 360 Data Preview link
- Multisource Data related list
- CMDB Workspace

The data under the CMDB 360 view populates each day after the following scheduled job executes:
- Multisource Dashboard Analytics Population

## Dynamic Reconciliation Rules
### Intro
ServiceNow dynamic reconciliation rules are designed to handle complex data reconciliation scenarios by leveraging Multisource CMDB data. They help ensure that the Configuration Management Database (CMDB) contains the most accurate and relevant information when multiple data sources are involved.

As learned in the previous lesson, a static reconciliation rule defines which class attributes discovery sources are authorized to update and prevents unauthorized sources from overwriting these values. It also establishes the priority among multiple discovery sources. Without static reconciliation rules, discovery sources could overwrite each other’s updates to attribute values.

Dynamic reconciliation rules use Multisource CMDB data to select values based on criteria such as the largest or first reported value within the Multisource CMDB. When both static and dynamic reconciliation rules apply to the same CI attribute, the dynamic reconciliation rule takes precedence.

**NOTE:** The Dynamic Reconciliation Rule option is only available after the Multisource CMDB is enabled. The reconciliation rule described in the previous lesson is renamed to Static Reconciliation Rule to differentiate the two rules types.

### Dynamic Reconciliation Rule Types
**Dynamic reconciliation rules support several rule types such as:**
- First Reported 
- Most Reported
- Last Reported
- Largest Value
- Smallest Value

**NOTE:** The largest and smallest value types only apply to numeric field types. When on the Select Attributes tab of the Create Reconciliation Rule wizard, only numeric field types are displayed and the other attributes are hidden.

When applying a dynamic reconciliation rule, the IRE first processes the current payload and then reviews the Multisource CMDB data to determine the appropriate value for updating the CMDB. Depending on the type of dynamic reconciliation rule, selecting the correct value may not always be straightforward. For instance, there might not be a single most-reported value, or the last discovered timestamp might not be available. In such cases, the IRE will use additional details—such as last reported, last discovered, and last updated values—to determine the most suitable value.

### Dynamic Reconciliation Rule Advantages
Using dynamic reconciliation rules is optional and only available when Multisource CMDB is enabled, however several advantages can be gained by implementing them.

![[dynamic-reconciliation-rule-advantage.png]]

