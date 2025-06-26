Goal:
Deploy two versions of a simple Nginx-based web app ("Blue" and "Green") using Kubernetes and switch traffic between them.

🛠️ Steps:
Created Blue & Green Versions:
Each had its own index.html and Dockerfile with a welcome message (e.g., "Welcome to the BLUE version").

Built Docker Images:
Created Kubernetes Deployments:

blue-deployment.yaml and green-deployment.yaml deployed 3 replicas each.
Images used: myapp:blue and myapp:green.

Created Kubernetes Service:

myapp-service.yaml of type NodePort, initially pointing to the blue deployment.

Accessed the Service:

Forwarded port:
kubectl port-forward svc/myapp-service 7080:80
Or accessed via EC2 public IP and NodePort.

Switched to Green Deployment:
Patched the service to redirect traffic to green:


Rollback to Blue (if needed):
kubectl patch svc myapp-service -p '{"spec":{"selector":{"app":"myapp","version":"blue"}}}'

Result:
successfully deployed and switched between blue and green versions using Kubernetes—mimicking a production-grade zero-downtime deployment model.
