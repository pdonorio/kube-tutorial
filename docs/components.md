# components

Kubernetes is an orchestrator for containers.

It takes on its shoulder all the complex parts of managing containers on a cluster of multiple nodes: networking, load balancing, firewalls and proxying, scheduling, scaling, failure handling, etc.

It's composed of two main parts:
1. The control plane, which is the handler for accessing resources via APIs. It's composed of "master" nodes: ideally 3 nodes are required here to keep the SLA =~ 99.9%.
2. The workers node, solely dedicated to host operational containers. When a node is prepared to act as a kubernetes workers, it launches a series of containers agent that handle metrics and resources.

To provide simple management of containers and exploit their deployment and services through all the resources, kubernetes defines a sets of components that virtually map what you need to commands.

## namespaces

> Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. 

[src](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

Namespaces are a sets of resources virtually divided to separate things that don't belong together.

If for example you are running different apps (or allowing different teams or groups) in the same kubernetes cluster, you can keep things clean by separating what you view using kubernetes commands through namespaces. 

Kuberenetes system containers run in dedicated namespaces.

To see which namespaces are defined in your cluster:

```bash
kubectl get namespaces
```

The `default` namespace always exist, and it's the one used if you don't explicitly use a different one.

## pods

> Pods are a model of the pattern of multiple cooperating processes which form a cohesive unit of service.

[src](https://kubernetes.io/docs/concepts/workloads/pods/pod/#motivation-for-pods)

To simplify, when you group one or more container into the most basic kubernetes unit, you need a `pod`. Also:

> - Containers within a Pod share an IP address and port space, and can find each other via localhost. 
> - They can communicate with each other using standard inter-process communications.
> - Applications within a Pod also have access to shared volumes

NOTE: Pods aren’t intended to be treated as durable entities. 
They won’t survive scheduling failures, node failures, or other...

Let's see how it works:

```bash
# see your pods
kubectl get pods
# this is equivalent to
kubectl get pods --namespace default
# while to see everything you can do
kubectl get pods --all-namespaces
```

## deployments

> A Deployment provides declarative (creation and) updates for Pods

[src](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

How do you create or define updates to existing pods?
You will need to use the standard declarative format (a template in a `YAML` file). See the [official base example](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment) to have a first glimpse. 

The key parts are the `metadata` section, where you give for example name and labels for your deployment, and the `specs` which contains the key elements of your pods.

By running a deployment, kubernetes will act based on your declarations.

## services

Services define the behaviour of a subset of pods.
Since pods can die, but their reference (e.g. their IP) is vital to the other resources they talk to, a service will hold in kubernetes this references, and the other attribute related.

See [src](https://kubernetes.io/docs/concepts/services-networking/service/#motivation).

## storage

work in progress
