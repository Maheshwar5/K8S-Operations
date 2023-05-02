# Encoding secrets in Base64 format
echo -n mahesh | base64
bWFoZXNo
echo -n mahesh786 | base64
bWFoZXNoNzg2



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




