# ex-yaml-k8b-superset

## About
This project provides a simple example of deploying Apache Superset (using the amancevice/superset image) and Redis to a local Kubernetes cluster (Minikube) using YAML manifests. It demonstrates resource configuration, persistent storage, and service exposure in a development environment.

You can use this as a template for learning, testing, or as a starting point for your own Superset deployments in Kubernetes.

## Quick Start

### 1. Start Minikube with CPU and Memory Limits
```
minikube start --cpus=2 --memory=4096
```

### 2. Apply Kubernetes YAML Manifests
```
kubectl apply -f sqlite/superset_k8s_deployment.yaml
```

### 3. Expose Superset Service in Minikube
To access the Superset web UI, run:
```
minikube service superset -n superset
```
This will open the Superset UI in your browser. If it does not, use the provided URL.

Alternatively, you can use port-forward:
```
kubectl port-forward service/superset 8088:8088 -n superset
```
Then open http://localhost:8088 in your browser.

### 4. Delete All Resources
To remove all deployed resources:
```
kubectl delete -f sqlite/superset_k8s_deployment.yaml
```
Or to delete the entire namespace (removes everything in it):
```
kubectl delete namespace superset
```

## Notes
- Make sure you have enough free memory on your system for Minikube and Superset pods.
- If Superset pod fails with OOMKilled, increase memory limits in the YAML and restart the pod.
- Default Superset credentials: admin / admin (unless changed in the image).
- To check pod status: `kubectl get pods -n superset`
- To view logs: `kubectl logs <pod-name> -n superset`
- If you need to reset everything, delete the namespace and re-apply the YAML.
