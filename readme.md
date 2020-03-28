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