# Setting up Kubernetes Endpoints
This repo contains slides and resources for the Kubernetes endpoint session
at [ParslFest/FuncXFaire 2021](https://parsl-project.org/parslfest2021.html).

The notebook [KubernetesEndpoint.ipynb](KubernetesEndpoint.ipynb) contains
the slides along with some simple cells for exercising the deployed endpoint.

## Instructions for Deploying the Endpoint
The endpoint is packaged as a Helm Chart with several useful options that 
can be set with a `values.yaml` file.

## Install Your FuncX Credentials
The first time you deploy an endpoint to your cluster, you will need to install
your funcX tokens as a Kubernetes Secret.

If you've used the funcX client, these will already be available
in your home directory's `.funcx/credentials` folder. If not, they can easily
be created with:
```shell
pip install funcx
python -c "from funcx.sdk.client import FuncXClient; FuncXClient()"
````
It will prompt you with an authentication URL to visit and ask you to paste the
resulting token.

Now that you have a valid funcX token, cd to your `~/.funcx/credentials`
directory and install the keys file as a kubernetes secret.

```shell script
kubectl create secret generic funcx-sdk-tokens --from-file=funcx_sdk_tokens.json
```

## Deploy the Helm Chart
Assumes you have a Kubernetes Cluster and the 
[helm CLI](https://helm.sh/docs/intro/quickstart/) available.

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