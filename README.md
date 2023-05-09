# Demo K8S

1 - ConfigMap -> MongoDB Endpoint
2 - Secret -> MongoDB User & Pwd
3 - Deployment & Service -> MongoDB application with *internal* service
4 - Deployment & Service -> WebApp with *external* Service

```console
Request (port: 27017) -> MongoService (targetPort: 27017) -> Pod (containerPod: 27017)
```

