# Services

1. ClusterIP:
* Default kubernetes service type
* Designed for internal communication within a cluster
* It assigns a stable, internal IP address to a group of Pods (typically a Deployment), allowing other components within the same cluster to access them without worrying about the underlying pods' ephemeral nature. 
* (What we did), we created a deployment and clusterIP and used for internal communication


2. NodePort:
* Provides the functionality of clusterIP along with,
* Expose an application running inside a cluster to the external world
* In environments where a cloud LoadBalancer (like in AWS, GCP, or Azure) is not available, NodePort is the standard way to expose applications.
* When a NodePort service is created, Kubernetes opens a specific port on every node (Virtual Machine) in the cluster.
* The port assigned is in the range 30000-32767.
* (What we did), since we are in minikube setup, we have to use `minikube service color-api-nodeport   --url` which will provide us the url.
