# external access

Access to external k8s can be done with credentials.

NOTE: this can be done only if you have already a kubernetes "hand made" cluster to handle. Nevertheless, it's an interesting quick read.

More info in the [official docs](https://kubernetes.io/docs/reference/access-authn-authz/authentication/) and [this blog post](https://medium.com/@emirozbirdeveloper/kubernetes-manage-access-via-certificates-1b3e9948cfc4).

## setup

Certificates needed for this operation are 3:
1. `admin.key`
2. `admin.crt`
3. `ca.crt`

If you have them, just follow these steps:

```bash
CLUSTER_NAME=...
SERVER_URL=...
kubectl config set-cluster $CLUSTER_NAME --server=$SERVER_URL

kubectl config set-cluster $CLUSTER_NAME --certificate-authority=ca.crt
kubectl config set-credentials fulladmin \
    --client-key=admin.key --client-certificate=admin.crt
kubectl config set-context $CLUSTER_NAME \
    --user=fulladmin --cluster $CLUSTER_NAME
kubectl config use-context $CLUSTER_NAME
```

The key concept here is that you can handle multiple `config` in your `$HOME/.kube` directory. Defining contextes you can switch seamlessly between different clusters on your kubectl binary.

## ports and basic proxy

To access private ports of pods, you need to forward the port to your local client through the kubectl tool. Docs are [here](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/).

```bash
# depends on your pod configuration
PORT=8080

kubectl get pods | grep MY_POD_PREFIX | awk "{print $1}"
kubectl port-forward $POD_NAME $PORT:PORT
```

With this operation you can basically map that container port to a local port. This gives access only to your local machine to that port, in a secured way.
