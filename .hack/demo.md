# Notes for Kubecon

# Backend
Appsodify the app
```
appsody init incubator/nodejs-express none
appsody deploy --generate-only
```
Run App
```
appsody run -p 3001:3000 -p 9230:9229
```

Deploy App direct
```
appsody deploy -t csantanapr/appsody-backend -n kabanero --push
```

# Frontend
Appsodify the app
```
appsody init incubator/nodejs-express none
appsody deploy --generate-only
```
Run App
```
appsody run
```

Get App ready for git deploy, update `app-deploy.yaml`
```yaml
spec:
  env:
    - name: APPSODY_BACKEND_DEFAULT_URL
      value: http://appsody-backend:3000/
```


Deploy direct
```
appsody deploy -t csantanapr/appsody-frontend --push -n kabanero
```





# Misc
appsody run --docker-options "--env-file .env"

# Service Binding Examples
https://github.com/seabaylea/appsody-frontend/blob/master/app-deploy.yaml#L34
https://github.com/seabaylea/appsody-backend/blob/master/app-deploy.yaml#L35

# DEBUG
Test the service bind
```
POD=$(kubectl get pod --selector app.kubernetes.io/name=appsody-frontend -o jsonpath="{.items[0].metadata.name}")
kubectl exec $POD -- curl -s -I -X POST http://appsody-backend:3000/signup
```
Port Forward
```
kubectl port-forward service/appsody-frontend 3000:3000
```

# Appsody Operator
https://github.com/appsody/appsody-operator/blob/service-binding/deploy/crds/appsody_v1beta1_appsodyapplication_crd.yaml

# Application Navigator
Edit `.appsody-config.yaml`
```
application-name: solution-startup
```
