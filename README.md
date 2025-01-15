# Application Migration With AWS
Migrating On-prem Workload to AWS Cloud

### Introduction:
Migrating the On-prem Workload to Cloud is one of the key aspects. This Project demonstrates migrating the  Web server and database server from the On-prem to the AWS Cloud using Rehosting and Replatforming Approach. Web Application is running in on-prem server which is connected to persistent layer [DB layer] which is deployed in other server. Here, we are migrating the application from web server to the EC2 running inside VPC in multiple availability zone for the Secure, High Availability, scalability, fault tolerant and Replatforming the MYSQL DB and its schema content from On-prem server to the AWS Purpose build database layer called RDS Mysql which is deployed in multiple AZ with Master and Standby DBs.

--------------------------------------------------------
### Architecture:
![Migration_final_GIF](https://github.com/user-attachments/assets/14150d77-2a16-4e05-bd95-a55fb5db8324)



--------------------------------------------------------
## Key Components of the Migration:
**Source Component:**
Simulated the on prem environment with the web application running in web server and Database running in other server in different VPC.Both were deliberately architected in a non-optimal setup to showcase the modernization that AWS enables (check the architecture diagram).

**Target Component:**
Migrated the application to a highly available, well-architected VPC in AWS, spanning two Availability Zones with redundancy and fault tolerance.

--------------------------------------------------------
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

--------------------------------------------------------
## Steps Taken:
1. Installed the AWS Discovery Agents in Source Environment Web server and database. It collects static configuration data, detailed time-series system-performance information, inbound and outbound network connections, and processes that are running and send to the Application Discovery Service which can be consolated and view from Migration Hub.

<img width="648" alt="agent status" src="https://github.com/user-attachments/assets/63385f9b-49a8-4ffe-bbf1-b76254d735e4" />


<img width="920" alt="Migration Hub Network" src="https://github.com/user-attachments/assets/b8622ac3-61c5-41ca-b2da-e5f87a91a7b8" />


2. Replatformed the Database from the On-prem to Managed RDS Instance in Multi-AZ setup using DMS. DMS migrate the table schema and records from source to target in one shot and replicate the live data updates happens at the source environment so that both the environment will be insync.We have created the DMS Replication instance in the public subnet and data from the on-prem synchronize to this instance. Finally, Data will be moved to the RDS MYSQL form the DMS instances.

<img width="893" alt="DMS Migration task" src="https://github.com/user-attachments/assets/a2cf9293-23c1-4638-a0f9-c7346a9560db" />


<img width="951" alt="dms task-table" src="https://github.com/user-attachments/assets/6c1ea029-263e-414d-a1af-0f1af8f87e8a" />


<img width="952" alt="endpoint-dms" src="https://github.com/user-attachments/assets/63e07fa0-69a2-4dad-b630-3aff2fbe9fef" />


3. Rehosted the web server using MGN, ensuring seamless block-level replication and minimal impact on the application. MGN simulates the same structure in on-prem to AWS Cloud like If the HDD is attached to the application in On-prem, it also creates the EBS volumes and mount to the EC2 instances. 

<img width="822" alt="volumes at dest" src="https://github.com/user-attachments/assets/983208a7-34de-45fa-8176-45e913d9999f" />


![image](https://github.com/user-attachments/assets/f8016da1-dc4c-4943-958c-d2bad5aa0c33)


4. Customized the target environment by fine-tuning EC2 Launch Templates and configuring NAT Gateways for secure communication.

![image](https://github.com/user-attachments/assets/ee5474ba-d711-4e15-b6e8-38cd1cd7c013)


5. Launch the Test instances to check whether MGN rehosted the Application correctly. You can verify that our test instance is currently running, with the public IP mapped in the right subnet and VPC. You could also connect to the instance to verify that all files are there.

![image](https://github.com/user-attachments/assets/7c23255b-cc14-4f07-b363-6eaabc686aa8)


6. Finally, performed a cutover to the target environment, reconfiguring the application to use the migrated database on RDS.

<img width="942" alt="Cutover-complete" src="https://github.com/user-attachments/assets/e51ca33b-d10e-49d8-b965-1414e05d2400" />


<img width="895" alt="cutover complete" src="https://github.com/user-attachments/assets/4d45007f-6e36-433f-871b-a0fc0dc55b19" />

--------------------------------------------------------
## Migration Workflow Highlights:
**Rehost(Lift and Shift):** Application has been moved from source environment to the Destination Cloud using Application Migration Service (MGN)

**Replatform:** Moved the MYSQL Database from Server to the AWS Managed RDS MYSQL using Database Migration Service (DMS)

--------------------------------------------------------
## SUMMARY:
**1. Discover:**
1. Initialized and configured AWS Application Discovery service (ADS).
	* Set Migration Hub home Region.
	* Created IAM user and credentials.
2. Deployed ADS Agent to the source Webserver and DBServer.
3. Verified that the data collection is started and in healthy condition.
4. Reviewed the data and the different options in the Migration Hub:
  	* Server list.
  	* Network visualization.
  	* Application grouping.
5. Worked with Application groups and tags:
  	* Create application group.
  	* Add or remove servers from the application group.

**2. Re-platform- AWS Database Migration Service(DMS)**
1. Created a new managed database, using Amazon Relational Database Service (RDS)
2. Created an AWS Database Migration Service (DMS) Replication Instance - that allows you to replicate data between databases
3. Created the source and target DMS Endpoints
4. Modified the configuration of the source database to allow for continuous replication of data (binary log)
5. Started the replication of data through a DMS replication task

**3. Re-host-Application Migration Service**
1. Initialized and configured AWS Application Migration Service (MGN)
2. Deployed MGN Agent to the source application server
3. Customized the EC2 Launch Template to fine tune how the rehosted server would be configured in the target AWS environment
4. Launched test instance with MGN to validate the rehost process was functional
5. Launched the cutover instance, and reconfigured the application to the new target environment
6. Finalized the cutover process, and executed housekeeping on AWS Application Migration Service (MGN) inventory

--------------------------------------------------------
## Conclusion:
This Project teaches how to migrate the on-prem workloads such as application layer and database layer to the AWS cloud by providing High RTO and RPO. By leveraging MGN, DMS and other Services we are able to move the workload in ease.
