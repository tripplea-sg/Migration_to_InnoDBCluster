# Clustering and Data Protection with MySQL InnoDB Cluster and MEB
This hands-on-Lab material covers the following topics:
1. Migrating MariaDB to MySQL Enterprise Edition 
2. Setup InnoDB Cluster 
3. Backup/Recovery with MySQL Enterprise Backup (MEB)

## About MySQL Enterprise Edition
MySQL Enterprise Edition includes the most comprehensive set of advanced features, management tools and technical support to achieve the highest levels of MySQL scalability, security, reliability, and uptime. It reduces the risk, cost, and complexity in developing, deploying, and managing business-critical MySQL applications to meet compliance, business and technical requirements. Oracle own, maintain, and develop all tech stacks in the MySQL Enterprise Edition, where no 3rd party is used for features such as hgh availability, backup/recovery, security, etc. 

## About InnoDB Cluster
InnoDB Cluster is a shared nothing clustering solution for MySQL Enterprise Edition. InnoDB Cluster uses Group Replication as the high availability engine to manage and automate clustering function such as auto-failover, autojoin, auto-healing, etc. as well as manage replication consistency between group members with RPO=0 based on quorum (majority win) as paxos variant. InnoDB Cluster has a requirement of minimum 3 members and maximum 9 members where usually odd number of total members are suggested. In a single primary mode, only 1 node is R/W and called as PRIMARY member, and the rest are SECONDARY members running with R/O. </br></br>
InnoDB Cluster uses MySQL Router to provide connection transparency from application to InnoDB Cluster, making database connection to an InnoDB Cluster the same as connecting to a standalone server. R/W port of MySQL Router will point to PRIMARY member, and R/O port will point to one of SECONDARY member. In case many R/O connections, MySQL Router will load balance R/O connections to all SECONDARY node in round-robin fashon</br></br>
MySQL Shell is used as a tool to build, monitor, and maintain InnoDB Cluster. MySQL Shell uses Admin API, a collection of single commands that can automate and orchestrate InnoDB Cluster operationalization, such as: deploying, switchover, adding nodes, start cluster, handling failure, etc. </br></br>
MySQL InnoDB Cluster has automatic failover. A failure of PRIMARY member will automatically trigger a promotion of one of SECONDARY member to be a new PRIMARY. When this failure member is back, it will automatically join to the group, run incremental recovery until all backlog transactions are applied, and finally ONLINE as SECONDARY member. Application connection failover is transparent as it's managed by MySQL Router.  
