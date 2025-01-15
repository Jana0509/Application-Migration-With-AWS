# Rehost-and-Re-platform-Using-AWS
Migration of Web Server and Database Server to AWS Cloud

## Introduction:
Migrating the On-prem Workload to Cloud is one of the key aspects. This Project demonstrates migrating the  Web server and database server from the On-prem to the AWS Cloud using Rehosting and Replatforming Approach. Web Application is running in on-prem server which is connected to persistent layer [DB layer] which is deployed in other server. Here, we are migrating the application from web server to the EC2 running inside VPC in multiple availability zone for the Secure, High Availability, scalability, fault tolerant and Replatforming the MYSQL DB and its schema content from On-prem server to the AWS Purpose build database layer called RDS Mysql which is deployed in multiple AZ with Master and Standby DBs.

## Architecture:



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
