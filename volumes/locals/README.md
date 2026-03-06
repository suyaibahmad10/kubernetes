# Local

Local support statically provisioned persistent volume only

1. Statically provisioed PV: 
```
suyaibahmad@Suyaibs-MacBook-Air locals % kc get pv
NAME           CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS    VOLUMEATTRIBUTESCLASS   REASON   AGE
local-volume   1Gi        RWO            Retain           Bound    default/local-volume-claim   local-storage   <unset>                          10s
```

```
suyaibahmad@Suyaibs-MacBook-Air locals % kc get pvc
NAME                 STATUS   VOLUME         CAPACITY   ACCESS MODES   STORAGECLASS    VOLUMEATTRIBUTESCLASS   AGE
local-volume-claim   Bound    local-volume   1Gi        RWO            local-storage   <unset>                 21s
suyaibahmad@Suyaibs-MacBook-Air locals %
```

