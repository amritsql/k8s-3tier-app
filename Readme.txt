In this example, we're creating a ServiceMonitor resource with the name vote-monitor that selects pods with the app: vote label. We're also specifying an endpoints section that specifies the port and path for the Prometheus metrics endpoint.

## minikube setup ##
1) Enable ingress
minikube addons enable ingress
2) Enable redis to deploy on node
kubectl label nodes minikube cache=true
3) enable vote to deploy on node
kubectl label nodes minikube app=vote
4) enable autoscaling
minikube addons enable metrics-server


## vote ##
vote-deployment.yaml --- creates required deployment, hpa(scaling based on memory and cpu), defines request and limit for resources, applies label and selectors --
vote-service.yaml -- creates required service --

## result ##
result-deployment.yaml --- creates required deployment, hpa(scaling based on memory and cpu), defines request and limit for resources, applies label and selectors --
result-service.yaml -- creates required service --

## db ##
db-deployment.yaml --- creates required deployment, applies label and selectors, creates persistent volume and stores data --
db-service.yaml -- creates required service  --

## redis ##
redis-deployment.yaml --- creates required deployment, hpa(scaling based on memory and cpu), defines request and limit for resources, applies label and selectors creates persistent volume and stores data --
redis-service.yaml -- creates required service --

## set /etc/hosts ## This is required as we do not own the domain hence we will make the changes locally on our system
192.168.64.2 example.com

## ingress ##
This is used to expose the application to the world
browser https://example.com
annotations section helps to force redirect from http to https
rules section helps to map host to service

## how to access the application result ##
minikube service result

![Application image](./images/application.png)
![Prometheus image](./images/prometheus.png)
