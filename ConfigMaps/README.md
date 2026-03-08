# ConfigMaps in Kubernetes

ConfigMaps allow you to decouple configuration artifacts from image content to keep containerized applications portable.

## Creating a ConfigMap

You can create a ConfigMap from literal values:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: value1
  key2: value2
```

Or from files:

```bash
kubectl create configmap my-config --from-file=config.txt
```

## Using ConfigMaps in Pods

You can mount ConfigMaps as volumes or use them as environment variables.

As environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
    env:
    - name: KEY1
      valueFrom:
        configMapKeyRef:
          name: my-config
          key: key1
```

As a volume:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: my-config
```


# Notes:

* Must not exceed 1 MB data
* Can set configMap as immutable, means cannot be modified but recreated.


## Commands Used:
```bash
suyaibahmad@Suyaibs-MacBook-Air ConfigMaps % kc get pod
NAME            READY   STATUS    RESTARTS   AGE
red-color-api   1/1     Running   0          5m3s

suyaibahmad@Suyaibs-MacBook-Air ConfigMaps % kc get configmap
NAME               DATA   AGE
kube-root-ca.crt   1      34d
red-config         1      14m

suyaibahmad@Suyaibs-MacBook-Air ConfigMaps % kc expose pod red-color-api
service/red-color-api exposed

suyaibahmad@Suyaibs-MacBook-Air ConfigMaps % kc get svc
NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes      ClusterIP   10.96.0.1      <none>        443/TCP   34d
red-color-api   ClusterIP   10.99.213.32   <none>        80/TCP    4s

suyaibahmad@Suyaibs-MacBook-Air ConfigMaps % minikube service red-color-api
|-----------|---------------|-------------|--------------|
| NAMESPACE |     NAME      | TARGET PORT |     URL      |
|-----------|---------------|-------------|--------------|
| default   | red-color-api |             | No node port |
|-----------|---------------|-------------|--------------|
😿  service default/red-color-api has no node port
❗  Services [default/red-color-api] have type "ClusterIP" not meant to be exposed, however for local development minikube allows you to access this !
🏃  Starting tunnel for service red-color-api.
|-----------|---------------|-------------|------------------------|
| NAMESPACE |     NAME      | TARGET PORT |          URL           |
|-----------|---------------|-------------|------------------------|
| default   | red-color-api |             | http://127.0.0.1:60809 |
|-----------|---------------|-------------|------------------------|
🎉  Opening service default/red-color-api in default browser...
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

```

