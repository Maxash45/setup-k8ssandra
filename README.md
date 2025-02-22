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

`kubectl create ns k8ssandra-operator`
