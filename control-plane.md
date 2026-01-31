# Control plane

1. Api server: 
    * Main entry point
    * Takes the kubectl or dashboard instructions
    * get pod, create pods or update pods any operation will communicate with api server

2. Scheduler:
    * placing pods to suitable nodes
    * picks based on resource availability and other constaints
    * can custom define to scheduler

3.  controller managers:
    * responsible for controller processes that handles routine tasks
    * e.g: node controller scheduler takes care nodes are healthy, registered with k8s and are healthy
    * e.g replicaSet controller takes care of replicasets in node and make sure correct number of replica sets are present

4. Etcd:
    * distributed key-value store that stores all the cluster data
    * stores both configuration and state of cluster
    * act as single source of trust
    * api server read and write data

5. cloud controller manager:
    * interacts with cloud infrastructure
    * manages cloud based LB, persistsent storage and node management