# Pods
-- Smallest Unit of K8s
-- Abstraction Over Container : Run Environment Over Docker Container  
-- Usually 1 application per pod 
-- Each Pod Gets It is own Ip Address 

-- Pods Are ephemeral : Thats Mean that they Can die very Easily And new One Will Be Created With New Ip Address 

# Service 
--Permanent Ip Address with Dns Name
-- lifecycle of pods and service is not connected  

-- Load Balancer 
    => if you need to define new pod you will not add new pod but
    define blueprints for pods (Specify how many replicas)

# Database
-- database url usually in the built application 

# configMap
-- Your External Configuration of your application  

# Secret
--Used To Store secret data (Database username And Password )
--base64 encoded 

# Data Storage 
 => Volumes : Storage on Local Machine or Remote , Outside of the K8s Cluster

 # StateFulSet
 => for stateful apps or databases


 # Cluster set-Up
 => 2 master node and 3 slaves

 # MinCube Test Local Cluster setup on Virtual Box


 # To Start Minikube
    =>minikube start --driver=hyperv 
    -- Enable HyperV:
       =>Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
# Get Nodes 
    =>kubectl get nodes

# Check minikube status:
    =>minikube status

# Create Deployment Called Nginx-depl from Nginx Docker Image 
    =>kubectl create deployment nginx-depl --image=nginx

    =>Get Deployments 
    --kubectl get deployment
# pods
    =>Consist of Deployment Name + Replica Set Id And Its own Id

# Edit Configuration File for Deployment (nginx-depl)
    =>kubectl edit deployment nginx-depl

# Debugging Pods

    -- Get Logs For monogo-deployment:
        => kubectl logs mongo-deployment-{pod-name} 
    -- Get Pods Describe 
        => kubectl describe pod mongo-deployment-{pod-name}
    -- Get Wide Information About Pod 
        =>kubectl get pods -o wide

# Get Terminal for Mongo-deployment
    => kubectl exec -it monggo-deployment-6cffdd4d69-5xk92 (pod name for mongo-deployment container ) -- bin/bash  (Note You Must Keep space between -- and flag (bin/bash))

# Exit from Terminal 
    =>Exit

# Delete Deployment
    => Kubectl delete deployemt  Deployment Name


# Apply Deployment Using Yaml File 
    =>kubectl apply -f [filename]
    --apply can create and configure if you edit yaml file


# Each Configuration File consist of 3 parts 
    --Metadata  
    --Specification
    --Status
        => Desire Statue Vs Actual Statue

# Etcd (cluster brain)
    => Holds The Current status Of Any K8s Component 


# Layers Of Abstraction 
    =>Deployment Manages a
    =>Replica set Manage a
    =>Pod Manage a
    =>Container 


# template 
    -- Has it is own metadata and spec section 

# Sample Configuration File For Deployment 
apiVersion: apps/v1
kind: Deployment 


---------  # is first part of Configuration file has some attributes [Name etc] ----------------
metadata: 
------ #Name Of The Deployment ------------
  name: nginx-deployment   
  labels:
    app: nginx
    ---------- # Specification For Deployment (it is the second part of configuration file) -------
spec: 
  replicas: 2

  ---------- #Connection Between Deployment And It is Pods ----------
  selector:  
    matchLabels:
    --Label  Key Value Pair App : Nginx Used To Connection
      app: nginx
  template:
    metadata:
      labels:
        app: nginx

    ---------- # Specification for Pods ---------------
    spec: 
      containers:
        - name: nginx
          image: nginx:1.16
          ports:
            - containerPort: 8080



# port In Service And Pod 
 -- Ports 
      -protocol:TCP
       port :80
       targetPort:8080
 => Db Service Connect To Nginx Service On port  80  
 => And Connect to Pod on 8080 That match pod configuration  

# Get Content Of Configuration File inTo Yaml File 
    =>kubectl get deployment nginx-deployment -o Yaml > ngnix-deployment-result.Yaml



# Secret Configuration File 

apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
type: Opaque   => Opaque It is The Default Type    Key-value Pair
data:
    mongo-root-username:dXNlcm5hbWU=
    mongo-root-password:cGFzc3dvcmQ=

