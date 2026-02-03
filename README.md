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