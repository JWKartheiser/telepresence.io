# Install with Helm

[Helm](https://helm.sh) is a package manager for Kubernetes that automates the release and management of software on Kubernetes. The Telepresence Traffic Manager can be installed via a Helm chart with a few simple steps.

## Before you begin

The Telepresence Helm chart is hosted by Ambassador Labs and published at `https://www.getambassador.io`.

Start by adding this repo to your Helm client with the following command:

```shell
helm repo add datawire https://www.getambassador.io
```

## Install with Helm

When you run the Helm chart, it installs all the components required for the Telepresence Traffic Manager.

1. If you are installing the Telepresence Traffic Manager **for the first time on your cluster**, create the `ambassador` namespace in your cluster:

   ```shell
   kubectl create namespace ambassador
   ```

2. Install the Telepresenc Traffic Manager with the following command:

   ```shell
   helm install traffic-manager --namespace ambassador datawire/telepresence
   ```

For more details on what the Helm chart installs and what can be configured, take a look at the Helm chart [README](https://github.com/telepresenceio/telepresence/tree/release/v2/charts/telepresence).

### Install into custom namespace

The Helm chart supports being installed into any namespace, not necessarily `ambassador`. Simply pass a different `namespace` argument to `helm install`.
For example, if you wanted to deploy the traffic manager to the `staging` namespace:

```bash
helm install traffic-manager --namespace custom-namespace datawire/telepresence
```

Note that users of telepresence will need to configure their kubeconfig to find this installation of the traffic manager:

```yaml
apiVersion: v1
clusters:
- cluster:
    server: https://127.0.0.1
    extensions:
    - name: telepresence.io
      extension:
        manager:
          namespace: custom-namespace
  name: example-cluster
```

See [the kubeconfig documentation](../reference/config#manager) for more information.

## Install RBAC only

Telepresence Traffic Manager does require some [RBAC](../../refrence/rbac/) for the traffic-manager itself, as well as for users.
To make it easier for operators to introspect / manage RBAC separately, you can use `rbac.only=true` to
only create the rbac-related objects.
Additionally, you can use `clientRbac.create=true` and `managerRbac.create=true` to toggle which subset(s) of RBAC objects you wish to create.
