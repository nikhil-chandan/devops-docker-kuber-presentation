# minikube commands
minikube status
minikube start --driver=virtualbox or minikube start --driver=docker or minikube start --driver=hyperv
minikube dashboard

# Imperative approach ( kub-first-app )
docker build -t kub-first-app .
docker images
docker tag kub-first-app nikhilchandan/kub-first-app 
docker push nikhilchandan/kub-first-app 
kubectl create deployment first-app --image=nikhilchandan/kub-first-app 

kubectl expose deployment first-app --type=ClusterIP --port=8080 (default type inside cluster)
kubectl expose deployment first-app --type=NodePort --port=8080 (should be exposed by IP of worker node)
kubectl expose deployment first-app --type=LoadBalancer --port=8080  (distribute trafic, supports aws, minikube etc but not all)
kubectl get deployments
kubectl get services
kubectl get pods
minikube service first-app 
kubectl scale deployment/first-app --replicas=3 ( create 3 pods)

docker build -t nikhilchandan/kub-first-app:3 . (when changes are made use it always, always user version or chnages are not recognised)
kubectl get deployments
docker push nikhilchandan/kub-first-app:3
kubectl set image deployments/first-app kub-first-app=nikhilchandan/kub-first-app:3
kubectl rollout status deployment/first-app 
minikube service first-app 

kubectl rollout undo deployment/first-app (will undo latest deployment)
kubectl rollout history deployment/first-app
kubectl rollout history deployment/first-app --revision=1
kubectl rollout undo deployment/first-app --to-revision=1 ( undo deployment )
kubectl delete service first-app
kubectl delete deployment first-app

# Declarative approach 
kubectl apply -f=deployment.yaml 
kubectl get deployments
kubectl get pods
kubectl apply -f=service.yaml 
kubectl get services
minikube service backend

to make changes rerun command
kubectl apply -f=deployment.yaml 

kubectl delete -f=deployment.yaml,service.yaml 
kubectl delete -f=deployment.yaml -f=service.yaml 

kubectl apply -f=master-deployment.yaml
minikube service backend
#kubectl delete deployments,services -l group=example

# check health of pods by liveliness probe
livenessProbe:
httpGet:
path: /
port: 8080
periodSeconds: 10
initialDelaySeconds: 5

# when ever change is found in image to pull new image
imagePullPolicy: Always







