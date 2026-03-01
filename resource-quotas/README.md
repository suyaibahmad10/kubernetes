## Reosurce and quotas

1. check resourcequotas
```
(venv) suyaibahmad@Suyaibs-MacBook-Air resource-quotas % kc get resourcequota -A 
NAMESPACE   NAME         AGE   REQUEST                                     LIMIT
dev         dev-quota    29s   requests.cpu: 0/1, requests.memory: 0/1Gi   limits.cpu: 0/2, limits.memory: 0/2Gi
prod        prod-quota   29s   requests.cpu: 0/2, requests.memory: 0/2Gi   limits.cpu: 0/4, limits.memory: 0/4Gi
```

2. describe resourcequota:
```
(venv) suyaibahmad@Suyaibs-MacBook-Air resource-quotas % kc describe resourcequota dev-quota -n dev
Name:            dev-quota
Namespace:       dev
Resource         Used  Hard
--------         ----  ----
limits.cpu       0     2
limits.memory    0     2Gi
requests.cpu     0     1
requests.memory  0     1Gi
```

## Issue when we create deployment with limited resources.
Since deployment create pod will rollingupdate when image is changed so it may be possible that replicas are less since resource quotas may be exhausted.
Error will be in replicaset level all the quota error and not on deployment.
