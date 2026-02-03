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

