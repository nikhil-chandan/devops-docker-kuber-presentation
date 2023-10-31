docker build -t nikhilchandan/kub-data-demo:1 .
docker push nikhilchandan/kub-data-demo:1
kubectl apply -f=deployment.yaml
kubectl apply -f=host-pv.yaml
kubectl apply -f=host-pvc.yaml
kubectl apply -f=environment.yaml
kubectl apply -f=service.yaml
kubectl get pods
kubectl get deployments
kubectl get services
minikube service story-service
Get localhost/story
Post localhost/story {"text" : "k8 demo"} http://127.0.0.1:62427/story

kubectl get sc ( manage volumes and storage )
kubectl get pv
kubectl get pvc


# A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.

# A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany or ReadWriteMany, see AccessModes).

