# Demo K8S

```cosole
1 - ConfigMap -> MongoDB Endpoint
2 - Secret -> MongoDB User & Pwd
3 - Deployment & Service -> MongoDB application with *internal* service
4 - Deployment & Service -> WebApp with *external* Service
```

```console
Request (port: 27017) -> MongoService (targetPort: 27017) -> Pod (containerPod: 27017)
```

```console
kubectl get pod # to list what we have

# First need to deploy the configuration service
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo-secret.yaml

# Deploy DB
kubectl apply -f mongo.yaml
# New needs to show: deployment created and service created

# Deploy webapp
kubectl apply -f webapp.yaml

# Show all the components created in the cluster
kubectl get all

kubectl get configmap
kubectl get secret

kubectl describe service webapp-service

# Get status of the POD
kubectl describe pod NAME_OF_THE_POD

kubectl logs NAME_OF_THE_POD_OR_DEPLOYMENT
kubectl logs NAME_OF_THE_POD_OR_DEPLOYMENT -f  # to stream the log
kubectl logs NAME_OF_THE_POD_OR_DEPLOYMENT -n NAMESPACE_NAME  # optionally if namespace isnot default

# Accessing WebApp from the browser
# Check the services
kubectl get svc

# NodePort is accessible on each Workers Node's IP address
# We only have 1 machine and using minikube, so we get the minikube ip
minikube ip
# or...
kubectl get node -o wide # show more columns including ip

# To access on browser we need to inform the minikube IP + NodePort we informed to the webapp service.
# Example:
kubectl get services webapp-service -o wide
# will show this:
# NAME             TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE   SELECTOR
# webapp-service   NodePort   10.104.180.246   <none>        3003:30100/TCP   42s   app=webapp-pod
# The NodePort we configured is the 30100

# IF SOMETHING WENT WRONG:
kubectl get pods # check if "Status" is Pending

# If pending status check "Events" of the describe result:
kubectl describe pod POD_NAME_OF_THE_SERVICE

# or...
kubectl get events

```
