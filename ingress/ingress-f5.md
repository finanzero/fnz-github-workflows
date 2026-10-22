# nginx-ingress by F5
Procedures to replace ingress-nginx by F5 supported nginx-ingress, because former one is deprecated by k8n community.

## Install container in cluster
Include repo in Helm controller
* helm repo add nginx-stable https://helm.nginx.com/stable
* helm repo update

Create workload
```sh
helm install nginx-f5 nginx-stable/nginx-ingress \
  --namespace nginx-f5 \
  --create-namespace \
  -f values-f5-prod.yaml
```

## Update Load Balancer
Create two new Backends:
* be-prd-neg-f5-01: standard back end, with CDN configured (to handle Next and WP requests) 
* be-prd-neg-f5-02: APIs back end, with CDN disabled and focused on all API services

## Update keepalive

## beta
kubectl -n default annotate ingress master-api-beta nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-ghub-beta nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-hub-beta nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-hub-beta-finan0 nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n finanvc annotate ingress finanvc-nginx-ingress-resource-f5 nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n lia annotate ingress lia-nginx-ingress-resource-ws nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite

## prod
kubectl -n default annotate ingress master-api nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-ghub nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-hub nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n default annotate ingress master-hub-finan0 nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n finanvc annotate ingress finanvc-nginx-ingress-resource-f5 nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
kubectl -n lia annotate ingress lia-nginx-ingress-resource-ws nginx.org/max-fails=0 nginx.org/keepalive=64 --overwrite
