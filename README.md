# Clustering and Data Protection with MySQL InnoDB Cluster and MEB
This hands-on-Lab material covers the following topics:
1. Migrating MariaDB to MySQL Enterprise Edition 
2. Setup InnoDB Cluster 
3. Backup/Recovery with MySQL Enterprise Backup (MEB)

## About MySQL Enterprise Edition
MySQL Enterprise Edition includes the most comprehensive set of advanced features, management tools and technical support to achieve the highest levels of MySQL scalability, security, reliability, and uptime. It reduces the risk, cost, and complexity in developing, deploying, and managing business-critical MySQL applications to meet compliance, business and technical requirements. Oracle own, maintain, and develop all tech stacks in the MySQL Enterprise Edition, where no 3rd party is used for features such as hgh availability, backup/recovery, security, etc. 

## About InnoDB Cluster
InnoDB Cluster is a shared nothing clustering solution for MySQL Enterprise Edition. InnoDB Cluster uses Group Replication as the high availability engine to manage and automate clustering function such as auto-failover, autojoin, auto-healing, etc. as well as manage replication consistency between group members with RPO=0 based on quorum (majority win) as paxos variant. InnoDB Cluster has a requirement of minimum 3 members and maximum 9 members where usually odd number of total members are suggested. InnoDB Cluster uses MySQL Router to provide connection transparency from application to InnoDB Cluster, making database connection to an InnoFB Cluster the same as connecting to a standalone server. </br></br>
MySQL Shell is used as a tool to build, monitor, and maintain InnoDB Cluster. MySQL Shell uses Admin API, a collection of single commands that can automate and orchestrate InnoDB Cluster operationalization, such as: deploying, switchover, adding nodes, start cluster, handling failure, etc.
