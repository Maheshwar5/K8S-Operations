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


* Deployment has two responsibilities:

1. It needs to maintain zero downtime
2. New version should be applied at the same time.

* The highest object we've is deployment.
* When ever deployment happens, it creates one replicaset and it manage the Pods through replicaset.


# Scenario: If you change the vesrion of your application, let's say...

nginx-alpine


* Before that, let's give 10 replicas and change the version of the image.

* When you apply with new version, within few seconds the new version 
reflects. Means a zero downtime rolling update is happening.




# Rolling Update:
* Example: 10 pods are running, it'll create 11th pod with new version.

* 10 pods are running
* 11th pod with new version --> running
* It'll remove the 10th old pod
* 12th pod with new version --> running
* It'll remove 9th old pod

* This cycle goes until the 20th pod comes to running,

* 20th pod --> running
* 1st pod --> removed

* This is what happens in the background. That's why Deployment is so much useful and during this operation, you can still access the pods, because other pods are running.

* That's the main disadvantage of this approach. 

* We can control this behaviour using RollingUpdate strategy.


# Refer update strategies!




# Reference:
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/


* Another advantage of Deployment apart from replicaset is...

* If i create multiple image versions,

* For Example,

* Application

v1 is running
released v2, --> wrong

rollback to v1. Actually it is diffcult.


* With Deployments it is easy.



# For checking status of the deployment:
* kubectl rollout status deployment/nginx-deployment


# History of the deployment:
* kubectl rollout history deployment/nginx-deployment --revision=3


# To undo the deployment, 
# Rolling Back to Previous Revision:
* kubectl rollout undo deployment/nginx-deployment --to-revision=3



# Commands are useful in CI CD Process:
# CICD Process:
# create new deployment
# check deployment status

# If fine --> end pipeline --> success

# If fails go to previous version --> kubectl rollout undo deployment/nginx-deployment --to-revision=3

# --> error the pipeline --> end

# So that, immediatel a notification will goes to everyone. 
# Notification will say like... We tried to update to the new version, unfortunately it didn't go well, so we reverted back to the previous version. They will check with above commands.
