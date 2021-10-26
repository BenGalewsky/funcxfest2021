# Setting up Kubernetes Endpoints
This repo contains slides and resources for the Kubernetes endpoint session
at [ParslFest/FuncXFaire 2021](https://parsl-project.org/parslfest2021.html).

The notebook [KubernetesEndpoint.ipynb](KubernetesEndpoint.ipynb) contains
the slides along with some simple cells for exercising the deployed endpoint.

## Instructions for Deploying the Endpoint
Assumes you have a Kubernetes Cluster

1. Add the funcX helm chart repo
```shell
helm repo add funcx http://funcx.org/funcx-helm-charts/  
```
2. Refresh the locally cached charts
```shell
helm repo update
```
3. Install the helm chart
```shell
helm install -f values.yaml funcx funcx/funcx_endpoint
```