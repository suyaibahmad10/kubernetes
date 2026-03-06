# Headless Service

This directory contains an example and documentation for a **headless service** in Kubernetes.

A headless service is a `Service` resource that does **not** receive a cluster‑wide
IP address. When `spec.clusterIP` is set to `None`, Kubernetes returns the
individual pod IPs directly instead of proxying traffic through a VIP. This
behaviour is useful for:

* Stateful workloads (databases, caches) that need to address each replica
directly.
* DNS‑based service discovery where clients implement their own load balancing
  or connection logic.
* Exposing `Endpoints` objects or external backends without a cluster IP.

## How It Works

With `clusterIP: None`, the Kubernetes DNS server generates A records for each
pod that matches the service's selector. Queries to
`<service>.<namespace>.svc.cluster.local` return a list of pod addresses.

A headless service still uses a selector to keep the endpoints list up to date,
and StatefulSets can use a headless service via the `serviceName` field to
provide stable network identities for pods.

## Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: headless-example
  labels:
    app: myapp
spec:
  clusterIP: None          # <== makes the service headless
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
```

Deploy pods (e.g. with a Deployment or StatefulSet) labeled `app: myapp`. DNS
lookups will show the individual pod IPs:

```bash
kubectl exec -it busybox -- nslookup headless-example
```

You should see multiple `Address` entries instead of a single cluster IP.

## Usage Notes

* Headless services have no virtual IP; clients must resolve DNS and connect to
the pods directly.
* In StatefulSets, a headless service specified via `serviceName` gives each
  pod a stable DNS name like
  `pod-0.headless-example.default.svc.cluster.local`.
* You can manually create an `Endpoints` resource with the same name as the
  service to point to external addresses or manage targets explicitly.


## CMD output:
```bash
suyaibahmad@Suyaibs-MacBook-Air headless-service % kc get pod
NAME         READY   STATUS    RESTARTS   AGE
color-ss-0   1/1     Running   0          8m21s
color-ss-1   1/1     Running   0          8m20s
color-ss-2   1/1     Running   0          8m19s
curl         1/1     Running   0          8m21s

suyaibahmad@Suyaibs-MacBook-Air headless-service % kc get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
color-svc    ClusterIP   None         <none>        80/TCP    8m30s
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   34d

suyaibahmad@Suyaibs-MacBook-Air headless-service % kc describe svc color-svc
Name:              color-svc
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=color-api
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                None
IPs:               None
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         10.244.0.217:80,10.244.0.219:80,10.244.0.220:80 # => You can see Endpoints
Session Affinity:  None
Events:            <none>
suyaibahmad@Suyaibs-MacBook-Air headless-service % 


suyaibahmad@Suyaibs-MacBook-Air headless-service % kc exec -it curl -- sh 
/ # curl color-ss-0.color-svc
<h1 style="color:blue;">Hello from color-api!</h1>

/ # curl color-ss-0.color-svc/api
COLOR : blue, HOSTNAME : color-ss-0/ 

```