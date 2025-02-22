# setup-k8ssandra
## Migration of Cassandra to K8ssandra with MinIO, Medusa Utility, and Backup Using CronJob with Retention Policy.

This document provides a comprehensive guide to migrate Cassandra to K8ssandra, implement a backup strategy using Medusa and MinIO, automate backups with CronJobs, and enforce a retention policy for effective data management.

### Prerequisites
●	A Kubernetes cluster (MicroK8s)
●	Sufficient compute and storage resources in the cluster to handle the Cassandra workload.
●	MinIO instance for object storage.
●	Network connectivity between K8ssandra pods and MinIO.
●	K8ssandra Helm chart for deploying Cassandra on Kubernetes.
●	Medusa for backup and restore management.
●	MinIO client (mc) for interacting with MinIO.
●	Kubectl for managing Kubernetes resources.
●	Helm for deploying Helm charts.
●	Cert manager.

### STEPS TO SET UP THE MINIO:
> Create new namespace e.g k8ssandra-operator
> Create new directory  e.g setupk8ssandra

```
kubectl create ns minio
mkdir setupk8ssandra
cd setupk8ssandra
```

now install minio first from `minio.yaml`

```
vi minio.yaml
```
```
kubectl apply -f minio.yaml -n minio
```
Check pod and service is up and running

```
kubectl get pods -n minio
kubectl get svc -n minio
```
To access minio or 
```
kubectl port-forward svc/minio 9090:9090 --address=0.0.0.0 -n minio
```
```
% http://<IPaddress:nodeport> /
```
> Create Bucket on minio e.g ifrm-cassandra-bucket and create new  access key // this is my bucket name

> Execute into the  pod  by using below command
```
%kubectl exec -it minio-bd46f5fdd-2r5rr  -- bash
```
> Setting Alias into minio pod and use your own access key and secret key.
```
mc alias set my minio http://<minio-service>:9000 <access-key> <secret-key>
mc alias list
```

### Minio setup done at this stage

