---
title: Ingest Data into the CMDB
tags:
  - ServiceNow
  - CMDB
  - Ingest
---
## Introduction
### Overview
ServiceNow CMDB (Configuration Management Database) provides a suite of management tools designed to help organizations effectively ingest, manage, and maintain their configuration items (CIs) and relationships. 

After ingesting data, a substantial(实质性) amount of valuable CI data is available in the ServiceNow CMDB. As a crucial next step that is often forgotten, ServiceNow strongly recommends that the CMDB team supplement the discovered data collected by the automated discovery tools with non-discoverable data, such as group and location information.

This lesson covers various ServiceNow tools for data ingestion and concludes with automated techniques for associating non-discoverable group data to CI data.

![[cmdb-tools-for-three-pillars.png]]

### CMDB Injestion
ServiceNow offers several products and features designed to collect and populate data into the CMDB. These tools help ensure that the CMDB remains accurate, comprehensive, and up-to-date. 

Here are some of the primary ServiceNow products used for this purpose:
- **ServiceNow Discovery (AKA: Horizontal discovery, Agentless discovery, IP-based discovery)**
	- **Automated Discovery:** Automatically discovers devices and applications in your network, populating the CMDB with accurate and up-to-date information.
	- **Infrastructure Mapping:** Identifies and maps dependencies between network devices, servers, and applications.
- **Service Mapping(AKA: Top-down discovery, Tag-based discovery, ML-powered mapping)**
	Creates a complete and accurate map of the services within your organization, showing how they are supported by underlying infrastructure and applications.
	- **Top-Down Mapping**: Maps services to their supporting IT components including relationships.
	- **Dynamic Updates:** Automatically updates service maps as changes occur in the environment.
- **Agent Client Collector** **(AKA: ACC, Agent-based discovery)**
	ACC requires an agent installed on each target host, which provides real-time visibility into endpoint configurations, helping IT teams maintain an up-to-date CMDB. In addition, it collects software utilization data, which is not possible without an agent, supporting Software Asset Management use cases.
	- **Hardware Inventory:** Collects detailed information about the hardware components of endpoints, including CPUs, memory, disk drives, network interfaces, and more.
	- **Software Inventory:** Gathers information about installed software, including versions, installations, and usage metrics.
	- **Configuration Details:** Captures system configuration details, including OS settings, patch levels, and network configurations.
- **Service Graph Connectors**
	Facilitates integration between ServiceNow and external systems to import and synchronize data.
	- **Pre-Built Connectors:** Integrate data from popular IT management tools, cloud services, and other third-party applications (e.g., Azure, InTune, MS SCCM, Jamf, AWS).
	- **Data Consistency:** To ensure consistency and accuracy of configuration data across different systems.
- **IntegrationHub ETL**
	ServiceNow IntegrationHub ETL (Extract, Transform, Load) is a feature designed to simplify and automate the process of importing and integrating data from various external sources into the ServiceNow AI Platform, particularly into the CMDB, though non-CMDB, foundational tables are also supported.
	- **Data Integration:** Facilitates the seamless import of data from external sources into ServiceNow.
	- **Data Transformation:** Allows data to be transformed and normalized according to the ServiceNow data model before being loaded into the CMDB or other applications.
	- **Automation:** Automate the ETL process, reducing manual intervention and ensuring consistent data updates.
- **Import Sets and Transform Maps**
	In ServiceNow, using import sets and transform maps is the oldest method for importing and transforming data into the CMDB.
	- **Data Staging:** Import Sets temporarily hold data extracted from external sources such as CSV files, Excel spreadsheets, databases, or APIs.
	- **Field Mapping:** Define how fields in the Import Set Table map to fields in the target CMDB tables.
	- **Transform Scripts:** Write scripts to handle complex data transformations, calculations, or formatting.
	**Requires Paid License:** No. Accessible from the System Import Sets application.

## ServiceNow Discovery
### Overview
ServiceNow Discovery is an automated discovery solution that scans and detects all components within an IT infrastructure on a scheduled basis, ensuring the Configuration Management Database (CMDB) remains accurate and up-to-date with the collected information.

