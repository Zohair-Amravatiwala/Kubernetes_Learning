# Pod local Volume storage 
- not portable
kubectl explain pod.spec.volumes | less

# Persistent Volumes 
- It is an independent resource that connects to an external storage.

# Persistent Volume Claims
- A PVC requests access to the PV according to the specific properties like accessMode, size etc.

# Storage Class
- Kubernetes storage class allows for automatic provisioning of PVs when a PVC request for storage comes in.
- StorageClass must be backed by a storage provisioner which takes care of the volume configuration.