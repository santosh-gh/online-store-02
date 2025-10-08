# Microservices Deployment - 02

  ### Dockerize Microservices and run in Minikube Cluster

  #### 1. Docker Desktop
  #### 2. Dockerfile
  #### 3. Docker Image  
  #### 4. Docker Hub
  #### 5. kubectl
  #### 6. minikube
  #### 7. Imperative Deployment
  #### 8. Declarative Deployment

  GitRepo: https://github.com/santosh-gh/online-store-02


> [!NOTE]
> This example and source code is taken from Microsoft Documentations for FREE demo and learning purposes. 

# Online Store

This sample app consists of a group of containerized microservices that can be easily deployed into Kubernetes. 
This is meant to show a realistic scenario using a polyglot architecture, event-driven design, and common open 
source back-end services (eg - RabbitMQ). 

> [!NOTE]
> This is not meant to be an example of perfect code to be used in production, but more about showing a 
  realistic application running in Kubernetes. 

# Architecture

The application has the following services: 

| Service | Description |
| --- | --- |
| `order-service` | This service is used for placing orders (Javascript) |
| `product-service` | This service is used to perform CRUD operations on products (Rust) |
| `store-front` | Web app for customers to place orders (Vue.js) |
| `rabbitmq` | RabbitMQ for an order queue |

![Logical Application Architecture Diagram](assets/store-architecture.png)


# Install kubectl

    https://kubernetes.io/docs/tasks/tools/

# Kubectl Commands

  ## Version / Help	

      Show version info
      kubectl version
      
      Show help for all commands
      kubectl help	

  ## Cluster Info	

      Display cluster details
      kubectl cluster-info

      List all cluster nodes
      kubectl get nodes

      List all pods in current namespace
      kubectl get pods

  ## Deployment	

      Apply configuration from a YAML file
      kubectl apply -f file.yaml

      Create a deployment
      kubectl create deployment <name> --image=<image>

      Delete a pod
      kubectl delete pod <name>	

  ## Services	

      List services
      kubectl get services	

      Expose a deployment
      kubectl expose deployment <name> --type=LoadBalancer --port=80	

  ## Scaling	

      Scale a deployment
      kubectl scale deployment <name>	 --replicas=3	

  ## Logs	

      Show logs of a pod
      kubectl logs <pod-name>		

      Stream logs (follow mode)
      kubectl logs  <pod-name> -f	

  ## Exec / Debug	

      Open shell inside a pod
      kubectl exec -it  <pod-name> -- /bin/bash

      Show detailed pod info
      kubectl describe pod  <pod-name>	

  ## Namespaces	

      List namespaces
      kubectl get namespaces	

      Set current namespace
      kubectl config set-context --current --namespace=<namespace>	

  ## Config

      Show kubeconfig
      kubectl config view	

      Switch context
      kubectl config use-context <context>

  ## Apply / Delete Resources	
   
      Create or update resources
      kubectl apply -f file.yaml	

      Delete resources from file
      kubectl delete -f file.yaml	

  ## Port Forwarding	

      Forward local port to pod
      kubectl port-forward <pod-name> 8080:80	  

# Install Minikube

      https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download

# Minikube commands

  ## Version & Info

    Show Minikube version.
    minikube version	

    Show client/server Kubernetes versions.
    kubectl version -short	

  ## Basic Commands
     
    Start a local Kubernetes cluster.
    minikube start	

    Start using a specific driver (e.g., Docker, VirtualBox, Hyper-V).
    minikube start --driver=docker	

    Stop the running cluster.
    minikube stop	   

    Show the status of the cluster and its components.
    minikube status	

    Pause Kubernetes without shutting it down.
    minikube pause	

    Resume a paused cluster.
    minikube unpause

    Restart the Minikube cluster.	
    minikube restart	

    Update your kubeconfig to point to Minikube.
    minikube update-context	

  ## Resource Management

    Allocate specific resources.
    minikube start --cpus=2 --memory=2000

    Check for new Minikube version.
    minikube update-check

  ## Application Deployment

    Run kubectl commands directly through Minikube.
    minikube kubectl -- get pods

    Deploy an application.
    kubectl apply -f <file.yaml>

    Access a Kubernetes service via browser.
    minikube service <service-name>

    List all services and their URLs.
    minikube service list

  ## Networking
    
    Get the cluster’s IP address.
    minikube ip

    SSH into the Minikube VM/node.
    minikube ssh

    Mount local directory into Minikube.    
    minikube mount <host_path>:<vm_path>

  ## Addons

    List all available addons.
    minikube addons list	

    Enable an addon (e.g., dashboard, metrics-server, ingress).
    minikube addons enable <addon>	

    Disable an addon.
    minikube addons disable <addon>

    Open the addon’s UI in a browser.
    minikube addons open <addon>	

  ## Debugging & Troubleshooting

    Show logs from Minikube components.
    minikube logs	

    Access the Minikube VM to debug.
    minikube ssh	

    Completely remove all clusters and configs.
    minikube delete --purge	

    Print the URL for a service.
    minikube service <service-name> --url	  
  
  ## Kubernetes Dashboard

    Launch the Kubernetes Dashboard in a browser.
    minikube dashboard	

    Get dashboard URL without opening a browser.
    minikube dashboard --url	

  ## Multi-node & Profiles

    Start a multi-node cluster.
    minikube start --nodes=3	

    List nodes in the cluster.
    minikube node list	

    Add a new node to the cluster.
    minikube node add	

    Delete a node.
    minikube node delete <node-name>	
  
  ## Cleanup

    Delete the cluster and all data.
    minikube delete	

    Delete all Minikube clusters.
    minikube delete --all

    Clean up Docker images/containers (if using Docker driver).
    docker system prune -a

