# Kubernetes-Labs

## Lab1#(for pods)

1. How many pods exist on the system?

```bash
# k is alias from kubectl
k get pods
```



2. How many Nodes exist on the system?

```bash

k get nodes
```

3. Create a new pod with the nginx image.
    Image name: nginx

```bash
# create and run pod
k run nginx --image=nginx  -oyaml > nginx.yml 
```


4. Which nodes are these pods placed on?

```bash
# to view all resources
k discribe pods nginx 
```

5. Create pod from the below yaml using kubectl apply command

    apiVersion: v1
    kind: Pod
    metadata:
    name: webapp
    namespace: default
    spec:
    containers:
    - image: nginx
        imagePullPolicy: Always
        name: nginx
    - image: agentx
        imagePullPolicy: Always
        name: agentx

```bash
# apply: to create pod using yml file
k apply -f nginx2.yml
```


6. How many containers are part of the pod webapp

```bash
k get pods
```
 
Answer : 2

7. What images are used in the new webapp pod?

```bash
k discribe pods nginx 
```
nginx
agentx

8. What is the state of the container agentx in the pod webapp



9. Why do you think the container agentx in pod webapp is in error?


10. Delete the webapp Pod.

```bash
k delete pod webapp
```

11. Create a new pod with the name redis and with the image redis123.
    • Name: redis
    • Image Name: redis123

```
k run pod redis --image=redis123
```

12. Now change the image on this pod to redis.
Once done, the pod should be in a running state.


k edit pod redis


13. Create a pod called my-pod of image nginx:alpine

```bash
k run pod my-pod --image=nginx:alpine
```

14. Delete the pod called my-pod

```bash
k delete pod my-pod
```