Available as a separate subscription from other products on the ServiceNow AI Platform, ServiceNow Discovery identifies devices such as computers, servers, printers, and various IP-enabled equipment, along with the applications running on them. It then updates the configuration items (CIs) in the CMDB with this data.

The ServiceNow® ITOM Visibility product includes ServiceNow Discovery. However, when engaging with different individuals within the ServiceNow ecosystem, ServiceNow Discovery may also be referred to by the following terms:
- Horizontal discovery
- Agentless discovery
- IP-based discovery

ServiceNow Discovery supports a wide range of platforms, including Windows, Linux, macOS, and cloud environments. It collects data such as operating system, installed software, running processes, and other configuration details. In addition, all data collected is sent to the IRE for processing to avoid duplicate records in the CMDB.

ServiceNow Discovery is schedule based; therefore, it is not considered a real-time discovery solution. For true real-time discovery, ServiceNow offers Agent Client Collector.

### Discovery Phases
#### Scan Phase
Discovery begins by scanning the network to identify all IP-enabled devices. It performs a sweep of IP addresses or ranges to detect live hosts within the network.

#### Classification Phase
Once devices are detected, Discovery classifies them based on their type, such as servers, routers, switches, printers, or specific software applications. It uses probes and sensors to determine the device type.

#### Identification Phase
In this phase, Discovery identifies the devices uniquely by gathering identifying attributes, such as a server's serial number, MAC address, hostname, or IP address. This ensures that each configuration item (CI) can be correctly matched and updated with a CI in the CMDB using identification rules or created if no match is found.

#### Exploration Phase
Discovery then collects detailed data about each identified device. This may include installed software, hardware configurations, network interfaces, running processes, and services. The depth of information depends on the type of target being explored.

Discovery uses a combination of Discovery probes and patterns to collect the details of a device.

### **MID Server**
The **ServiceNow MID Server** (Management, Instrumentation, and Discovery Server) plays a critical role in the ServiceNow Discovery process, especially for environments where direct communication between ServiceNow and network devices is restricted due to security, firewalls, or network segmentation. The MID Server acts as a bridge between the ServiceNow instance and the organization's internal network.

The MID Server operates within an organization's trusted network environment, ensuring that sensitive data and credentials never leave the organization's boundaries. It uses encrypted communication to securely transmit data between the MID Server and ServiceNow.

Here's how it supports Discovery:
The MID Server enables secure communication between ServiceNow and devices or applications in the internal network. It handles all network scans and interactions with systems that reside behind a firewall or in remote locations, ensuring that ServiceNow doesn’t require direct access to internal systems.

During the Discovery process, ServiceNow sends **probes** (requests for information) to the MID Server, which executes them against the target systems. The MID Server then collects the responses and returns them to ServiceNow, where **sensors** process the data and update the CMDB.

As Discovery is agentless, the MID Server probes devices without permanent software. It uses WMI to discover Windows machines, uses SSH to connect to Unix or Linux computers, runs commands to gather information, and employs SNMP to collect data from network switches or printers.

### Discovery Schedules

**Discovery Admin Workspace**

The Discovery Admin Workspace Schedules page acts as a central hub for overseeing the performance of all Discovery operations. This workspace enables efficient management of Discovery schedules and statuses, giving administrators real-time visibility into daily Discovery activities.

A Discovery schedule defines the parameters for horizontal Discovery, including the scope of the searches, the timing of those scans, and the assigned MID Servers. You can create schedules tailored to your local environment or to detect resources within your cloud service account.

These schedules trigger horizontal Discovery, which uses probes, sensors, and pattern-based operations to systematically scan your network and identify configuration items (CIs).

### Types of  Discovery
- Network discovery
- CI discovery
- Cloud discovery
- Serverless discovery
![[types-of-discovery.png]]

### Limiting Discovery Data
Limiting discovery data initially when running ServiceNow Discovery offers several important benefits, particularly during the early stages of configuring and populating your Configuration Management Database (CMDB).

