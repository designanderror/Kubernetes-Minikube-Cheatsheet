## Configuring a Pod to use PersistentVolume for Storage

#### Before you begin, You need to have a Kubernetes cluster that has only one Node, and the kubectl command-line tool must be configured to communicate with your cluster. 


#### Open a shell to the single Node in your cluster
```
minikube ssh
```
### Creating a data mounting directory

```
# This assumes that your Node / current user uses "sudo" to run commands
# Check the installation process to add the user into sudo group
sudo mkdir /mnt/data
```

#### Creating an ```index.html``` page 
```
sudo sh -c "echo 'Hello from Kubernetes storage' > /mnt/data/index.html"
```

#### Check whether the ```index.html``` is created or not
```
cat /mnt/data/index.html
```

#### The output should be:
```
Hello from Kubernetes storage
```

#### Create a file named ```pv-volume.yaml``` anywhere and remember / note the path of the file. 

```
vi pv-volume.yaml
```
#### Copy paste the file details into this file and save it. 

#### Create the PersistentVolume
```
kubectl apply -f <file-path>
```
i.e
```
kubectl apply -f pv-volume.yaml
```
#### View information about the PersistentVolume
```
kubectl get pv task-pv-volume
```

#### The output shows that the PersistentVolume has a STATUS of Available. This means it has not yet been bound to a PersistentVolumeClaim.
```
NAME             CAPACITY   ACCESSMODES   RECLAIMPOLICY   STATUS      CLAIM     STORAGECLASS   REASON    AGE
task-pv-volume   10Gi       RWO           Retain          Available             manual                   4s
```


#### Create a file named ```pv-claim.yaml``` in the same folder as the previous file
```
vi pv-claim.yaml
```

#### Creating a Persistent Volume Claim
```
kubectl apply -f <file-path>
```
i.e
```
kubectl apply -f pv-claim.yaml
```
#### Look again at PV 
```
kubectl get pv task-pv-volume
```
### Now the output shows a ```STATUS``` of ```Bound```.
```
NAME             CAPACITY   ACCESSMODES   RECLAIMPOLICY   STATUS    CLAIM                   STORAGECLASS   REASON    AGE
task-pv-volume   10Gi       RWO           Retain          Bound     default/task-pv-claim   manual                   2m
```
#### Look at the PersistentVolumeClaim:
```
kubectl get pvc task-pv-claim
```
#### The output shows that the PersistentVolumeClaim is bound to your PersistentVolume, task-pv-volume.
```
NAME            STATUS    VOLUME           CAPACITY   ACCESSMODES   STORAGECLASS   AGE
task-pv-claim   Bound     task-pv-volume   10Gi       RWO           manual         30s
```

#### The next step is to create a Pod that uses your PersistentVolumeClaim as a volume.

#### Create a file ``` pv-pod.yaml```

```
vi pv-pod.yaml
```

#### Creating the Pod
```
kubectl apply -f <file-path>
```
i.e
```
kubectl apply -f pv-pod.yaml
```
#### Verify that the container in the Pod is running;
```
kubectl get pod task-pv-pod
```
#### Get a shell to the container running in your Pod:
```
kubectl exec -it task-pv-pod -- bash
```
#### In your shell, verify that nginx is serving the index.html file from the hostPath volume:

```
apt install curl
curl http://localhost/
```
#### The output shows the text that you wrote to the index.html file on the hostPath volume:
```
Hello from Kubernetes storage
```
#### If you see that message, you have successfully configured a Pod to use storage from a PersistentVolumeClaim

#### To exit from the shell just type ```exit```

## Clean Up

#### Delete the Pod, the PersistentVolumeClaim and the PersistentVolume use commands: 
```
kubectl delete pod task-pv-pod
kubectl delete pvc task-pv-claim
kubectl delete pv task-pv-volume
```