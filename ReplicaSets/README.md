# Limitation of ReplicaSet

## Scenario (when we change a image in replica-set manifest file)
* Replicaset changed the image when we do `kubectl describe rs <rs-name>`
* However Replicaset do not automatically does not change image at Pods, since it only check for numbers of replicas
* When manually pod is deleted then only new pod will have updated image

NOTE: So rolling out updates with pure and only RS is a manual process.