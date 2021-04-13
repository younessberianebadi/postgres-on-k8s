# Postgres on K8s demo
![Scheme](/images/scheme.png)
This is a simple demo for deploying a **postgressql** databse with two php web applications on **minikube**.
First start by creating the configmap and the secret:
```
kubectl apply -f postgres-configmap.yaml
kubectl apply -f postgres-secret.yaml
```
Then create the postgres deployment and the postgres persistant volume and persistant volume claim:
```
kubectl apply -f postgres-storage.yaml
kubectl apply -f postgres-deployment.yaml
```
Create the postgres service:
```
kubectl apply -f postgres-service.yaml
```
Finally deploy the two applications and their LoadBalancer services:
```
kubectl apply -f phpadd-deployment.yaml
kubectl apply -f phpadd-service.yaml
kubectl apply -f phpapp-deployment.yaml
kubectl apply -f phpapp-service.yaml
```
I would after that login the postgres pod using:
```
kubectl exec -it <postgres-pod-name> bash
```
and creating the database and the table using the following commands:
```
psql -h localhost -U postgesadmin -p 5432 postgresdb
```
```sql
CREATE DATABASE digiwise;
```
```
\c digiwise
```
```sql
CREATE TABLE people(
fullname text,
birthplace text);
```
That should work!
:tada: