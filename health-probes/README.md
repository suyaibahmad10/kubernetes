# Probes
Probes are health checks performed by the Kubelet to monitor the status of containers within a pod.

# Types of probes:

1. Startup probes: 
    * Ensures that a container has started successfully. If the startup probe failes, k8s will kill the container and restart it

2. Liveness probe: 
    * Keeps executing throughout the container lifecycle
    * If liveness probe fails, k8s will restart the container.

3. Readiness probe:
    * Keeps executing throughout the container lifecycle
    * Checks if container is ready to accept traffic.
    * If readiness probe fails, k8s will remove the container from list of endpoints which accepts traffic.
