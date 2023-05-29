# Encoding secrets in Base64 format

# In realtime these kind of secrets not be considered! It can be decoded easily

# Encoding:
echo -n mahesh | base64
bWFoZXNo
echo -n mahesh786 | base64
bWFoZXNoNzg2

# Decoding:

echo -n bWFoZXNo | base64 --decode
mahesh

echo -n bWFoZXNoNzg2 | base64 --decode
mahesh786



[ec2-user@ip-172-31-36-191 Secrets]$ ll
total 8
-rw-rw-r-- 1 ec2-user ec2-user 122 May  2 08:29 01-secret.yaml
-rw-rw-r-- 1 ec2-user ec2-user 112 May  2 08:29 Encodee-Secrets.md
[ec2-user@ip-172-31-36-191 Secrets]$ kubectl apply -f 01-secret.yaml
secret/mysecret created
[ec2-user@ip-172-31-36-191 Secrets]$ kubectl describe secret mysecret
Name:         mysecret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
password:  9 bytes
username:  6 bytes



Example:
-------

Important Points: 
- Configmap is for non-confidential information
- Secret is for confidential information.


Reference for kubernetes secrets:
https://www.mirantis.com/cloud-native-concepts/getting-started-with-kubernetes/what-are-kubernetes-secrets/
--------------------------------------------------
1. Generate, Username & Password in encode format.

[ec2-user@ip-172-31-41-59 Pod]$ echo -n Mahesh | base64
TWFoZXNo

[ec2-user@ip-172-31-41-59 Pod]$ echo -n mahesh999 | base64
bWFoZXNoOTk5


2. Place it in yaml file

secret.yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque  
data:
  username: TWFoZXNo 
  password: bWFoZXNoOTk5


3. Data cannnot be exposed! Only the size can be visible.

[ec2-user@ip-172-31-41-59 Secrets]$ kubectl describe secret mysecret
Name:         mysecret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
password:  9 bytes
username:  6 bytes




4. Create pod and use mysecret reference:

[ec2-user@ip-172-31-36-191 2-Pod]$ cat 10-secret-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
spec:
  containers:
  - name: nginx
    image: nginx
    env:
      - name: USERNAME
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: username
      - name: PASSWORD
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: password
#  restartPolicy: Never


[ec2-user@ip-172-31-36-191 2-Pod]$ kubectl apply -f 10-secret-pod.yaml
pod/secret-pod created

[ec2-user@ip-172-31-36-191 2-Pod]$ kubectl exec -it secret-pod -- bash


Note: At runtime, kubernetes willr refer that secrets and it'll decode automatically for us and make it available for the application.

root@secret-pod:/# env
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_SERVICE_PORT=443
HOSTNAME=secret-pod
PWD=/
PKG_RELEASE=1~bullseye
HOME=/root
USERNAME=mahesh
KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
PASSWORD=mahesh786
NJS_VERSION=0.7.11
TERM=xterm
SHLVL=1
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_ADDR=10.100.0.1
KUBERNETES_SERVICE_HOST=10.100.0.1
KUBERNETES_PORT=tcp://10.100.0.1:443
KUBERNETES_PORT_443_TCP_PORT=443
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
NGINX_VERSION=1.23.4
_=/usr/bin/env


====================================================================
