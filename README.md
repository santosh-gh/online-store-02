# Dockerize Microservices and run in Minikube Cluster
  #### 1. Docker Desktop
  #### 2. Dockerfile
  #### 3. Docker Image  
  #### 4. Docker Hub
  #### 5. kubectl

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

# Addons:

    dashboard – Kubernetes Dashboard

    metrics-server – Metrics for HPA

    ingress – NGINX Ingress controller

    registry – Local Docker registry

    registry-creds – Credential helper for registries

    storage-provisioner – Dynamic volume provisioning

# Build Images

    docker build -t order-service src/order-service
    docker build -t product-service src/product-service
    docker build -t store-front src/store-front

  docker images

# Tag Images

    docker tag order:latest e880613/order:1.0.0
    docker tag product:latest e880613/product:1.0.0
    docker tag store-front:latest e880613/store-front:1.0.0

# login

    docker login docker.io -u <username> -p <password>

# Push to docker hub

    docker push e880613/order:1.0.0
    docker push e880613/product:1.0.0
    docker push e880613/store-front:1.0.0

# Port Forward

    kubectl port-forward service/store-front 8080:80

    minikube service <service-name>


