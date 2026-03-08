# Secrets in Kubernetes

Secrets are objects that contain a small amount of sensitive data such as passwords, tokens, or keys. They help keep sensitive information separate from the application code.

## Types of Secrets

- **Opaque**: Default type, arbitrary user-defined data (base64-encoded)
- **kubernetes.io/service-account-token**: Service account token
- **kubernetes.io/dockercfg**: Serialized Docker config
- **kubernetes.io/dockercfg-json**: Docker registry credentials
- **kubernetes.io/basic-auth**: Credentials for basic authentication
- **kubernetes.io/ssh-auth**: SSH authentication data
- **kubernetes.io/tls**: TLS certificate and key pair
- **bootstrap.kubernetes.io/token**: Bootstrap token

## Creating a Secret

From literal values:

```bash
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=secret
```

From a file:

```bash
kubectl create secret generic my-secret --from-file=secret.txt
```

Using YAML:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=      # base64-encoded "admin"
  password: c2VjcmV0=     # base64-encoded "secret"
```

## Using Secrets in Pods

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
    - name: USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: username
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
    - name: secret-volume
      mountPath: /etc/secrets
  volumes:
  - name: secret-volume
    secret:
      secretName: my-secret
```

## Important Notes

- Secrets are base64-encoded by default, not encrypted
- For production, consider using encrypted storage or external secret management solutions
- Maximum size of a Secret is 1MB
- etcd stores secrets unencrypted by default; consider enabling encryption at rest
