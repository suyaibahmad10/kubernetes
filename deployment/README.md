# history of commands used 
``` 
 kc rollout undo deployment nginx-deployment
 kubectl rollout history deployment/nginx-deployment
 kubectl rollout history deployment/nginx-deployment --version=2
 kubectl rollout history deployment/nginx-deployment --revision=2
 kubectl rollout history deployment/nginx-deployment --revision=3
 kc rollout history deployment nginx-deployment

 # manually annotate
 kc annotate deployment nginx-deployment "kubernetes.io/change-cause"="update nginx tag to nginx:1.27.2"
```