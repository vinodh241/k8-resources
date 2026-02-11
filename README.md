# container Orchestrator :
--------------------------
* kubernetes : k8  --PAAS
 -----------------
 Auto scaling is easy, storage is outside of cluster, roll back and multiple deployment strategies are available in kubernetes. 
 Networking between containers is little easy in kubernetes

 # cluster:
 ================= 

terms:

* control plane
* worker nodes 
* Pods
* ConfigMap
* Service
* RollBack
* Blue-Green
* Secrets
* Replicaset
* Labels 
* Namespace


* data is not stored in clusters , stored outside of cluster ( volumes)
* we can configure n number of nodes 

  * A single masternode and mutliple worker nodes 
  * Here we are writing manifest files 
  * using terraform we can create culster 
  * To interact with cluster using kubectl 

# Workstation:
 -----------

 1. install docker 
 2. Run aws configure 
 3. install eksctl for cluster creation ( we have mini kube , if it install system will slow)
 4. install kubectl for cluster intercation 

===================================================================================================================

#  Install eksctl and kubectl :
 ---------------------------

 * aws configure

 * ARCH=amd64

 * PLATFORM=$(uname -s)_$ARCH

 * curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

 * curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

 * tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

 * sudo install -m 0755 /tmp/eksctl /usr/local/bin && rm /tmp/eksctl

 * eksctl version

 * curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.34.2/2025-11-13/bin/linux/amd64/kubectl

 * chmod +x ./kubectl

 * sudo mv kubectl /usr/local/bin/kubectl

 * kubectl version

=======================================================================================================================

# How to create a cluster :
-----------------------------

* eksctl create cluster --config-file=eks.yaml 

* eksctl delete cluster --config-file=eks.yaml 

* kubectl get nodes -- shows the worker nodes

* everything is called resources in kubernetes 


# ManageNode Group:
-----------------
No need to login aws instances and install , managenode component will take care everything 


# spot instances:
  --------------

on-demand -- whenever you required  you create instances , aws gaurntees you  to get instances 

spot -- aws data center have lot of resources 
 give for less cost 70-90 % discount --

# namespace:
  -------------

  * Isolated project space in kubernetes where you can create your workloads


syntax:

    apiVersion: v1  -- 
    kind: Namespace
    metadata:
      name: devlopment
      labels:
        project: roboshop
        environment: dev 

* comman for every resource group

##

# how to create namespaces?
-------------------------

* kubectl apply -f <file.yam> -- create a namespace

* kubectl delete -f <file.yam> -- delete the namespace 

* kubectl get namespaces  -- to get the namespaces 


## POD:
--------

* pod is like container 

* it contains all basic resources 

* but k8's definition : pod is smallest deployable unit in kubernetes , one pod have multiple containers 

 POD definition:
 ==============

 apiVersion: v1
 kind : Pod 


# To create pod command is ?
-------------------------------

* kubectl apply -f <file.yaml>

* kubectl get pods -- to show the pods 

* kubectl describe pod <pod-name>  -- to check the pod errors 

Note: if you install os and except to run container it will not run , you should install some softwares then it will run continsouly 

* * *  if you make or add any chnages on sepc: fileds , if you trying to re-create pod it wont work, so need to delete the pods and re-create again 


# How to login pod ( inside container) ?
------------------------------------------


* kubectl exec -it <pod-name> -- bash 

#  if you have mutli-containers inside pod then how to login?
----------------------------------------------------------

* kunectl exec -it <pod-name> -c <container-name> -- bash 

                                | 
                           container name
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# POD                                   VS                                                     container
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
* pod is the smallest deployable unit in k8                                                                                
  A pod can have 1 or many contaners.
  all containers inside pod sahre same n/w & 
  storage 


* Multi-container are useful in sidecar patterns and proxy patterns. proxy means frist proxy container gets the request , it checks whether reuest should be forwwarded to main container or not 


## CrashLoopBackOFF: Error 
----------------------
container is unable to start 


## LABLES:
-----------------

* Metadata (Labels)

  metadata:
  name: nginx-np
  labels:
    purpose: service-np-demo
    project: roboshop
    environment: dev

 # Container Section

spec:
  containers:
  - name: nginx
    image: nginx   


* labels are used as selectors for other resources ......., labels values we cant keep long values, we can keep only 63 charcters 

# Annotations"
------------------------

* annotations are similar to labels , it is key value pair, but not used as seletors, annatations are used to provision external resources to k8's
 we keed external informations build url , image registry , etc .. Annatations values can be 256 charcteres 


## Resource limiting:
-----------------------
* we can limit the resoures using resouce limits, ( like cpu , memory)

* soft limit ( for softwares)
* hard limit ( for hardwares)


# Vertical & Horizontal scaling:
---------------------------------


* before increase the limit need to stop the instance and increase  the resources it is called vertical scaling , we have down time and single point of failures

* Horizontal scaling means prallel creating another instances ( means parallely creating pods) , we are using horizontal scaling 



# How to check pods how much resources utilizing ?
 ------------------------------------------------

 * kubectl top pods


# configMap:
-----------------

* we try to keep the configurations out side of pod definition ,. i;e is called configmap 
* here we keep non conf

* kubectl get configmap

# Secrects 
--------------

* Here data should be encoded 
* for storing the username and password for DB and other users 

 Ex: echo -n "username" | base64 
  
   The above command will give you base64 encrypted format 


# Service Mesh:
---------------

* pod to pod communication , IP address is not useful since it is ephemeral 
* we have services in kubernetes to achive 
 1. cluster IP -- internal to the cluster 

 2. Load balancing  -- it will open one port called nodePort in every node 
   * it will work only in cloud environment


 3. nodeport -- it will create a loadbalancer and nodeport in the all nodes

 * like assiging ports to containers 


# NodePorts:
---------------------

👉 What is NodePort?

NodePort is a Service type in Kubernetes that exposes a Pod externally by opening a static port (30000–32767) on each cluster node. External users can access the application using NodeIP:NodePort.

* node port ip is a cluster IP , but it has extra futures, opening a port in worker node , it has internal communication capalities 

* default node port range is { 30000-32767 }

## How can i create multiple pods to same image?
=================================================
* A replica set purpose is to maintain a stable set of replica pods running at any given time, 

  spec: 
  replicas: 2

* define a deployment and let that deployment manage replicasets automatically 

# Deployment:
===============

* Pod is sub set of replicaset
* replicaset is a subset of deployment 

# Volumes:
===========

* volumes nothing but = storage 
* EBS -- elastic block storage  - Docker
* EFS -- elastic file system  - kubernetes 

* in kubernetes, its  self created a storage classes t oreduce the dependencies between storage and remainig resources
  on behalf us it will login and it will perform operations 

* PV   -- persistant voulme
* PVC  -- persistant volume claim 
* SC   -- storage class 

EBS:
=====

1. Static provisioning --  need to be create storage class 
2. dynamic provisioning -- disk will be created automatically 

EBS Static provisioning:
== - == - == - == - == 

1. Need to create a disk
2. EBS disks should be in the same EC2 and AZ zone 
3. Install drivers
4. Ec2 nodes should have permissions to connect EBS disks.

# PV: persistant volume:
------------------------
 * it is the physical representation of the volumes

 # PVC:
 ==========

 * it is claiming resources of the storage . i;e PV 
* Once PV and PVC volumes created need to attch them into POD

* once you can create PV and PVC its should go to the perticlur availability zone , we should create a lables to nodes and use those   lables as ( NODE Selectors) 
 In side POD

 * 