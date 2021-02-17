#### To start the minikube
```
minikube start 
```

#### To view config details
```
kubectl config view
```

#### To see cluster information
```
kubectl cluster-info
```

#### To get the details of nodes
```
kubectl get nodes
```

#### To see list of all minikube pods
```
kubectl get pods
```
OR 
```
kubectl get po
```

#### To check the status of minikube
```
minikube status
```

#### To stop running the single node cluster type:
```
minikube stop
```

#### To delete the single node cluster:
```
minikube delete
```

#### To find namespace
```
kubectl get ns
```

#### get the pods from a name space
```
kubectl get pods -n <namespace name>
```

#### To check in which nodes the pods are running
```
kubectl get pods -n <namespace name> -o wide
```

#### To create a namespace
```
kubectl create ns <namespace name>
```

#### To navigate into another namespace
```
kubectl config set-context --current --namespace=<insert-namespace-name-here>
```

#### To see the details of a namespace
```
kubectl describe ns <namespace name>
```

#### To see the pods which are running from another namespaces
```
kubectl get pods -n <namespace name>
```

#### To see the details of a pod
```
kubectl describe pods <pod name> -n <namespace name>
```
OR 
```
kubectl describe pods <pod name> -n <namespace name>|more
```

### deploy any application 
####you can replace nginx-test with the name that you want to get
```
kubectl run nginx-test --image=nginx --port=443 
```

#### To watch what is going on 
```
watch kubectl get pods
```

#### to see the pods which are running in namespaces
```
kubectl get pods nginx-test
```

#### Jump or execute the pod
```
kubectl exec -it <pod name > -- bash
```

#### To get replicas count or set
```
kubectl get replicaset
```

#### Deployment of yaml file
##### -f stands for file 
```
kubectl apply -f deployment.yaml    
kubectl apply -f service.yaml
kubectl get deployment
```

#### Scaling up the pods
```
kubectl scale --current-replicas=2 --replicas=3 deployment/<app-name>
```

#### Scaling down
```
kubectl scale --current-replicas=5 --replicas=3 deployment/<app-name>
```

#### Delete pods
```
kubectl delete pod <pod name>
```

                                                                                                                                                                                                             