### Discovery Ranges
Discovery uses several methods to define the network or network segment to be scanned. You can choose to include or exclude specific IP ranges from your scans by setting specific ranges.

You also have the option to scan an entire IP network, covering the full range of available IP addresses within that network. This is not recommended during an initial implementation to prevent data overload, where an excessive amount of irrelevant or unnecessary data can clutter the database.

Configuring a schedule and setting the discovery range this way includes both the network address (the lowest address in the range) and the broadcast address (the highest address in the range). By setting the range in this manner, ServiceNow Discovery will attempt to scan a large number of target IP addresses.

**Broader Discovery Range using Subnets:**

- 192.168.0.0/24
- 10.11.128.192/26

The broadcast address can lead to significant errors in the Discovery data. It returns all devices within the network along with the network address, potentially including a large number of redundant devices. This inherent control feature makes IP networks the most efficient method for specifying which IP address ranges to query.

To avoid performance issues, limit Discovery schedules to a maximum range of /16, which encompasses no more than 65,000 IP addresses. Alternatively, consider dividing the Discovery schedules into smaller IP address ranges.

Configuring a schedule and setting the discovery range this way excludes the network and broadcast addresses. In addition, the ranges are configured to target a small range of IP addresses to allow for simplified CMDB management. It is important to be prescriptive on the IP ranges and know, if possible, if these target ranges include devices that the CMDB team wants to manage.

Starting with a small IP range offers the advantage of collecting a more controlled set of discovery data, making the troubleshooting process more manageable and improving data quality. This approach allows you to quickly identify and resolve issues before scaling the discovery process to cover a larger IP range, which will inherently include a broader variety of device types and applications.

**Limited Discovery Range:**

- 192.168.0.1–192.168.0.254
- 10.11.128.193–10.11.128.254

### Discovery Configuration Console
The console provides configuration options to specify which types of devices, applications, software files, and software configuration items (CIs) you want Discovery to detect. If you choose to exclude a CI from scanning, the instance disables the corresponding probe or classifier used by Discovery to identify that CI.

This feature is helpful for CMDB teams that have identified principal classes they want to manage, allowing them to focus Discovery on those specific device classes while excluding others.

The Discovery Configuration Console can be accessed by navigating to **Discovery Definition > Configuration Console**.

### Discoverable Data
ServiceNow Discovery collects detailed hardware, software, and network device data, which is known as discoverable data. Examples of discoverable data are:

- **Hardware details** (e.g., CPU, memory, storage)
- **Software details** (e.g., installed applications and operating systems)
- **Network details** (e.g., IP addresses, MAC addresses, network topology)
- **Cloud resources** (e.g., AWS, Azure, Google Cloud)
- **Discovery source** ServiceNow

After ServiceNow is scheduled, it will on an ongoing basis keep the Configuration Management Database (CMDB) up-to-date by regularly scanning the IT infrastructure for changes to any discoverable data.

**IMPORTANT**: When Discovery identifies a device, it is added to the CMDB with the discovery source field set to ServiceNow. If a record already exists in the CMDB but was not discovered—such as one created through Asset Management—its discovery source will initially be listed as SNAssetManagement. Once the device is discovered by ServiceNow Discovery, this field is updated to ServiceNow.

### Non-Discoverable Data
After ingesting data using ServiceNow Discovery, Service Mapping, and/or Service Graph Connectors, a substantial amount of valuable CI data is available in the ServiceNow CMDB. As a next step, it is crucial for the CMDB administrator to supplement the discoverable data collected by the automated discovery tools with non-discoverable data, such as group and location information.

Groups are essential when incidents are opened against CIs or when changes need to be made. Accurate group information is vital for streamlining these processes. Examples of non-discoverable data are:

- Assigned to
- Owned by
- Support group
- Change Group
- Managed By Group

## ServiceNow Service Mapping
### Overview (Top-Down)
Traditionally, IT organizations have been responsible for managing infrastructure. However, there is a drive by IT to create alignment between how IT and the business view how a service is delivered. Forward-thinking IT organizations are starting to care less about specific compute infrastructure, such as servers or routers, and care more about the critical services they use to:

