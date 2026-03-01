## Commands

1.  kc get ns
2. kc get pods -n kube-system


### Set context for namepsaces

1. Check context
```
(venv) suyaibahmad@Suyaibs-MacBook-Air namespaces % kc config current-context
minikube
```

2. Set current context to a namespace and now default will be dev namepapce:
```
(venv) suyaibahmad@Suyaibs-MacBook-Air namespaces % kc config set-context --current --namespace=dev
Context "minikube" modified.
```

3. To see the config:
```
 kc config view
 ```

4. To get all pods from all namespaces:
```
kc get pod --all-namespaces
```
OR
```
kc get pod -A
```

5. If the service is required from other namespace then FQDN is required, example in traffic-generator.yml file
