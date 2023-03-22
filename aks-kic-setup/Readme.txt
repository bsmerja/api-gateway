git clone https://github.com/nginxinc/kubernetes-ingress.git --branch v2.4.2
cd kubernetes-ingress/deployments

Create a namespace and a service account for the Ingress Controller:

kubectl apply -f common/ns-and-sa.yaml

Create a cluster role and cluster role binding for the service account:

kubectl apply -f rbac/rbac.yaml

Create a secret with a TLS certificate and a key for the default server in NGINX

kubectl apply -f common/default-server-secret.yaml

Create a config map for customizing NGINX configuration:

kubectl apply -f common/nginx-config.yaml

Create an IngressClass resource:

kubectl apply -f common/ingress-class.yaml

Create custom resource definitions for VirtualServer and VirtualServerRoute, TransportServer and Policy resources:
kubectl apply -f common/crds/k8s.nginx.org_virtualservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_virtualserverroutes.yaml
kubectl apply -f common/crds/k8s.nginx.org_transportservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_policies.yaml

Deploy the Ingress Controller after modifying downloaded yaml file, mention your own private repo and secret if any.

kubectl apply -f ~/nginx-plus-ingress.yaml

Create a Service for the Ingress Controller Pods

kubectl create -f ~/nodeport.yaml

Create namespace "arc"

kubectl create ns arc

Deploy arcadia application in arc namespace

kubectl apply -f ~/arcadia-all-clusterip.yaml

Create arcadia secret for TLS certificates

kubectl apply -f ~/arc-secret.yaml

Create Arcadia specific virtual server

kubectl apply -f ~/arc-virtual-server.yaml


JamOPD&4*56(