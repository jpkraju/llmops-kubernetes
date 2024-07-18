# Docker Commands

```
--get all images / containers
docker images
docker ps -a

-- create docker image with version (:v1)
docker build -t chatgpt-k8s:v1 .

--run docker on a port
docker run -d -p 8080:80 chatgpt-k8s:v1

--run docker with env variables
docker run -d -e OPENAI_API=<open ai id> -p 8080:80 chatgpt-k8s:v2

--access container bash
docker exec -it <container-id> /bin/bash

-- rename or add username before image name
docker tag chatgpt-k8s:v1 jpkraju/chatgpt-k8s:v1

--push to docker registry
docker push jpkraju/chatgpt-k8s:v1

--pull from docker registry
docker pull jpkraju/chatgpt-k8s:v1

docker stop <container_id>
docker rm <container-id>

docker rmi <image-id> -f

```

## Kubernetes commands
```
-- look 
kubectl api-resources

--pod objects
kubectl get pods
kubectl apply -f pod.yaml
kubectl describe pod myapp

-- logs of pod
kubectl logs <pod-id>

--service object
kubectl apply -f svc-local.yaml
kubectl get svc
kubectl describe svc mysvc

-- delete all pods, svc, deploy objects
kubectl delete pods --all / <pod-id>
kubectl delete svc --all / <svc-id>
kubectl delete deploy --all / <deploy-id>
kubectl delete secrets --all / <secret-id>

--create namespace if provided in deploy.yaml 
kubectl create namespace rk-namespace

--deployment objects
kubectl get deployments
kubectl apply -f deploy.yaml
kubectl describe deployments

--scale down pods to ZERO and then delete
kubectl scale deploy -n <namespace> --replicas=0 --all
kubectl scale deploy --replicas=0 chatgpt-deploy

--rollout 
kubectl rollout status deployment

--config map
kubectl create configmap app-config --from-literal=DATABASE_URL="mysql://user:password@mysql-server:3306/db_name"
kubectl describe cm app-config 

-- access the pod/docker enviromnet
kubectl exec -it app-pod -- /bin/bash

--secret object
kubectl get secrets
kubectl create secret generic openai-secret --from-literal=API_KEY=<api-key>
kubectl create secret generic db-secret --from-literal=DB_PASSWORD=password123

-- access the pod/docker enviromnet
kubectl exec -it db-pod -- /bin/bash

```

# Deployment Object
self healing
scaling
rolling updates

# Deployment Controller
Process which runs on the Control Plane that monitors the cluster making use all the deployment object are running as per the specification