# Kubernetes-Labs

## Lab2(RS)

1. Create a ReplicaSet using the below yaml

    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
    name: new-replica-set
    namespace: default
    spec:
    replicas: 4
    selector:
        matchLabels:
        name: busybox-pod
    template:
        metadata:
        labels:
            name: busybox-pod
        spec:
        containers:
        - command:
            - sh
            - -c
            - echo Hello Kubernetes! && sleep 3600
            image: busybox777
            imagePullPolicy: Always
            name: busybox-container

```bash
toush busybox.yaml
```
```
vi busybox.yaml
```

```
k apply -f ./busybox.yaml

```


2. How many PODs are DESIRED in the new-replica-set?

```
k get pod 
```

there are 4 pods (replicas: 4 in ymal file) 


3. What is the image used to create the pods in the new-replica-set?

there is two way 
 - frist from yaml file (mage: busybox777)
 - second (k discribe pods podName )


4. How many PODs are READY in the new-replica-set?

there are for pods

5. Why do you think the PODs are not ready?

Answer: as there no image with name busybox777



6. Delete any one of the 4 PODs. 

```bash
k delete pod podName
```



7. How many pods now

also 4


8. Why are there still 4 PODs, even after you deleted one?

as there is ReplicaSet (replicaset ensures that a specified number of pod replicas are running at any given time)



9. Create a ReplicaSet using the below yaml


    There is an issue with the file, so try to fix it.

    apiVersion: v1
    kind: ReplicaSet
    metadata:
    name: replicaset-1
    spec:
    replicas: 2
    selector:
        matchLabels:
        tier: frontend
    template:
        metadata:
        labels:
            tier: frontend
        spec:
        containers:
        - name: nginx
            image: nginx

```bash
toush replica.yaml 
k apply -f ./replica.yaml
```
