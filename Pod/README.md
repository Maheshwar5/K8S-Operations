1. Pods
reference: https://kubernetes.io/docs/concepts/workloads/pods/


Pod vs Container:

- container is just one
- Pod can have multiple containers


------------------------------------------------------------------------

liveness probe:
liveness probe --> when containers starts running

readiness probe:
readiness probe --> Whether the container is ready to serve the requests or not

Example: If we're running nginx container, but nginx server taking time to be up and running
If you do liveness probe, it'll fail.

First readiness probe, what it does is, it gives sometime to the container to becomme ready.

liveness probe is when container is ready it will check whether container is keep on running or not.


