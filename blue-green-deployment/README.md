# Blue-Green Deployment (Kubernetes + Minikube)

This project demonstrates a zero-downtime deployment using the Blue-Green strategy.

## 📦 Folder Structure
- `blue/`: Contains Dockerfile and index.html for blue version.
- `green/`: Same for green version.
- YAML files define deployments and service.

## 🚀 Deployment Steps

1. Enable Docker inside Minikube:
   ```bash
   eval $(minikube docker-env)
   ```

2. Build Docker images:
   ```bash
   docker build -t myapp:blue ./blue
   docker build -t myapp:green ./green
   ```

3. Apply deployments and service:
   ```bash
   kubectl apply -f blue-deployment.yaml
   kubectl apply -f green-deployment.yaml
   kubectl apply -f myapp-service.yaml
   ```

4. Access service:
   ```bash
   kubectl port-forward svc/myapp-service 7080:80
   curl http://localhost:7080
   ```

5. Switch traffic to green:
   ```bash
   kubectl patch svc myapp-service -p '{"spec":{"selector":{"app":"myapp","version":"green"}}}'
   ```

6. Rollback to blue:
   ```bash
   kubectl patch svc myapp-service -p '{"spec":{"selector":{"app":"myapp","version":"blue"}}}'
   ```

## ✅ Outcome
You can seamlessly toggle between blue and green versions using the service patching technique.
