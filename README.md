
# Buildpacks Tekton Task for OpenShift
Runs without `privileged : true`  
Runs as `nonroot`


Based on:
https://github.com/tektoncd/catalog/tree/main/task/buildpacks/0.3/



## Install

```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.4/git-clone.yaml
```

```bash
REGISTRY_SERVER=https://index.docker.io/v1/ REGISTRY_USER=XXXXX REGISTRY_PASSWORD=XXXX

kubectl create secret docker-registry push-secret \
    --docker-server=$REGISTRY_SERVER \
    --docker-username=$REGISTRY_USER \
    --docker-password=$REGISTRY_PASSWORD


kubectl apply -f resources.yaml -f sa.yaml -f pipeline.yaml
```

## Run
```bash
kubectl create -f run.yaml
```


## Delete resources
```bash
kubectl delete -f resources.yaml -f sa.yaml -f pipeline.yaml

kubectl delete secret push-secret
```
