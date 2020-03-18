# setup

Go to [digital ocean](https://try.digitalocean.com/performance/) with this special link. Register your account, add a credit card, and get 100$ to use in 60 days.

When you're ready and confirm the credits, you're ready to head to:
[https://cloud.digitalocean.com/kubernetes/clusters](https://cloud.digitalocean.com/kubernetes/clusters).

Read a little bit around, then click "Create a Kubernetes Cluster"!
- select the latest version
- choose Frankfurt or Amsterdam region if you're in Europe like me
- leave the defaults for cluster capacity
- choose a short name, e.g. `my-first-k8s`

That's all

Now follow the rest of instructions. In step 2, `Install management tools` you will find out you need to install `kubectl` and `doctl` installed on your terminal, so in step 3 you can download correctly your config file to query your cluster from the command line. NOTE: you can probably download the config file from the UI too, in which case you might skip doctl installation.

When you're all set, try a basic command like:
```bash
kubectl get pods --all-namespaces
```


