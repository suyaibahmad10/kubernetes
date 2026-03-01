## Labels & selectors

1. Filter labels with cli:
```
suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pods -L app -L tier
NAME             READY   STATUS    RESTARTS   AGE   APP         TIER
color-backend    1/1     Running   0          66s   color-api   backend
color-frontend   1/1     Running   0          66s   color-api   frontend
```

2. Get the label filter outputs:
```
suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pod -l tier=frontend
NAME             READY   STATUS    RESTARTS   AGE
color-frontend   1/1     Running   0          2m36s
```

3. Few more:
```
suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pod -l tier=frontend -l app=color-api
NAME             READY   STATUS    RESTARTS   AGE
color-backend    1/1     Running   0          4m31s
color-frontend   1/1     Running   0          4m31s

suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pod -l 'tier=frontend,app=color-api' 
NAME             READY   STATUS    RESTARTS   AGE
color-frontend   1/1     Running   0          5m

suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pod -l 'tier in (frontend)'         
NAME             READY   STATUS    RESTARTS   AGE
color-frontend   1/1     Running   0          5m36s

suyaibahmad@Suyaibs-MacBook-Air labels_and_selectors % kc get pod -l 'tier notin (frontend)'
NAME            READY   STATUS    RESTARTS   AGE
color-backend   1/1     Running   0          5m45s

