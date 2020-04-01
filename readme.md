# Building and Running with Docker

```bash
docker build -t todo:1.0.0 .
docker run --rm --name todo-docker-example -p 80:8080 todo:1.0.0
open http://localhost
```
# HELM 

## Creating, Installing, Editing, and Uninstalling Helm Charts

```bash
helm create todo
# edit files: values, Chart, and deployment
helm install todo
helm uninstall todo
```

## Helm Templating

```bash
helm template todo > todo/rendered.yaml
```

# Kustomize

## Adding a Working Base

Unlike Helm the base template for Kustomize is just a normal valid YAML that can simply be deployed with `kubectl apply`.

```bash
docker tag todo:1.0.0 todo:latest
kubectl apply -f k8s/base
```

## Adding Kustomization Base

One Kustomization file is needed in base

```bash
cd k8s/base
kustomize edit add resource deployment.yaml 
kustomize edit add resource service.yaml
kubectl apply -k k8s/base
```
