# Before you begin 

The requirements are applicable only for deploying Enterprise Edition of ownCloud Server 10.0.10 for large enterprises and service providers with 5,000 to >100,000 users and storage up to 1 petabyte.


**To properly install ownCloud Enterprise Edition using the Linux package manager, it is important to meet the basic ownCloud-specific requirements:**

## Software requirements

* RHEL 7 with latest service packs.
* MySQL/MariaDB Galera Cluster with 4x master-master replication.
* A cluster of 2 or more database servers. Each database server must have 4 sockets and 128GB RAM.
* Apache Web server version 2.4. Around 4 to 20 web servers with 4 sockets and 64GB RAM.  
* PHP version 5.6+. Ensure to install and configure certain PHP extensions. For more details, see the [PHP Extensions](https://doc.owncloud.org/server/10.0/admin_manual/installation/source_installation.html#php-extensions). 
* An NFS server or an object store that is S3 compatible.
* Cloud federation for a distributed setup over several data centers.
* A standard SSL certificate. 
* Redis for session management storage and distributed in-memory caching. 
* Authentication via an existing LDAP, Active Directory server, or SAML.

## Hardware requirements

* 2 Hardware load balancers such as BIG IP from F5.
* A redundant hardware load-balancer with heartbeat such as F5 Big-IP. This runs two load balancers in front of the application servers.

## Permission requirements

In order to install and configure ownCloud, the Administrator must have access to command-line and crontab.

For more information related to the requirements for other deployment scenarios, see the [Deployment Recommendations](https://doc.owncloud.org/server/10.0/admin_manual/installation/deployment_recommendations.html#scenario-3-large-enterprises-and-service-providers).