# Available Addons:

    dashboard – Kubernetes Dashboard

    metrics-server – Metrics for HPA

    ingress – NGINX Ingress controller

    registry – Local Docker registry

    registry-creds – Credential helper for registries

    storage-provisioner – Dynamic volume provisioning

# Crete minikube cluster

    minikube start

# Build Images

    docker build -t order-service src/order-service
    docker build -t product-service src/product-service
    docker build -t store-front src/store-front

  docker images

# Tag Images

    docker tag order-service:latest e880613/order-service:1.0.0
    docker tag product-service:latest e880613/product-service:1.0.0
    docker tag store-front:latest e880613/store-front:1.0.0

# login

    docker login docker.io -u <username> -p <password>

# Push to docker hub

    docker push e880613/order-service:1.0.0
    docker push e880613/product-service:1.0.0
    docker push e880613/store-front:1.0.0

# Deployment

    A Deployment in Kubernetes is a resource that manages a set of pods (containers) and 
    ensures that the desired state is maintained.

# Service

    A Service in Kubernetes is a stable network endpoint that exposes one or more pods to 
    internal or external traffic.

# Imperative Deployment 
    
  ## Config

      kubectl create configmap rabbitmq-enabled-plugins \
      --from-literal=rabbitmq_enabled_plugins="[rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]."    

  ## Rabbitmq

    - Deployment

      kubectl create deployment rabbitmq \
      --image=mcr.microsoft.com/azurelinux/base/rabbitmq-server:3.13 \
      --replicas=1

      # Set env

      kubectl set env deployment/rabbitmq \
      RABBITMQ_DEFAULT_USER=username \
      RABBITMQ_DEFAULT_PASS=password

      # Set resources

      kubectl set resources deployment/rabbitmq \
      --requests=cpu=10m,memory=128Mi \
      --limits=cpu=250m,memory=256Mi

      # Add ports

        kubectl patch deployment rabbitmq --type='json' -p='[
          {"op": "add", "path": "/spec/template/spec/containers/0/ports", "value": [
            {"containerPort": 5672, "name": "rabbitmq-amqp"},
            {"containerPort": 15672, "name": "rabbitmq-http"}
          ]}
        ]'

      # Add nodeSelector

      kubectl patch deployment rabbitmq --type='json' -p='[
        {"op": "add", "path": "/spec/template/spec/nodeSelector", "value": {"kubernetes.io/os": "linux"}}
      ]'

      # Add volume and mount

      kubectl patch deployment rabbitmq --type='json' -p='[
        {"op": "add", "path": "/spec/template/spec/volumes", "value": [
          {
            "name": "rabbitmq-enabled-plugins",
            "configMap": {
              "name": "rabbitmq-enabled-plugins",
              "items": [{"key": "rabbitmq_enabled_plugins", "path": "enabled_plugins"}]
            }
          }
        ]},
        {"op": "add", "path": "/spec/template/spec/containers/0/volumeMounts", "value": [
          {"name": "rabbitmq-enabled-plugins", "mountPath": "/etc/rabbitmq/enabled_plugins", "subPath": "enabled_plugins"}
        ]}
      ]'

    - Service

      kubectl expose deployment rabbitmq \
      --name=rabbitmq \
      --type=ClusterIP \
      --port=5672 --target-port=5672 \
      --port=15672 --target-port=15672

  ## Order  

    - Deployment

      kubectl create deployment order --image=e880613/order:1.0.0 \
      --replicas=1

    - Service

      kubectl expose deployment order \
      --port=3000 \
      --target-port=3000 \
      --name=order-service \
      --type=ClusterIP

  ## Product

    - Deployment

      kubectl create deployment product --image=e880613/product:1.0.0 \
      --replicas=1

    - Service

      kubectl expose deployment product \
      --port=3002 \
      --target-port=3002 \
      --name=product-service \
      --type=ClusterIP

  ## Store-front

    - Deployment

      kubectl create deployment store-front --image=e880613/store-front:1.0.0 \
      --replicas=1

    - Service

      kubectl expose deployment store-front \
      --port=80 \
      --target-port=8080 \
      --name=store-front \
      --type=LoadBalancer

  ## Port Forward

      kubectl port-forward service/store-front 8080:80

      minikube service store-front

  ## Clean up

      kubectl delete all -all 

# Declarative Deployment

  ## Create Manifests files

      config.yaml

      rabbit-deployment.yaml
      rabbit-service.yaml    

      order-deployment.yaml
      order-service.yaml

      product-deployment.yaml
      product-service.yaml

      store-front-deployment.yaml
      store-front-service.yaml

  ## Deploy    

      kubectl apply -f ./manifests/config -n dev

      kubectl apply -f ./manifests/rabbitmq -n dev

      kubectl apply -f ./manifests/order -n dev

      kubectl apply -f ./manifests/product -n dev 

      kubectl apply -f ./manifests/store-front -n dev


      kubectl delete -f ./manifests/config -n dev

      kubectl delete -f ./manifests/rabbitmq -n dev

      kubectl delete -f ./manifests/order -n dev

      kubectl delete -f ./manifests/product -n dev 

      kubectl delete -f ./manifests/store-front -n dev


  ## Port Forward

      kubectl port-forward service/store-front 8080:80

      minikube service store-front

  ## Clean up

      kubectl delete all -all