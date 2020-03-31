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