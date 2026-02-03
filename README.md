##
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

* To create pod command is ?
-------------------------------

* kubectl apply -f <file.yaml>

* kubectl get pods -- to show the pods 

* kubectl describe pod <pod-name>  -- to check the pod errors 

Note: if you install os and except to run container it will not run , you should install some softwares then it will run continsouly 

* * *  if you make or add any chnages on sepc: fileds , if you trying to re-create pod it wont work, so need to delete the pods and re-create again 


# How to login pod ( inside container) ?
------------------------------------------


* kubectl exec -it <pod-name> -- bash 

* if you have mutli-containers inside pod then how to login?
----------------------------------------------------------

* kunectl exec -it <pod-name> -c <container-name> -- bash 

                                | 
                           container name
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# POD                                                                           VS                                                     container
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

* labels are used as selectors for other resources ......., labels values we cant keep long values, we can keep only 63 charcters 

# Annotations"
------------------------

* annotations are similar to labels , it is key value pair, but not used as seletors, annatations are used to provision external resources to k8's
 we keed external informations build url , image registry , etc .. Annatations values can be 256 charcteres 


## Resource limiting:
-----------------------
* we can limit the resoures using resouce limits


# Vertical & Horizontal scaling:
---------------------------------


* before increase the limit need to stop the instance and increase  the resources it is called vertical scaling , we have down time and single point of failures

* Horizontal scaling means prallel creating another instances ( means parallely creating pods) , we are using horizontal scaling 



* How to check pods  how much resources utilizing ?
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

