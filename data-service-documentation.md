# RSWT Data Service Open Documentation

This documentation provides high level, public versions of the Data Service's documentation which includes detais on platforms, processes and security mechanisms used to create robust, accessible and secure data analytics.

## What we use

 ### Databricks 
  
The Databricks Lakehouse is a unified data management architecture that combines the flexibility and scale of data lakes with the performance and reliability of data warehouses.
Databricks Workspaces provide an user fieiendly environment for data engineering, data science, and analytics, providing a collaborative space to manage notebooks, 
data pipelines, and machine learning experiments. 
Databricks uses a [medallion architecture](https://www.databricks.com/glossary/medallion-architecture). 
This is a data design pattern used to logically organise data in a lakehouse, with the goal of incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables). 


![Medallion Architecture](https://github.com/RSWT-Data-Service/git-docs/blob/e35587f701cc908b22cc64471a74e4ca62c05500/Images/medallion-architecture.png)

Figure 1; Medallion Architecture.

:3rd_place_medal: **Bronze layer (raw data)**
The Bronze layer is where raw data is landed from source systems. Data may undergo minimal processing prior to landing in the bronze layer, for example, stripping out unnecessary personal data before data is saved.

:2nd_place_medal: **Silver layer (cleansed and conformed data)**
In the Silver layer, the data from the Bronze layer is cleaned, matched, merged, and conformed to the required data model or standards e.g. naming conventions etc. This provides a better view of the data and can help understand steps to achieve a unified data model. Data from different sources may be joined at this level, or kept independent but set to a shared model, for future unification. 

:1st_place_medal: **Gold layer (analysis ready data)**
Data in the Gold layer of the lakehouse is typically organized in analysis-ready tables and is used for reporting.  The final layer of data transformations and data quality rules are applied here. 



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
