# Service:

Kubernetes service works as a LoadBalancer between the pods. 
We can use this service for pod to pod communication. Because Pods are ephemeral, IP Address may change anytime.
But if you use service, you can call other Pods with the name of the service.

If we've multiple pods, we can attach those pods to the service and other pods can call through the serice name.



# There are three types of services:

1. clusetr IP  --> Purely Internal to the K8s cluster. 
                   It only works on pod to pod communication.  

2. NodePort: --> A NodePort is a type of service where you can  
                 expose the Port of the Node. 

So, Container port will attached to this NodePort, so user call this NODE-IP <Node_Port>, request comes to this NodePort and it forward the traffic to the container.


When NodePort is created, clusterIP is also get created automatically.

When you use NodePort, it'll open the port in each and every Node in EKS cluster.  



3. Load Balancers: 

AWS
Azure
GCP


Mechanism: 
ELB --> It'll got to any instance on NodePort --> ClusterIP --> Pod


# Service Flow:

ClusterIP is a subset of NodePort
NodePort is a subset of LoadBalancer

request comes from top to bottom
1. LB 
2. NodePort
3. ClusterIP 
4. Pod

