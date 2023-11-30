# VLP - Virtual Learning Platform (Infrastructure)

This repository facilitates the deployment of the VLP (Virtual Learning Platfrom) application using Docker Compose for local development and Helm charts for Kubernetes environments.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Docker Compose](#docker-compose)
  - [1. Pull Docker Images](#1-pull-docker-images)
  - [2. Build and Start Containers](#2-build-and-start-containers)
  - [3. Access the Application](#3-access-the-application)
  - [4. Stop and Remove Containers](#4-stop-and-remove-containers)
- [Helm Chart](#helm-chart)
  - [1. Minikube Setup](#1-minikube-setup)
  - [2. Deploy Helm Chart](#2-deploy-helm-chart)
  - [3. Access the Deployed Application](#3-access-the-deployed-application)
  - [4. Uninstall Chart](#4-uninstall-chart)
  - [5. Additional Commands](#5-additional-commands)
- [Summary](#summary)

## Prerequisites

Before you begin, ensure that you have the following installed on your system:

- [Docker](https://docs.docker.com/get-docker/) - containerization platform that automates the deployment and scaling of applications within lightweight, portable containers.
- [minikube](https://minikube.sigs.k8s.io/docs/start/) - tool designed for local development, providing a convenient way to run Kubernetes clusters on a single machine.
- [kubectl](https://kubernetes.io/docs/tasks/tools/) - command-line tool for interacting with Kubernetes clusters, allowing users to deploy and manage applications on Kubernetes.
- [Helm](https://helm.sh/docs/intro/install/) - package manager for Kubernetes that simplifies the deployment and management of applications by providing a templating system and a collection of pre-configured packages called charts.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/vlp-docker.git
cd vlp-docker
```

## Docker Compose

Before you begin, ensure that you have started the Docker Desktop application.

The steps below cover the basic usage of docker-compose for setting up and managing the VLP (Virtual Learning Platform) application locally.

### 1. Pull Docker Images

If you've recently cloned the repository or wish to ensure you're using the latest versions of the Docker images, you'll need to pull them from Docker Hub. Navigate to the **vlp-docker-compose** folder, where the **docker-compose.yaml** file is located, using the terminal. Then, execute the following command:

```bash
docker-compose pull
```

### 2. Build and Start Containers

Build and start the containers as defined in the **docker-compose.yaml** file by running the following command:

_The_ **_-d_** _flag starts the containers in detached mode, hiding the logs. If you prefer to view the logs, simply omit the_ **_-d_** _flag._"

### 3. Access the Application

Once the containers are running, you can access and interact with the VLP application at the following URLs:

- **VLP Backend:** [http://localhost:34100](http://localhost:34100)
- **VLP UI:** [http://localhost:4200](http://localhost:4200)

### 4. Stop and Remove Containers

To stop and remove the Docker containers, execute the following command:

```bash
docker-compose down
```

This command stops and removes the containers, but **keeps the volumes (data persists)**.

If you want to **remove volumes as well**, add the **-v** option:

```bash
docker-compose down -v
```

## Helm Chart

Before you begin, ensure that you have started the Docker Desktop application.

### 1. Minikube Setup

- Start Minikube

```bash
minikube start --driver=docker --ports=31000:32000
```

- Get IP Address of the minikube cluster

```bash
minikube ip
```

- Edit **hosts** file in different operation systems:

  - [MacOS](https://www.imore.com/how-edit-your-macs-hosts-file-and-why-you-would-want#page1)
  - [Windows](https://www.groovypost.com/howto/edit-hosts-file-windows-10/)
  - [Ubuntu](https://manpages.ubuntu.com/manpages/trusty/man5/hosts.5.html)
    &nbsp;

- Add the IP to the hosts file:

```
127.0.0.1       localhost vlp.k8s.com
192.168.49.2 vlp.k8s.com
```

_replace 192.168.49.2 with the ip of your minikube cluster_

### 2. Deploy Helm Chart

After you have successfully setup the minikube environment,navigate to the **vlp-helm** folder, where the **Charts.yaml** file is located, using the terminal. Then, execute the following command:

```bash

helm upgrade --install vlp-helm .
```

_This command will either install a new release or upgrade an existing one, ensuring that the release is installed if it doesn't already exist_

### 3. Access the Deployed Application

Once the pods are up and running, you can access and interact with the VLP application at the following URL:

- **VLP UI:** [http://vlp.k8s.com:32000](http://vlp.k8s.com:4200)

### 4. Uninstall Chart

To stop and remove all the Kubernetes resources associated with a release, in our case vlp-helm, execute following:

```bash
helm uninstall vlp-helm
```

### 5. Additional Commands

In addition to the basic Minikube, Helm, and kubectl commands mentioned above, here are some supplementary commands that can be useful for managing the Kubernetes environment:

#### minikube

```bash
minikube service SERVICE_NAME --url # retrieve the URL for accessing the service exposed by the Kubernetes service.
minikube start                      # Start Minikube
minikube stop                       # Stop Minikube
minikube delete                     # Delete Minikube
minikube dashboard                  # View Minikube Dashboard
minikube ip                         # Get Minikube IP
minikube ssh                        # SSH into Minikube Node
minikube addons list                # List Minikube Addons
minikube addons enable ADDON_NAME   # Enable Minikube Addon
minikube addons disable ADDON_NAME  # Disable Minikube Addon
minikube config view                # Show Minikube Configuration
minikube config set KEY VALUE       # Set Minikube Configuration
minikube profile list               # List Minikube Profiles
```

#### kubectl

```bash
kubectl get pods                                      # Display all Pods in the current namespace
kubectl describe pod POD_NAME                         # Display detailed information about a Pod
kubectl get services                                  # Display all Services in the current namespace
kubectl describe service SERVICE_NAME                 # Display detailed information about a Service
kubectl get deployments                               # Display all Deployments in the current namespace
kubectl describe deployment DEPLOYMENT_NAME           # Display detailed information about a Deployment
kubectl get configmaps                                # Display all ConfigMaps in the current namespace
kubectl describe configmap CONFIGMAP_NAME             # Display detailed information about a ConfigMap
kubectl delete RESOURCE_TYPE RESOURCE_NAME            # Delete a resource by name
kubectl scale deployment DEPLOYMENT_NAME --replicas=3 # Scale a Deployment
kubectl logs POD_NAME                                 # Get logs from a Pod
kubectl get events                                    # Get all events in the current namespace
kubectl delete all --all                              # Delete all resources in the current namespace
```

#### helm

```bash
helm list -A              # List releases across all namespaces
helm list --uninstalled   # Show uninstalled releases
helm status vlp-helm      # Displays detailed information about the release
helm show chart vlp-helm  # Displays information about vlp-helm helm chart, such as its values, README, and templates.
helm show values vlp-helm # Displays the default values used by a Helm chart.
helm lint vlp-helm        # Checks vlp-chart for issues, ensuring it follows best practices.
```

## Summary

This repository streamlines the deployment of the Virtual Learning Platform (VLP) application, providing a flexible approach for both local development using Docker Compose and production environments leveraging Helm charts on Kubernetes.

- **Local Development with Docker Compose:** Quickly set up the VLP application on your local machine using Docker Compose. Pull the latest Docker images, build and start containers, and access the application at your fingertips.

- **Kubernetes Deployment with Helm Charts:** Take advantage of Helm charts for deploying the VLP application on Kubernetes. Whether you're using Minikube for testing or a production Kubernetes cluster, this repository simplifies the process. Access the deployed application and manage the lifecycle of the Helm release effortlessly.
