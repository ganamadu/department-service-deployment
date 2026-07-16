# department-service-deployment

# Docker & Kubernetes Commands Cheat Sheet

## Maven

``` bash
mvn clean
mvn compile
mvn test
mvn clean package
mvn clean install
mvn clean package -DskipTests
mvn dependency:tree
```

## Docker

``` bash
docker build -t department-service:1.0 .
docker images
docker run -d --name department-service -p 8081:8081 department-service:1.0
docker ps
docker ps -a
docker logs department-service
docker logs -f department-service
docker exec -it department-service sh
docker stop department-service
docker start department-service
docker restart department-service
docker rm department-service
docker rmi department-service:1.0
docker login
docker tag department-service:1.0 <dockerhub-user>/emp-service:1.0
docker push <dockerhub-user>/emp-service:1.0
docker pull <dockerhub-user>/emp-service:1.0
```

## Minikube

``` bash
brew install minikube
minikube start --driver=docker
minikube status
minikube dashboard
minikube image load department-service:1.0
minikube service emp-service
minikube service emp-service --url
minikube stop
minikube delete
```

## kubectl

``` bash
kubectl cluster-info
kubectl get nodes
kubectl get ns
kubectl apply -f namespace.yaml
kubectl apply -f departmentdeployment.yaml
kubectl apply -f departmentservice.yaml
kubectl apply -f .
kubectl get all
kubectl get pods
kubectl get svc
kubectl get deployments
kubectl get rs
kubectl get endpoints
kubectl describe pod <pod-name>
kubectl describe deployment emp-service
kubectl describe svc emp-service
kubectl logs <pod-name>
kubectl logs -f <pod-name>
kubectl exec -it <pod-name> -- sh
kubectl port-forward svc/emp-service 8081:80
kubectl scale deployment emp-service --replicas=3
kubectl rollout status deployment emp-service
kubectl rollout restart deployment emp-service
kubectl rollout history deployment emp-service
kubectl rollout undo deployment emp-service
kubectl get events
kubectl delete -f .
```

## End-to-End Workflow

``` bash
mvn clean package
docker build -t department-service:1.0 .
docker login
docker tag department-service:1.0 <dockerhub-user>/emp-service:1.0
docker push <dockerhub-user>/emp-service:1.0
minikube start --driver=docker
kubectl apply -f .
kubectl get all
kubectl logs -f <pod-name>
kubectl port-forward svc/emp-service 8081:80
```
