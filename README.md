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


