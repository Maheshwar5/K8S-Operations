1. Pods
reference: https://kubernetes.io/docs/concepts/workloads/pods/


Pod vs Container:

- container is just one
- Pod can have multiple containers


Pod:

Ex: pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: roboshop
spec:
  containers:
  - image: nginx:1.14.2
    name: nginx
    ports:
      - containerPort: 80 

$ kubectl apply -f podyaml


$ kubectl get po    
$ kubectl get po -o wide

- To get pods specification in yaml format
$ kubectl get po -o yaml




$ kubectl get po -n roboshop -o wide

IP
192.168.xx.xxx

- let us login to instances to check access to pods

Take private IP of worker instance and login

$ curl 192.168.xx.xxx

you'll see welcome message!


- But you cannot access this outside of the nodes.