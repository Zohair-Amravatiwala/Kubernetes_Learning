There are multiple ingress solutions available by the community to which helps to load balance and connect the outer world with the applications running inside the kubernetes cluster.

Ingress is a controller (Load balancer) as well as an API resource.

User > myapp.com (Domain Name) > DNS  >  Ingress load balancer(Controller) > Ingress API resource > Applications (ClusterIP, NodePort)

Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster

Ingress can be configured to do the following: 
- Give services externally reachable URLs.
- load balance the traffic
- terminate SSL/TLS 
- offers name based virtual hosting


Different ingress controllers
- nginx
- haproxy
- traefik
- kong
- contour

Commands
kubectl create ingress NAME --rule=host/path=service:port[,tls[=secret]]  [options]

Enable ingress controller in minikube
minikube addon enable ingress



LAB commands

```
k create deploy helloworld --image=gcr.io/google-samples/hello-app:2.0 -o yaml --dry-run=client > helloworld_deploy.yaml

kubectl apply -f helloworld_deploy.yaml

k expose deploy helloworld --port=8080 -o yaml --dry-run=client >> helloworld_deploy.yaml 

kubectl apply -f helloworld_deploy.yaml

kubetcl create ingress helloworld-ingress --rule="/=helloworld:8080" -o yaml --dry-run=client >> helloworld_deploy.yaml

kubectl apply -f helloworld_deploy.yaml

curl http://(minikube ip):80

For configuring DNS for mapping minikube ip to some custome URL edit hosts file
sudo vim /etc/hosts
```