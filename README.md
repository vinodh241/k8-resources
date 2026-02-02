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

* kubectl apply -f <yaml.file> -- create a namespace
* kubectl delete -f <yaml.file> -- delete the namespace 

* kubectl get namespaces  -- to get the namespaces 

## POD:
--------

* pod is like container 
* it contains all basic resources 
* but k8's definition : pod is smallest deployable unit in kubernetes , one pod have multiple containers 



