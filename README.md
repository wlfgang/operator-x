# operator-x

A basic example Kubernetes operator implemented in Go using Operator SDK.

## Getting Started

To simply install the operator in your cluster, you can do:
```sh
kubectl apply -f https://raw.githubusercontent.com/wlfgang/operator-x/refs/tags/1.0.0/dist/install.yaml
```
If you want to modify anything, read on.

### Prerequisites
- go version v1.22.0+
- docker version 17.03+.
- kubectl version v1.11.3+.
- Access to a Kubernetes v1.11.3+ cluster.

### To Deploy on the cluster

Build and push the container to the specified registry:
```sh
make docker-build docker-push IMG=ghcr.io/wlfgang/operator-x:1.0.0
```

Install the CRDs into the cluster:
```sh
make install
```

Deploy the Manager to the cluster:
```sh
make deploy IMG=ghcr.io/wlfgang/operator-x:1.0.0
```

You can apply the samples (examples) from the config/sample:
```sh
kubectl apply -k config/samples/
```

### To Uninstall

Delete the instances (CRs) from the cluster:
```sh
kubectl delete -k config/samples/
```

Delete the APIs(CRDs) from the cluster:
```sh
make uninstall
```

UnDeploy the controller from the cluster:
```sh
make undeploy
```

## Project Distribution

Following are the steps to build the installer and distribute this project to users.

1. Build the installer for the image built and published in the registry:

```sh
make build-installer IMG=ghcr.io/wlfgang/operator-x:1.0.0
```

NOTE: The makefile target mentioned above generates an 'install.yaml'
file in the dist directory. This file contains all the resources built
with Kustomize, which are necessary to install this project without
its dependencies.

2. Using the installer

Users can just run kubectl apply -f <URL for YAML BUNDLE> to install the project, i.e.:

```sh
kubectl apply -f https://raw.githubusercontent.com/wlfgang/operator-x/refs/tags/1.0.0/dist/install.yaml
```
