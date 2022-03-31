
# Buildpacks Tekton Task for OpenShift
Runs without `privileged : true`  
Runs as `nonroot`

Regular user should be able to run this Task, ie. no cluster admin rights are required.

Based on:
https://github.com/tektoncd/catalog/tree/main/task/buildpacks/0.3/


## Install

```bash
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/task/git-clone/0.4/git-clone.yaml
```

### Create a secret with `~/.docker/config.json` contents
kubectl apply -f secret.yaml
```

```bash
kubectl apply -f buildpacks.yaml -f resources.yaml -f pipeline.yaml 
```

## Run
```bash
kubectl create -f run.yaml
```

## Delete resources
```bash
kubectl delete task git-clone
kubectl delete pipelinerun --all
kubectl delete -f pipeline.yaml -f resources.yaml -f buildpacks.yaml -f secret.yaml
```
