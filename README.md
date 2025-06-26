# Blue-Green-Deployments-in-Kubernetes
Switching the Traffic from Blue deployment to green deployment or vise-versa


<<<<< commands that have been used >>>>>>

docker build -t myapp:blue ./blue
docker build -t myapp:green ./green
kubectl apply -f blue-deployment.yaml  ###  applying manifest###
kubectl apply -f green-deployment.yaml
kubectl apply -f service.yaml


kubectl get pods -l app=myapp       ###Check pods and services###
kubectl get svc myapp-service

kubectl patch svc myapp-service -p '{"spec":{"selector":{"app":"myapp","version":"green"}}}'   ##Switch traffic to green deployment (blue-green switch)###
kubectl patch svc myapp-service -p '{"spec":{"selector":{"app":"myapp","version":"blue"}}}'    ##Roll back traffic to blue deployment
kubectl port-forward svc/myapp-service 7080:80                                                 ##Port-forward to test locally


