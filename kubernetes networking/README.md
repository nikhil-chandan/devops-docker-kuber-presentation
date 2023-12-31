# Kubernetes Networking

## Networking

- Pod-internal through localhost
- Outside world communication is possible with a service of type LoadBalancer
- Cluster-internal communication is possible with a service of type ClusterIP
  - Auto generated Cluster internal IP Address
  - Auto generated Cluster internal domain names
  - Auto generated Environment Variables


docker build -t nikhilchandan/kub-demo-users .
docker push nikhilchandan/kub-demo-users
kubectl apply -f=users-deployment.yaml
kubectl apply -f=users-service.yaml
kubectl get services
minikube service users-service
http://127.0.0.1:49504/login post {"email" : "niks@gmail.com", "password": "test123a"}
http://127.0.0.1:49504/signup {"email" : "niks@gmail.com", "password": "test123a"}


we do not want to expose this to public so used clusterIP
k8 gives automatic env variables eg. AUTH_SERVICE_SERVICE_HOST , USER_SERVICE_SERVICE_HOST
docker build -t nikhilchandan/kub-demo-auth:latest .
docker push nikhilchandan/kub-demo-auth
kubectl apply -f=auth-deployment.yaml
kubectl apply -f=auth-service.yaml
kubectl get services
minikube service auth-service

docker build -t nikhilchandan/kub-demo-users .
docker push nikhilchandan/kub-demo-users
kubectl apply -f=users-deployment.yaml
kubectl apply -f=users-service.yaml

kubectl get namespaces
autogenerated domain name services  eg. auth-service.default (AUTH_ADDRESS)

docker build -t nikhilchandan/kub-demo-users .
docker push nikhilchandan/kub-demo-users
kubectl apply -f=users-deployment.yaml
kubectl apply -f=users-service.yaml
http://127.0.0.1:49504/tasks post header Authorization:Bearer abc
http://127.0.0.1:49504/tasks getcall


docker build -t nikhilchandan/kub-demo-frontend .
docker push nikhilchandan/kub-demo-frontend
kubectl apply -f=frontend-deployment.yaml
kubectl apply -f=frontend-service.yaml
minikube service frontend-service


docker build -t nikhilchandan/kub-demo-tasks .
docker push nikhilchandan/kub-demo-tasks
kubectl apply -f=tasks-deployment.yaml
kubectl apply -f=tasks-service.yaml
minikube service tasks-service
