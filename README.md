
# Buildpacks Tekton Task for OpenShift
Runs without `privileged : true`  
Runs as `nonroot`

Based on:
https://github.com/tektoncd/catalog/tree/main/task/buildpacks/0.3/


## Install

### As developer user
```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.4/git-clone.yaml
```

```bash
REGISTRY_SERVER=https://index.docker.io/v1/ REGISTRY_USER=XXXXX REGISTRY_PASSWORD=XXXX

kubectl create secret docker-registry push-secret \
    --docker-server=$REGISTRY_SERVER \
    --docker-username=$REGISTRY_USER \
    --docker-password=$REGISTRY_PASSWORD

kubectl apply -f sa.yaml
```

### As kube-admin
```bash
oc adm policy add-role-to-user edit -z buildpacks-service-account --namespace=$(oc project -q)
oc adm policy add-role-to-user pipelines-scc-clusterrole -z buildpacks-service-account --namespace=$(oc project -q)
```

### As developer user
```bash
kubectl apply -f buildpacks.yaml -f resources.yaml -f pipeline.yaml 
```

## Run
```bash
kubectl create -f run.yaml
```

## Delete resources

### As developer user
```bash
kubectl delete task git-clone
kubectl delete pipelinerun --all
kubectl delete -f pipeline.yaml -f resources.yaml -f sa.yaml -f buildpacks.yaml
kubectl delete secret push-secret
```

### As kube-admin
```bash
kubectl delete rolebinding edit
kubectl delete rolebinding pipelines-scc-clusterrole 
```
