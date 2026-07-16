# Kubernetes Learning Guide

## 1. Namespace

Purpose: Logically isolate Kubernetes resources.

``` yaml
apiVersion: v1
kind: Namespace
metadata:
  name: department-dev
```

Commands:

``` bash
kubectl apply -f namespace.yaml
kubectl get ns
kubectl get all -n department-dev
```

------------------------------------------------------------------------

## 2. Deployment

Purpose: Manages Pods and ReplicaSets.

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: emp-service
  namespace: department-dev
spec:
  replicas: 2
```

Commands:

``` bash
kubectl apply -f deployment.yaml
kubectl get deployments -n department-dev
kubectl rollout status deployment emp-service -n department-dev
kubectl rollout restart deployment emp-service -n department-dev
kubectl scale deployment emp-service --replicas=3 -n department-dev
```

------------------------------------------------------------------------

## 3. Service

Purpose: Exposes Pods.

Types: - ClusterIP - NodePort - LoadBalancer - ExternalName

Commands:

``` bash
kubectl apply -f service.yaml
kubectl get svc -n department-dev
kubectl describe svc emp-service -n department-dev
kubectl port-forward svc/emp-service 8081:80 -n department-dev
```

------------------------------------------------------------------------

## 4. ConfigMap

Purpose: Store non-sensitive configuration.

Commands:

``` bash
kubectl apply -f configmap.yaml
kubectl get configmap -n department-dev
kubectl describe configmap department-config -n department-dev
```

------------------------------------------------------------------------

## 5. Secret

Purpose: Store sensitive configuration.

Commands:

``` bash
kubectl apply -f secret.yaml
kubectl get secrets -n department-dev
kubectl describe secret department-secret -n department-dev
```

------------------------------------------------------------------------

## 6. Debugging

``` bash
kubectl get all -A
kubectl get pods -o wide
kubectl describe pod <pod-name> -n department-dev
kubectl logs <pod-name> -n department-dev
kubectl logs -f <pod-name> -n department-dev
kubectl exec -it <pod-name> -n department-dev -- sh
kubectl get events -n department-dev
```

------------------------------------------------------------------------

## 7. Resource Flow

Namespace ↓ Deployment ↓ ReplicaSet ↓ Pods ↓ Service ↓ Client

------------------------------------------------------------------------

## 8. Next Topics

-   Namespace ✅
-   Deployment ✅
-   Service ✅
-   ConfigMap ✅
-   Secret ✅
-   NodePort
-   Ingress
-   HPA
-   Helm
