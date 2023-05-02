### namespace 
Kubernetes resources:

1. namespace:

Def: namespace is a logical isolation of project resources in kubernetes. 

- it is a space where you can create your containers or Pods.

- every project will have one namespace

- in our project we create a namespace called roboshop.

- we can have only roboshop resources only at security level.


Ex: namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: roboshop

$ kubectl create -f namespace.yaml

we created a namespace with name roboshop