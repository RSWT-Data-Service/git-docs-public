# RSWT Data Service Open Documentation

This documentation provides high level, public versions of the Data Service's documentation which includes detais on platforms, processes and security mechanisms used to create robust, accessible and secure data analytics.

## What we use

![High Level Design Diagram](https://github.com/RSWT-Data-Service/git-docs/blob/3b815488f4c63676100e86147fdd729c72df3332/Images/RSWT_DSP_highlevel.png)

Figure 1; High Level Design Diagram. 

### Azure Data Factory

Azure Data Factory is a cloud-based data integration service that enables users to create, schedule, and orchestrate data workflows. This service is particularly useful for enterprises looking to manage data transformation and movement at scale, allowing them to collect data from various sources, transform it in a scalable environment, and deliver processed data to data stores for business intelligence and analysis purposes. Azure Data Factory supports a wide range of data integration activities, facilitating the automation of data-driven workflows and integration with a broad spectrum of on-premises and cloud data sources.

### Azure Storage

[Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) Gen2 is a comprehensive solution for Big Data Analytics
Azure Data Lake Storage Gen2 is a powerful set of capabilities built on Azure Blob Storage, designed specifically for big data analytics. It combines the strengths of Azure Data Lake Storage Gen1 with Azure Blob Storage, offering a range of features such as file system semantics, file-level security, and scalability. Additionally, it provides low-cost, tiered storage with high availability and disaster recovery capabilities.

 ### Databricks 
  
The Databricks Lakehouse is a unified data management architecture that combines the flexibility and scale of data lakes with the performance and reliability of data warehouses.
Databricks Workspaces provide an user friendly environment for data engineering, data science, and analytics, providing a collaborative space to manage notebooks, 
data pipelines, and machine learning experiments. 
Databricks uses a [medallion architecture](https://www.databricks.com/glossary/medallion-architecture). 
This is a data design pattern used to logically organise data in a lakehouse, with the goal of incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables). 


![Medallion Architecture](https://www.databricks.com/sites/default/files/inline-images/building-data-pipelines-with-delta-lake-120823.png)

Figure 1; Medallion Architecture.


:3rd_place_medal: **Bronze layer (raw data)**
The Bronze layer is where raw data is landed from source systems. Data may undergo minimal processing prior to landing in the bronze layer, for example, stripping out unnecessary personal data before data is saved.

:2nd_place_medal: **Silver layer (cleansed and conformed data)**
In the Silver layer, the data from the Bronze layer is cleaned, matched, merged, and conformed to the required data model or standards e.g. naming conventions etc. This provides a better view of the data and can help understand steps to achieve a unified data model. Data from different sources may be joined at this level, or kept independent but set to a shared model, for future unification. 

:1st_place_medal: **Gold layer (analysis ready data)**
Data in the Gold layer of the lakehouse is typically organized in analysis-ready tables and is used for reporting.  The final layer of data transformations and data quality rules are applied here. 

### ESRI Arc GIS Online 

Esri’s ArcGIS Online (AGOL) is a cloud-based geospatial platform that enables organizations to collect, manage, analyze, and share spatial data through web services and applications. Te Widlfie Trusts use AGOL as our primary GIS tool for webmapping, collaboration and data collection, alongside QGIS which is an open source desktop GIS. Within the AGOL ecosystem, Survey123 serves as one of the primary data ingestion tools for the Data Service, allowing users to design smart, form-centric surveys for capturing structured field data—often including location, photos, and geospatial attributes—in real time or offline. Data collected via Survey123 is directly published to hosted feature layers in AGOL and streamed into the Data Service making it immediately accessible for analysis and integration. Using the [ArcGIS API](https://developers.arcgis.com/rest/) and [AGOLxDatabricks Python linrary](https://www.esri.com/arcgis-blog/products/api-python/announcements/new-use-the-arcgis-api-for-python-in-databricks-notebooks), these datasets can be programmatically managed, accessed, and processed—supporting automated workflows for data validation, transformation, and synchronization with downstream data products, thereby streamlining the end-to-end data pipeline.

### Power BI

The Data Service use Power BI as one of the primary tools for producing data reports, visualisations and dashboards. BI products are produced for internal (RSWT) and external (federation and wider partners/public) audiences. Power BI Embedded Capacity is a dedicated set of compute resources (CPU, RAM, storage) used to host and deliver Power BI content. It acts as a private, high-performance, and scalable server, enabling fast report performance, large dataset storage, and widespread report distribution to free users enabling them to view content published by Pro/PPU users in workspaces assigned the Capacity. This is particularly important for The Wildlife Trusts as this enables us to share outputs with users from the different Trusts regardless of whether these Trusts have Power BI licences.


---

## How we keep things safe

:white_check_mark: **Microsoft Defender for Cloud**
Microsoft Defender for Cloud is deployed to protect cloud-based applications from various cyber threats and vulnerabilities. 

:white_check_mark: **Microsoft Sentinel**
RSWT’s CSOC partners deploy Sentinel on our behalf and monitor security threats and reports. 

:white_check_mark: **Infrastructure encryption on all stored data**
Azure Storage Service Encryption (SSE) for data at rest is enabled by default and uses 256-bit AES encryption.

:white_check_mark: **TLSv1.2**
Safe transfer of data between systems is protected using a minimum of TLS 1.2 for all HTTPS connections.  

:white_check_mark: **HTTPS encryption**
All data in transit uses HTTPS to ensure secure communication. 

:white_check_mark: **Microsoft ENTRA ID**
Access is integratedwith RSWT's wider Microsoft Entra ID system.

:white_check_mark: **Multifactor Authentication**
MFA is enabled for all users and roles on Databricks, Azure and GitHub. 

:white_check_mark: **Conditional Access Policies**
RSWT deploys a range of Conditional Access Policies to enforce security requirements when accessing resources. 

:white_check_mark: **Resource Locks**
RSWT ensures that specific resources remain protected by Resource Locks, maintaining their integrity and availability.

:white_check_mark: **Audit Logs**
Wthin Databricks, RSWT has deployed a range of audits to log user activity and record specific changes or access to specific resources. 


## How we manage who can see what and what they can do 

:white_check_mark: **Role Based Access Control**
Users are assigned to security groups based around functional job roles to manage access to sensitive data and administrative processes within the data service assets.

:white_check_mark: **Role Based Access Control**
RSWT follows the Principle of Least Privilege meaning that staff are only assigned the lowest role required to complete their task, rather than roles which are higher privilege which may include entitlements beyond the scope of the staff members job. This may mean that staff are assigned multiple roles or entitlements rather than a single higher privilege one, as staff are expected to only activate specific roles to carry out specific tasks. 

:white_check_mark: **Privileged Identity Management**
RSWT follows the Just-in-Time principle, eliminating 'always on' roles and therefore reducing vulnerability to attack. Where possible, staff are required to activate their roles, providing an audit trail and authorisation for activation where necessary.

## How we make sure what we do is good quality 

The Data Service team adopts a range of methods to help ensure that the data analytics we produce are of a high quality. This includes data validation, code reviews, meta data standards, standardisation and data dictionaries.

### Data Validation
Data validation is the process of checking data against predefined rules to ensure its accuracy, consistency, and quality. This may vary for each use case and for every variable however in general this will include carrying out checks for these common issues; 

:x:	null values 

:x:	outliers

:x:	duplicate variables or values

:x:	values out of any applied constraints

:x:	whether primary and foreign keys have been identified.


### Standardisation
Standardisation aids clarity, reduces inconsistency and enables all of the team and others to be clear on data lineage, appropriate use and helps create ‘single sources of truth’. 
Tools used to standardise our work include;

:x: naming conventions

:x: data dictionaries

:x: utilising packages & functions

:x: utilising shared datasets, not data in silos.


### Shared repositories & Peer Reviews
Code repositories are key to ensuring that code is stored appropriately, not lost when individual members of staff leave, and is available for peer review. Code held in silos or in different systems risks these being lost, inappropriate analytic being carried out, or different methods of analysis in different systems producing inconsistent results.

The Data Service team peer reviews each others work and suggest improvements and changes. Broadly, reviewers are looking at two areas; errors (any mistakes in code, typos or incorrectly calculated variables) and standards (has the original analysts followed our internal data standards and industry best practice). 
