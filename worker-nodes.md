# worker node

1. kubelet:
    * an agent running on each worker node and communicates with control plane via API server
    * Ensures containers are running in pods defined by pod specification

2. container runtime (CRT):
    * responsible for running container on each worker node
    * support many CRT such as docker, containerd, CRI-O

3. kube-proxy:
    * responsibe for managing network rules on each worker node
    * maintainer network connectivity
    * lb for services
    * ensure requests are routed to appropriate pods

4. other k8s obejcts:
    * replicaSet
    * deployments
    * jobs
    * services
    * statefulSets