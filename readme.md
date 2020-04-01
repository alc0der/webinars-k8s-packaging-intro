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
## Adding Kustomization Overlay

One kustomization file is needed in each overlay

```base
kustomize edit add resource ../../base
kustomize edit set namespace dev
kustomize edit set image todo=todo:latest
kustomize edit set replicas todo=2
kustomize edit add patch patch-deployment.yaml
```

Running kustomize
```bash
kustomize build k8s/overlays/dev > k8s/overlays/dev/rendered.yaml
kubectl apply k8s/overlays/dev/rendered.yaml 
# or
kustomize build k8s/overlays/dev | kubectl apply -f -
```

# Ship

```bash
mkdir k8s/base-local/nginx
cd k8s/base-local/nginx
ship init https://github.com/helm/charts/tree/master/stable/nginx-ingress
# make sure to disable default gateway
touch kustomization.yaml
kustomize edit add resource ./nginx/rendered.yaml
cd ../overlays/dev
touch ingress.yaml
kustomize edit add resource ingress.yaml
# switch service to clusterIP
kustomize build k8s/overlays/dev > k8s/overlays/dev/rendered.yaml
kubectl apply k8s/overlays/dev/rendered.yaml 
```

# WATCH

watch 'echo "============ namespace: default ============"; kubectl get svc,deployment,po,ingress; echo "============ namespace: dev ============"; kubectl -n dev get svc,deployment,po,ingress'

