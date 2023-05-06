Check if the current user has access to perform a task
kubectl auth can-i get pods

check for another user
kubectl auth can-i get pods --as bob@example.com


# Service Account
- It is an identity created within cluster to perform some tasks.
- The Role defines access permissions to API resources.
- The role binding connects the service account to a specific role.

# Commands
1) Create  Service Account
kubectl create serviceaccount / sa mysa
- while creating the service accounts a secret is automatically created to have the service account connect to the API
- The secret is mounted in pods using the service accounts
- After creating the SA, RBAC must be configured.
2) Assign service account to a pod or deployment
kubectl set serviceaccount deploy <deployment_name> <service_account_name>