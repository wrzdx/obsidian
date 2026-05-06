Most apps today store data on managed cloud services rather than on one local machine

## Why Databases Moved to the Cloud?
Traditional databases often ran on a single server inside one organization.

Modern apps need:
- Internet-scale access
- 24/7 uptime
- Users in many regions

Cloud providers offer elastic compute, managed storage, backups, and global networking.
>[!summary] Result
>Teams spend less time maintaining hardware and more time building features.


## Cloud Databases
cloud database stores and manages data using infrastructure provided through the cloud. The provider may handle deployment, patching, backups, failover, and scaling.

- **Patching** = process of updating software to fix problems or improve it
- **Failover** = automatic switching from a failed system to a backup system.

Cloud databases can be both SQL and NoSQL database

- **Managed** – Provider runs most operations
- **Elastic** – Resources can grow or shrink
- **Networked** – Accessed over the internet / VPC
- **Durable** – Copies, backups, and recovery

In one service we get:
- Database software 
- Storage 
- Automation 
- Global infrastructure

## Database-as-a-Service (DBaaS)
DBaaS is a cloud service model where the provider delivers a fully managed database platform, while users access and use the database without managing the underlying infrastructure.

>[!note] 
>Instead of installing and maintaining a database server manually, organizations rent a ready-to-use database service in the cloud.

- **Provider** handles: server provisioning, software installation, patching and updates, backups and recovery, monitoring, scaling, high availability and failover
- **User** manages: database schema and tables, queries and application logic, access permissions, data quality and performance tuning at the application level


**Benefits of DBaaS:**
- Fast setup – DBaaS can be deployed in minutes because the provider prepares the infrastructure and database software.