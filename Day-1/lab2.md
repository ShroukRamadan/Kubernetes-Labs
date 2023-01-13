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

![l2-1](https://user-images.githubusercontent.com/57557314/212433359-ea5d3772-3ee5-4e5d-b282-96ddc0f8ce8a.png)


2. How many PODs are DESIRED in the new-replica-set?

```
k get pod 
```
![2](https://user-images.githubusercontent.com/57557314/212434183-593254ca-f369-463d-846f-128664b080e1.png)

there are 4 pods (replicas: 4 in ymal file) 


3. What is the image used to create the pods in the new-replica-set?

there is three ways 
 - frist from yaml file (mage: busybox777)
 - second (k discribe pods podName )

4. How many PODs are READY in the new-replica-set?

there are 4 pods

5. Why do you think the PODs are not ready?

Answer: as there no image with name busybox777



6. Delete any one of the 4 PODs. 

```bash
k delete pod podName
```
![l2-6](https://user-images.githubusercontent.com/57557314/212433760-20b164a7-488d-4b3d-a135-f853ff35aba9.png)



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
toush nginx.yaml 
k apply -f ./replica.yaml
```
