# Deploy mongodb on Kubernetes environment


kubectl create -f mongo-deployment.yaml

once you deploy mongodb, please follow the below steps.

1. create user account
Type in the MongoDB query below to create the new administrator user:
#kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
mongo-controller-r8952         1/1     Running   0          21h

#kubectl exec -it mongo-controller-r8952 /bin/bash
#mongo

db.createUser(
  {
    user: "admin",
    pwd: "admin123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)

quit


2. modify mongo.conf file - allow all IP to access mongodb from remote machine (depends on your requirement)
#kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
mongo-controller-r8952         1/1     Running   0          21h

#kubectl exec -it mongo-controller-r8952 /bin/bash
#vim /etc/mongod.conf.orig 
net:
  port: 27017
  bindIp: 0.0.0.0

save and exit from pod
