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

<!-- NAME                           READY   STATUS              RESTARTS   AGE
nginx-deployment-547d878d89-2js5t   1/1     Running             0          62s
nginx-deployment-547d878d89-4bcbs   1/1     Running             0          64s
nginx-deployment-547d878d89-674sb   1/1     Running             0          63s
nginx-deployment-547d878d89-cfhzx   1/1     Running             0          63s
nginx-deployment-547d878d89-dmr5f   1/1     Running             0          64s
nginx-deployment-547d878d89-drzpr   1/1     Running             0          64s
nginx-deployment-547d878d89-lzgnz   1/1     Running             0          64s
nginx-deployment-547d878d89-stj6j   1/1     Terminating         0          63s
nginx-deployment-547d878d89-x4djg   1/1     Terminating         0          63s
nginx-deployment-547d878d89-zf6jn   1/1     Running             0          64s
nginx-deployment-965685897-2ddhw    0/1     ContainerCreating   0          0s
nginx-deployment-965685897-72mpw    0/1     ContainerCreating   0          0s
nginx-deployment-965685897-8twv7    0/1     ContainerCreating   0          0s
nginx-deployment-965685897-tbgc2    0/1     ContainerCreating   0          0s
nginx-deployment-965685897-tz5lc    0/1     ContainerCreating   0          0s -->


