# VLP - Virtual Learning Platform (Infrastructure)

## Prerequisites

<ul>
  <li> Docker </li>
  <li> Minikube - Locally installed Kubernetes cluster </li>
  <li> Kubectl - Kubernetes command line tool </li>
  <li> Helm (v3) - package manager for Kubernetes</li>
</ul>

## Start minikube

```
minikube start
```

### Enable ingress addon

```
minikube addons enable ingress
```

### Get IP Address of the minikube cluster

```
minikube ip
```

### Add the IP to the hosts file

```
# VLP Hosts
192.168.49.2 vlp.k8s.com
```
