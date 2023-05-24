# Service:
To achieve pod to pod communication in kubernetes we've kubernetes service, that can work as loadbalancer.

If we've multiple pods, we can attach those pods to the service and other pods can call through the serice name.


# Types of services:

1. clusetr IP  --> Purely Internal to the K8s cluster. 
                   It only works on pod to pod communication.  

2. NodePort: --> A NodePort is a type of service where you can  
                 expose the Port of the Node. 

So, Container port will attached to this NodePort, so user call this NODE-IP <Node_Port>, request comes to this NodePort and it forward the traffic to the container.


