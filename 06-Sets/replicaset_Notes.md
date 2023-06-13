# Sets:
  =====

# ReplicaSet:

# Pod:
* Now, 
I want multiple replicas/pods? How can i do that?
Ans: ReplicaSet

# ReplicaSet
* It can create multiple pods. ReplicaSet always guarantees in running a desired number of Pods.    

* ReplicaSet manages the Pod lifecycle.

* If one of the Pod get deleted y any reason, it'll create another Pod automatically in order to maintain the desired number of Pods.

* A controller that always guarantees the desired number of Pods are running.




* Service is attaching to Pod based on Labels. 
* Similarly, ReplicaSet also understand which Pod to scale, based on the Labels.

Example yaml:
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels: # This sis the syntax, ReplicaSet uses to find which Pod should be scaled and maintain.
      tier: frontend
  template: # This is Pod template. Labels are related to Pod. 
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx


