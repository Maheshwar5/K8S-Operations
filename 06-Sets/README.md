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

* If one of the Pod get deleted for any reason, it'll create another Pod automatically in order to maintain the desired number of Pods.

* A controller that always guarantees the desired number of Pods are running.

* Service is attaching to Pod based on Labels. 
* Similarly, ReplicaSet also understand which Pod to scale, based on the Labels.


* Problem: When there is a new version of application, you need to manually remove the replicaset and create again!

Note: replicaset only maintains the number of Pods. It cannot update the version, until you do it manually!


* To overcome this, we've a feature called deployment.

# Deployment:
* It can do updates to the application.


* When you apply the yaml file to deploy Pods, Pods are getting created, but the pattern is little different.

* Example for pod_name: nginx-deployment-7fb96c846b-kb9jh

* podname = [deployment_name]-[replicaset]-[random-name]

* Pod is a subset of replicaset.
* replicaset is a subset of deployment

* The highest object we've is deployment.
* When ever deployment happens, it creates one replicaset and it manage the Pods through replicaset.

