# Volumes

1. emptyDir:
    * Volumes exist at the **pod** level and are ephemeral
    * Created when a pod is scheduled onto a node and removed upon pod termination
    * All containers within the same pod share the same emptyDir and can read/write the same files
    * Containers may mount the volume at different paths if needed
    * Backed by node storage: can be memory (tmpfs) or disk depending on `medium` field
    * Useful for scratch space, caches, or passing data between containers in a pod
    * **Data is lost** when the pod is deleted, evicted, or rescheduled to another node
    (Note: Not suitable for long‑term persistence or data you can't afford to lose)

2. Local:
    * Persistent volumes that point to storage local to a specific node (e.g. a hostPath, SSD)
    * Data survives pod restarts but **not** node failure or deletion — the volume is lost if the node is removed
    * Only supports **static provisioning**; Kubernetes does not dynamically allocate local volumes
    * Requires explicit `nodeAffinity` in the `PersistentVolume` so scheduler places pod on the correct node
    * Pods access them through normal `PersistentVolumeClaim` bindings
    * Good for workloads needing high I/O or using node‑specific hardware, but portability is limited
    * Carefully manage locality and availability; typically not recommended for multi‑node production unless using local persistent storage operators
    (Note: unsuitable for general production unless part of a well‑designed local storage solution)

3. StatefulSets:
    * Designed for stateful applications requiring stable network identities and persistent storage
    * Pods are created in order and have stable, unique identities (e.g., pod-0, pod-1)
    * Each replica can get its own `PersistentVolumeClaim` via `volumeClaimTemplates`
    * PVCs remain after pod deletion, so data persists across restarts and rescheduling
    * Useful for databases and clustered systems where each instance needs its own storage and consistent hostname
    * Works with `Headless` Services to provide DNS for each pod instance
    * Scaling down deletes pods in reverse order but does not delete the associated PVCs by default
