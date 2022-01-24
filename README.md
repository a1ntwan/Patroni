This is an interesting implementation of Patroni cluster I've made as a final task for my Postgres course. The task did not require automatization, but I decided make it in a more complicated way using Ansible and different Linux distributions.

***
The main task was to build a Patroni cluster using **3 etcd nodes** and **4 Patroni nodes**: **1 master node**, **1 synchronous replica**, **1 asynchronous replica** and a **reserve node** that should be included in cluster only when primary master is not being active for 3 min after failover.
It was also necessary to create **2 nodes for pgbouncer** - I've used **confd** to check the availability and the status of the nodes in the cluster. 
Master is node in Patroni cluster is **rw** and replicas are just **ro**. Load Balancer should be in front of the cluster, so I've chosen **HAproxy with keepalived** to keep it HA on 2 nodes. 
Last but not least - **Prometheus server**, **node_exporter** on every node of the cluster and **postgres_exporter** just for db nodes.
***

These playbooks have been tested on **Centos7**, **Ubuntu 20.04** and **Rocky Linux8**.
