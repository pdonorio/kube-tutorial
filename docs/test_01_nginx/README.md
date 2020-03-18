# first example

deploy and play with nginx on k8s

- example: [src](https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/)

- expose the port: [src](https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/)


## setup

Start the deployment, then verify and check

```bash
kubectl apply -f application-deployment.yaml
kubectl describe deployment nginx-deployment
kubectl get pods -l app=nginx
kubectl describe pod <pod-name>
```


## expose

To access the service we need to "expose" the referring port of our replicas

```bash
kubectl expose deployment nginx-deployment \
    --type=LoadBalancer --name=my-service
kubectl get services
# wait for the service to be ready and it shows the external IP
# when you get it try to access port 80 of that IP
# NOTE: make sure you don't try HTTPS instead, which is port 443

# check logs for all containers in the service/app
kubectl logs -f -l app=nginx
```


## update

You can use a new deployment (a copy of the original one)
and add a difference (e.g. image version), and run the update:

```bash
kubectl apply -f test_01_nginx/application-deployment-update.yaml
# watch the update
kubectl get pods -l app=nginx -w
```

NOTE: a new pod is spawn, and doesn't get used until it's green/online
so there is no downtime

Another example is scaling:
```bash
kubectl apply -f test_01_nginx/application-deployment-scale.yaml
# watch the update
kubectl get pods -l app=nginx -w
```

NOTE: you need to put a new replica value in the current or duplicated yaml to do so


## clean

Clean the service and deployment created

```bash
kubectl delete services my-service
kubectl delete deployment nginx-deployment
```