- run operations
- provide to their customers
- drive corporate revenues
- increase IT efficiency
- create new business strategies

Rather than focusing on specific infrastructure, IT is starting to set goals to ensure that their services are highly available, responsive, and cost-effective. To accomplish this, an organization has to know how these services are delivered. **Service maps provide enterprise visibility and an understanding of what CIs are critical in supporting a particular service.**

**Service Map**
ServiceNow offers a solution to automate the discovery and maintenance of service maps with its Service Mapping product which discovers and models the relationships and dependencies between discovered CIs that make up a service and automatically populate this information into the CMDB.

These service maps allow team members that support Service Management processes, such as Incident, Problem, and Change, to gain instant visibility of what CIs support critical services in their organization. For example, the loss of disk drives may take a database instance down, which affects the requisition service the HR department uses to order equipment for new employees.

### Bridge the Gap between IT Operations and Business Users
A gap exists in many enterprises where IT has traditionally managed their business through technology domains, while the end users who are the customers of IT, consume services. Often, IT has a difficult time mapping services to the infrastructure that supports it.

### Planning for a Successful CMDB Deployment with Service Mapping
The most effective CMDB’s are populated using automation with tools like Service Mapping Discovery. 90% of the data in your CMDB should be automatically populated, leaving the other 10% to be updated manually after proper governance.

The problem is that there are usually no maps that show which IT components work together to deliver a particular service. 

For example, a customer portal may depend on multiple applications, middleware, virtualized and physical servers, and network connections. When any of these components fail—or the connections between them fail, the service is impacted. Without a map, it is almost impossible to know why a service is down or performing poorly for a company's business users. 

With Service Mapping, the map is automatically built upon discovery with the proper CI relationships and attribute details. The appropriate tables in the CMDB are updated with the mapped CIs and their attributes according to Identification and Reconciliation rules (part of the governance plan). This **map** represents the nearest real-time configuration of the application service.
#### Gain visibility across your entire operational estate
When you think about all the resources being deployed and removed daily, how are you going to manage the costs and risks associated with these to your business if you don’t have visibility to them?

- Discover your infrastructure and applications
	The first step is to discover your infrastructure and applications regardless of their location. From the datacenter to the cloud and beyond, it is critical to have visibility across your entire estate to achieve value from your strategic initiatives.
- Discover your services
	The second step is to discover your services to gain business context for how infrastructure and applications support the business.
	
	Going back to our strategic initiative of aligning IT with the business, the way to achieve this is by discovering your services.
- Unify enterprise-wide configuration data
	By completing the first two steps, you will have a central system of record of configuration data (CMDB) that will drive outcomes and empower data-driven decisions for your business.

### What is an Application Service?
It is a service type that logically represents a deployed system, application, or product stack.
- First and foremost, it is an **operational CI** that is used in your ITSM and ITOM Health best practices.
- It is a **unique instance and/or version** of an application or product in your ecosystem.
- May be created per **Environment**—e.g., Dev, Test, QA, Prod.
- May be created per **Geographic region**—e.g., AMS, EMEA, APJ.
- May represent an **Organization or Line of Business**—e.g., HR, Marketing, Sales, Delivery, Manufacturing.
- It is stored in the **Application Service parent class** `[cmdb_ci_service_auto]` or one of its sub-classes.
### Common Service Data Model
The Common Service Data Model (CSDM) provides a standardized set of terms and definitions for all ServiceNow products on the ServiceNow AI Platform, forming the foundation for CSDM guidelines. These terms enable consistent service reporting and offer prescriptive guidelines for service modeling within the CMDB.

Service Mapping supports CSDM by adding automation to the discovery and maintenance of application services, their underlying components, and relationships, as shown in the **Service Delivery** domain for CSDM 5.0.

CSDM value received from implementing Service Mapping includes the following:

