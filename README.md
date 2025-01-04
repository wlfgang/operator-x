# operator-x

## Getting Started

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
kubectl apply -f https://raw.githubusercontent.com/wlfgang/operator-x/1.0.0/dist/install.yaml
```

## Contributing
// TODO(user): Add detailed information on how you would like others to contribute to this project

**NOTE:** Run `make help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## License

Copyright 2025 wlfgang.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

