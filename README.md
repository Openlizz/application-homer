<h1 align="center">Lizz compatible Homer application</h1>

Lizz compatible application to add the [Homer application](https://github.com/bastienwirtz/homer) to a Lizz managed Kubernetes cluster.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-homer \
    --path=./default \
    --destination=homer \
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.

> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

Check the pods with:

```
kubectl get pod -n homer
```

The output should be similar to:

```
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
homer           homer           main/b0dac60    False       True    Applied revision: main/b0dac60
```
    
## Usage

Access the application using port-forwarding or using the ingress created.

## Acknowledgements

This repository is only a wrapper to the [Helm chart](https://github.com/k8s-at-home/charts/tree/master/charts/stable/homer) of the [Homer application](https://github.com/bastienwirtz/homer) to help its deployment in a Kubernetes cluster managed by Lizz.

Therefore, the credit goes to the developers and maintainers of the application and the chart.