- **Accurate Service Modeling**: Service Mapping identifies and maps all components within a service, such as applications, infrastructure, and dependencies, which aligns with the CSDM framework for representing IT services in the CMDB.
- **Enhanced Data Quality**: By automatically populating the CMDB with accurate service and dependency information, Service Mapping helps ensure the CMDB data adheres to CSDM standards, which are essential for consistency across ServiceNow applications.
- **Dependency Management**: Service Mapping maps relationships among CIs and services, providing the foundation for dependency management that is key to CSDM’s guidelines for service health, impact analysis, and operational support.


## Agent Client Collector
### Overview
**ServiceNow Agent Client Collector (ACC)** is a lightweight agent-based solution designed to perform **discovery** and **real-time monitoring** of infrastructure components, including servers, cloud resources, and applications across an organization. ACC is a key part of the ServiceNow IT Operations Management (ITOM) suite, enhancing visibility and control over the IT environment.

ACC is a single agent for ServiceNow and is a key enabler for the following ITOM use cases:
- Visibility and Monitoring
- Software Asset Management
- Security Incident Response
- Service Management
- Discovery of workstations that intermittently connect to the network
- Discovery of devices in a secure network where the security team does not want external discovery solutions to remotely connect to them

### Key Features
- Real-Time Monitoring
- Data Collection
- Integration with CMDB
- Support for Multiple Platforms
![[acc-key-features.png]]

## IntegrationHub ETL (Extract, Transform, Load)
### Overview
The ServiceNow IntegrationHub ETL Store application is designed to create and manage ETL (Extract, Transform, Load) transform maps, which integrate third-party data into the CMDB or non-CMDB tables while ensuring data integrity.

IntegrationHub ETL offers a user-friendly interface to guide users through the integration process, including the option to run test integrations with sample data. Transform maps allow you to modify source data and map it to target tables. During this process, small data sets can be used for testing, and mappings can be reviewed, tested, and rolled back if needed. Imported data is automatically processed through the Identification and Reconciliation Engine (IRE) to enhance data quality and minimize duplicates.

ServiceNow Service Graph Connectors leverage IntegrationHub ETL transform maps to prepare data for ingestion into the CMDB. A CMDB administrator can preview and adjust mappings using IntegrationHub ETL.

**Why use IntegrationHub ETL?**
- **Data Integrity:** A seamless way to route data via the Identification and Reconciliation Engine (IRE) to maintain CMDB’s integrity.
- **Consistent and Efficient**: IntegrationHub ETL simplifies the process of transforming source data and mapping it to target tables.
- **Improved Data Quality**: Create transforms and mappings using a small sample data set, test-run the definition on that data set, review the results, and “rinse and repeat” as needed until the desired outcomes are achieved.

### IntegrationHub ETL
The two key components that IntegrationHub ETL uses for processing are:

- **Robust Transform Engine (RTE)**: Used to transform raw source data stored in staging tables into mapped and integrated data for the CMDB. It utilizes ETL transform maps created specifically for the integration process to carry out the data transformation.
- **Identification and Reconciliation engine (IRE**): Serves as a centralized framework for managing identification and reconciliation processes across various data sources. IRE ensures data integrity by preventing conflicts and maintaining accuracy, both within the CMDB and in other supported non-CMDB tables.

![[process-flow-integrationhub-etl.png]]
Process Flow

---
IntegrationHub ETL leverages the RTE and IRE components to streamline data processing and integration. First, data is imported from external sources and temporarily stored in staging tables as Import Sets.

Next, RTE uses the data from these staging tables, along with ETL transform maps created within IntegrationHub ETL, to generate IRE payloads. These payloads are then handed off to IRE for processing.

IRE performs reconciliation to prevent issues like duplicate configuration items (CIs) and ensures the integrity of the target tables before the data is integrated.

Finally, the processed data is stored in the CMDB, which serves as the system of record, keeping accurate and up-to-date information from multiple data sources.

### IntegrationHub ETL Terms

**CMDB Application:** Name of the third-party vendor such as _SCCM_. Ensure a discovery source for the application is configured.

A CMDB application has two associated attributes: Name and Discovery Source. One CMDB application can have multiple ETL transform maps, and each of those ETL transform maps is associated with a single Data Source.

