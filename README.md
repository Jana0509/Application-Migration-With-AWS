# Application Migration With AWS
Migrating On-prem Workload to AWS Cloud

## Introduction:
Migrating the On-prem Workload to Cloud is one of the key aspects. This Project demonstrates migrating the  Web server and database server from the On-prem to the AWS Cloud using Rehosting and Replatforming Approach. Web Application is running in on-prem server which is connected to persistent layer [DB layer] which is deployed in other server. Here, we are migrating the application from web server to the EC2 running inside VPC in multiple availability zone for the Secure, High Availability, scalability, fault tolerant and Replatforming the MYSQL DB and its schema content from On-prem server to the AWS Purpose build database layer called RDS Mysql which is deployed in multiple AZ with Master and Standby DBs.

## Architecture:
![Image-Migrate](https://github.com/user-attachments/assets/1397069f-1de2-46f2-a5d3-51252666c1dd)



## Key Components of the Migration:
**Source Component:**
Simulated the on prem environment with the web application running in web server and Database running in other server in different VPC.Both were deliberately architected in a non-optimal setup to showcase the modernization that AWS enables (check the architecture diagram).
**Target Component:**
Migrated the application to a highly available, well-architected VPC in AWS, spanning two Availability Zones with redundancy and fault tolerance.

## AWS Services Involved:
**Application Discovery Service (AWS ADS):**
It helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers and databases. Application Discovery Service offers two ways of performing discovery and collecting data about your on-premises servers:

1. Agentless Discovery Service : can be performed by deploying the Application Discovery Service Agentless Collector (Agentless Collector) (OVA file) through your VMware vCenter.
2. Agent based Discovery: We are using this approach by installing the agent in the web server and database server, and this agent sends the updates about the usage, configuring data, network in and out, etc.

**Migration Hub :** 
It is the Console where we can visually see the Server usage, network topology for the server and simplifies your migration tracking as it aggregates your migration status information into a single console. You can view the discovered servers, group them into applications, and then track the migration status of each application from the Migration Hub console in your home Region.

**Application Migration Service(MGN):**
This is the key service which helps in migrating the application from Source Infra(on-prem) to the AWS Cloud and it helps in modernize your applications during migration with options such as disaster recovery and operating system or license conversion.


**Database Migration Service(DMS):**
It is a managed migration and replication service that helps move your database and analytics workloads to AWS quickly, securely, and with minimal downtime and zero data loss. AWS DMS supports migration between 20-plus database and analytics engines, covering homogeneous (ex. MySQL to MySQL) or heterogeneous (Oracle to PostgreSQL) use cases, and single or continuous replication mode. Here, In this Project, we are replatforming the homogeneous data from on-prem to AWS CLOUD.

## Steps Taken:
1. Installed the AWS Discovery Agents in Source Environment Web server and database. It collects static configuration data, detailed time-series system-performance information, inbound and outbound network connections, and processes that are running and send to the Application Discovery Service which can be consolated and view from Migration Hub.

2. Replatformed the Database from the On-prem to Managed RDS Instance in Multi-AZ setup using DMS. DMS migrate the table schema and records from source to target in one shot and replicate the live data updates happens at the source environment so that both the environment will be insync.We have created the DMS Replication instance in the public subnet and data from the on-prem synchronize to this instance. Finally, Data will be moved to the RDS MYSQL form the DMS instances.

3. Rehosted the web server using MGN, ensuring seamless block-level replication and minimal impact on the application. MGN simulates the same structure in on-prem to AWS Cloud like If the HDD is attached to the application in On-prem, it also creates the EBS volumes and mount to the EC2 instances. 

4. Customized the target environment by fine-tuning EC2 Launch Templates and configuring NAT Gateways for secure communication.

5. Launch the Test instances to check whether MGN rehosted the Application correctly. You can verify that our test instance is currently running, with the public IP mapped in the right subnet and VPC. You could also connect to the instance to verify that all files are there.

6. Finally, performed a cutover to the target environment, reconfiguring the application to use the migrated database on RDS.

## Migration Workflow Highlights:
Rehost (Lift and Shift) : Application has been moved from source environment to the Destination Cloud using Application Migration Service (MGN)

Replatform : Moved the MYSQL Database from Server to the AWS Managed RDS MYSQL using Database Migration Service (DMS)

## Conclusion:
This Project tells how to migrate the on-prem workloads such as application layer and database layer to the AWS cloud by providing High RTO and RPO. By leveraging MGN, DMS and other Services we are able to move the workload in ease.
