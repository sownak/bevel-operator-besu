# bevel-operator-besu
WIP
This is a WIP repository for Kubernetes Operator for Hyperledger Besu

## Description

This will evolve to form a complete operator for Hyperledger Besu. Currently, it is helm based operator only. Contributions are welcome.

## Getting Started
You’ll need a Kubernetes cluster to run against. You can use [KIND](https://sigs.k8s.io/kind) to get a local cluster for testing, or run against a remote cluster.
**Note:** Your controller will automatically use the current context in your kubeconfig file (i.e. whatever cluster `kubectl cluster-info` shows).

### Running on the cluster
1. Build and push your image to the location specified by `IMG`:

```sh
make docker-build docker-push IMG=<some-registry>/bevel-besu-operator:tag
```

1. Deploy the controller to the cluster with the image specified by `IMG`:

```sh
make deploy IMG=<some-registry>/bevel-besu-operator:tag
```

1. Verify that the bevel-operator-besu is up and running:

```sh
kubectl get deployment -n bevel-operator-besu-system
NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
bevel-operator-besu-controller-manager   1/1     1            1           8m

```

1. Install Instances of Custom Resources:

```sh
# Genesis should be run first
kubectl apply -f config/samples/charts_v1alpha1_besu-genesis.yaml

# then apply the validators and members
kubectl apply -f config/samples/charts_v1alpha1_besu-validator-1.yaml
kubectl apply -f config/samples/charts_v1alpha1_besu-validator-2.yaml
kubectl apply -f config/samples/charts_v1alpha1_besu-validator-3.yaml
kubectl apply -f config/samples/charts_v1alpha1_besu-member-1.yaml
```

1. Updates

```sh
# Make changes to the validator or member files and apply
# NOTE genesis updates would not work as it is a job
kubectl apply -f config/samples/charts_v1alpha1_besu-member-1.yaml
```

### Uninstall CRDs
To delete the CRDs from the cluster:

```sh
make uninstall
```

### Undeploy controller
UnDeploy the controller from the cluster:

```sh
make undeploy
```

## Contributing

First things first, please review the [Hyperledger Code of Conduct](https://wiki.hyperledger.org/display/HYP/Hyperledger+Code+of+Conduct) before participating and please follow it in all your interactions with the project.

The helm chart operator is complete, only updates will be needed as new versions of the charts are released. 

The contributions that are needed are:
- Go lang controllers to add additional CLI capabilities to the operator. 

You are welcome to join us at [Discord channel](https://discord.com/channels/905194001349627914/941739691336679454). [Please join our Discord first](https://discord.gg/hyperledger). 

### How it works
This project aims to follow the Kubernetes [Operator pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/).

It uses [Controllers](https://kubernetes.io/docs/concepts/architecture/controller/),
which provide a reconcile function responsible for synchronizing resources until the desired state is reached on the cluster.

### Test It Out
1. Install the CRDs into the cluster:

```sh
make install
```

2. Run your controller (this will run in the foreground, so switch to a new terminal if you want to leave it running):

```sh
make run
```

**NOTE:** You can also run this in one step by running: `make install run`

### Modifying the API definitions
If you are editing the API definitions, generate the manifests such as CRs or CRDs using:

```sh
make manifests
```

**NOTE:** Run `make --help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## License

Copyright 2024.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.