**ETL Transform Map:** The output generated by IntegrationHub ETL. You can integrate third-party data into the CMDB or into non-CMDB tables using an ETL transform map which is configured for the respective integration.

**Data Source:** The source feed, such as _SCCM Computer Identity_, from which the raw source data is imported. If you use various REST endpoints for different types of data, each REST endpoint is associated with its own data source and an ETL transform map.

### Non-CMDB Table Support for IntegrationHub ETL
IH-ETL includes advanced functionality that allows data ingestion into non-CMDB tables.

A list of non-CMDB tables supported by default are specified in the system property **`glide.identification_engine.non_cmdb_tables`**. These are the only tables that IH-ETL and IRE can work with. In addition, identification rules, including CI identifiers and identifier entries, must be created for these tables.

The following non-CMDB tables are supported in the latest release.
- Location `[cmn_location]`
- Department `[cmn_department]`
- Cost Center `[cmn_cost_center]`
- Building `[cmn_building]`
- User `[sys_user]`
- Group `[sys_user_group]`

## Service Graph Connectors
### Overview
The CMDB is your organization’s digital foundation, and it is the foundation for ServiceNow. It is the central repository of configuration data needed to drive outcomes for your transformational goals.

To ensure your CMDB has business context and remains healthy and trustworthy, ServiceNow recommends ingesting data using automated methods. ITOM Visibility, using Discovery, Agent Client Collector, and Service Graph connectors provide the fastest time to value for gaining visibility of your entire operational estate, and drives differentiated outcomes with a vast set of solutions.

These connectors are designed to simplify the integration process without needing extensive customization. ServiceNow Service Graph Connectors are specialized integrations designed to help organizations import, normalize, and maintain high-quality data in their Configuration Management Database (CMDB) by connecting ServiceNow with external systems and data sources.

ServiceNow provides several out-of-the-box connectors to popular platforms like AWS, Azure, and VMware, ensuring easy setup and faster time-to-value. These connectors are designed to simplify the integration process without needing extensive customization. ServiceNow has connectors that fall into the following categories.

- Partner cloud providers
- Endpoint or IT asset management applications
- Monitoring and observability applications
- Security solutions
- Software, server, or network applications
- Operational Technology (OT) applications
- Partner-built connectors

### Breadth of Service Graph Connectors
ServiceNow has an ever-growing number of Service Graph connectors available in the ServiceNow store in categories such as Security, Monitoring, IOT, and Endpoint management sources.

Each connector has been reviewed to ensure data comes in properly, using the IRE to avoid duplicates and overwriting important data from each source. ServiceNow continuously improves the connectors when needs expand or problems arise, working with the partner product teams to ensure they work properly.

Each connector has been reviewed for CSDM conformance, ensuring the data and structure meet CSDM-prescribed guidance. Now all connectors leverage IntegrationHub ETL, which makes it easy for administrator to view and modify mappings if required.

ITOM visibility licensing is required to use Service Graph connectors that leverage the IRE with the exception of SCCM.

### Key Features
- Seamless Data Import
- Data Reconciliation and Deduplication
- Automation
- Security and Compliance
![[key-feat-of-service-graph-connectors.png]]

## Import Sets and Transform Maps
**IMPORTANT UPDATE:** 
This lesson explains how to import data into the CMDB using import sets, transform maps, and identification rules, which remains a viable solution. However, with recent releases, the IntegrationHub ETL application from the ServiceNow Store offers a more modern and simplified user interface for importing data into the CMDB, while natively utilizing identification rules to prevent duplicates.

Refer to the lesson on IntegrationHub ETL for more details.

## Populate Foundation Group Data
ServiceNow CMDB groups, dynamic CI groups, technology management services (formerly technical services), and technology management offerings (formerly technical service offerings) defined in the Common Service Data Model (CSDM) are essential components for managing foundation data across your IT landscape.

