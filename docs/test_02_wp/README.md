# second example

deploy and play with wordpress and storage persistence

- example: [src](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)

- yamls: [src](https://github.com/kubernetes/examples/tree/master/mysql-wordpress-pd)

- use block storage on DO: [src](https://www.digitalocean.com/docs/kubernetes/how-to/add-volumes/)


## setup

Learning there is a `kustomization.yaml` file that can bring together, merge, patch and declare things for your app in kubernetes.

Super cool.
Putting that file in the folder, all you have to do is now:

```bash
kubectl apply -k test_02_wp/
```

## check

```bash
kubectl get secrets
kubectl get pvc
kubectl get pv
kubectl get services -l app=wordpress
```

## clean

```bash
kubectl delete -k test_02_wp/
```

