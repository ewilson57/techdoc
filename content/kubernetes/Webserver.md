---
title: "nginx webserver demo"
date: 2019-10-05T19:39:36-04:00
draft: true
---

## Start a local kubernetes cluster (run as root/Administrator)

````bash
minikube start
````

## Stop a local kubernetes cluster

````bash
minikube stop
````

## Get kubernetes cluster status

````bash
minikube status
````

> Sample output:

````text
minikube: Running  
cluster: Running  
kubectl: Correctly Configured: pointing to minikube-vm at 10.9.21.103  
````

## Open/display the kubernetes dashboard URL for your local cluster

````bash
minikube dashboard
````

## Create a new deployment

nginx-deployment.yaml

````yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
````

````bash
kubectl create -f .\nginx-deployment.yaml
````

> Sample output:

````text
deployment.apps/nginx-deployment created
````

## Create a service

nginx-service.yaml

````yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  labels:
    run: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    protocol: TCP
  selector:
    app: nginx
````

````bash
kubectl create service -f .\nginx-service.yaml
````

> Sample output:

````text
service/nginx-service created
````

## Get information on deployments

````bash
kubectl get deployments
````

> Sample output:

````text
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   3/3     3            3           20m
````

## Get information on replicasets

````bash
kubectl get replicaset
````

Sample output:

````text
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-54f57cf6bf   3         3         3       21m
````

## Get information on pods

````bash
kubectl get pods
````

> Sample output:

````text
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-54f57cf6bf-9xhhz   1/1     Running   0          22m
nginx-deployment-54f57cf6bf-f6c5z   1/1     Running   0          22m
nginx-deployment-54f57cf6bf-hhmgb   1/1     Running   0          22m
````

## Get information on services

````bash
kubectl get service
````

> Sample output:

````text
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP        25h
nginx-service   NodePort    10.97.222.168   <none>        80:31928/TCP   17m
````

## Get information on a service

````bash
kubectl describe service nginx-service
````

> Sample output:

````text
Name:                     nginx-service
Namespace:                default
Labels:                   run=nginx-service
Annotations:              <none>
Selector:                 app=nginx
Type:                     NodePort
IP:                       10.97.222.168
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  31928/TCP
Endpoints:                172.17.0.6:80,172.17.0.7:80,172.17.0.8:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>  
````

## Get IP address of cluster

````bash
minikube ip
````

> Sample output:

````text
192.168.134.204
````

## Browse to \<minikube ip>:\<web service port>

````text
http://192.168.134.204:31928/
````
