# Kubernetes-Labs

## Lab#6

* NOTE: Deployment will take place in a namespace called **lab3**

### P1:Create basic resources

1. Create the specified Namespace

```
kubectl create namespace lab3
```
OR 
```
kubectl apply -f ns-lab3.yml 
```
2. Create a deployment nginx with 3 replicas

```
kubectl create deployment deployment-nginx --image=nginx --replicas=3 -n lab3 
```
OR
```
kubectl apply -f deployment-nginx.yml 
```


3. Expose the deployment on port 80

```
kubectl expose deployment deployment-nginx --type=NodePort --port=80 --target-port=80 -n lab3 
```
OR

```
kubectl apply -f service.yml 
```

![p1](https://user-images.githubusercontent.com/57557314/213478124-629648b8-f463-46b0-b6e4-e8b5ade17add.png)


---------------------------------------------


### P2:Create a CronJob for listing the EndPoints

1. Create a **serviceaccounts** cronjob-sa

```
kubectl create sa cronj-sa -n lab3 
```
OR

```
kubectl apply -f  sa.yml
```
 

2. Create a Role that allows listing all the services and endpoints 

```
kubectl create role services-endpoints-lister --verb=list,get --resource=services,endpoints -n lab3 
```
```
kubectl apply -f role.yml
```

3. Link the Role with the created SA 

```
kubectl create rolebinding service-endpoint --role=services-endpoints-lister --serviceaccount=lab3:cronj-sa -n lab3

```

```
kubectl apply -f rolebinding.yml 
```


4. Create a CronJob that lists the endpoints in that namespace every minute and paste the output for the first pod created

```
kubectl create cronjob endpoint-lister --schedule="* * * * *" --namespace=lab3 --image=bitnami/kubectl -- kubectl get endpoints 
```
```
kubectl apply -f cronjob.yml 
```


5. After listing try to delete the 3 nginx pods ? again try to view the logs for the newly created pod for that cronJob what do you think happened ? 

```
kubectl delete pods <pods-names> -n lab3

```

```
kubectl logs <pod-name> -n lab3 
```
-----------------------------------------------------------

![kk](https://user-images.githubusercontent.com/57557314/213480356-88837e6e-5344-4601-b80c-b0504550f0ad.png)