After ingesting data using ServiceNow Discovery, Service Mapping, and/or Service Graph Connectors, a substantial amount of valuable CI data is available in the ServiceNow CMDB. As a next step, it is crucial for the CMDB administrator to supplement the discovered data collected by the automated discovery tools with non-discoverable data, such as group and location information.

Groups are essential when incidents are opened against CIs or when changes need to be made. Accurate group information is vital for streamlining these processes.

**Key group fields to populate include:**

- **Managed By Group**: Used to streamline the assignment of Data Manager tasks for attestation, life cycle, and certification policies.
- **Support Group**: Maps to Incident Assignment Group to streamline incident routing.
- **Change Group:** Maps to Change Assignment Group to streamline change routing.

**Incident Routing:** is the process of automatically directing incoming incidents or support tickets to the appropriate teams or individuals within an organization based on predefined criteria. Effective incident routing ensures that incidents are handled promptly by the right resources, improving response times, reducing resolution time, and enhancing the overall efficiency of IT service management.

**Change Routing:** is the process of automatically directing change requests to the appropriate groups or individuals based on predefined rules or criteria within the Change Management process. It ensures that change requests are efficiently assigned to the right teams or approvers for evaluation, approval, and implementation, improving the workflow and minimizing the risk of delays or errors in handling changes.

After adding group data, it's crucial to audit it periodically to ensure accuracy. ServiceNow offers a tool called **Data Manager**, which allows CMDB administrators to easily configure certification policies. These policies can be scheduled to run regularly, with tasks assigned to groups or individuals to verify the accuracy of CI data.

### Two Methods to Auto-Populate Group Fields
ServiceNow provides two methods to streamline the population of group assignment attributes. A CMDB administrator can use either CI Class Manager or technology management offerings to manage the group fields.

**CI Class Manager**: Managed By Group

- Set the Managed By Group attribute for a specific class in the CI Class Manager.
- All CIs within the class will have their Managed By Group field populated based on the value specified in the CI Class Manager.

With this method, the Managed By Group setting is applied only to the CIs that aren’t associated with a technology management offering.

**Technology Management Offering**: Managed By Group, Support Group, Change Group

- Directly set the Support group, Change group, and/or Managed By Group attributes in the offering.
- Settings are applied to CIs that are associated with the offering.

For CIs that are managed by an offering, the Managed By Group field is first synchronized with its dynamic CI group. This field is then synchronized with the CIs that are part of that dynamic CI group, overwriting the entry from the CI Class Manager.

Both of these methods synchronize group attributes across all CIs that belong to the specified CI class configured in CI Class Manager or the group of CIs referenced from the offering.

The following diagram illustrates how group attributes can be managed using either method, however, technology management offerings offer a more comprehensive approach to manage groups. Support, change, and managed by groups can all be managed from the offerings, and take precedence over any configuration defined using CI Class Manager as indicated by the priority levels shown in the diagram (priority 1 and priority 2).

### Method1: CI Class Manager
CI Class Manager provides an easy method to populate the **Managed By Group** field data for a specific class.

For each class, CI Class Manager provides a **Managed By Group** field that if populated, is propagated to all CIs within the CI class, but not within the extended classes.

This field can be used to eliminate possible lack of knowing who is responsible for a class of CIs.

Upon saving a value populated in the **Managed By Group** field on a CI class in CI Class Manager automatically synchronizes the values to the underlying CIs of the class.

### Method 2: Technology Management Offering (using forms)
Technology management service offerings (formerly technical service offerings) help simplify and optimize the process of populating and maintaining group data across your enterprise infrastructure stored in the CMDB. Group information is critical when incidents are raised against CIs or when changes need to be implemented. Ensuring accurate group data is essential for improving the efficiency of these processes.

### Method 2: Technical Service Offering (using Service Builder)
Technical service offerings can certainly be configured by navigating to the various forms and completing the information as needed. However, ServiceNow does provide a free ServiceNow Store application called Service Builder that can be downloaded. Service Builder can be used to create technical services and their corresponding offerings quickly and easily in a guided, step-by-step flow. Helpful hints and descriptions explain the critical fields and values, and their purposes.