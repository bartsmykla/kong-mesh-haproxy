```sh
kubectl apply -n atmos-system -f other-resources.yaml
helm repo add haproxy-ingress https://haproxy-ingress.github.io/charts 
helm repo update
helm upgrade --debug --install -n atmos-system --values values.yaml ingress haproxy-ingress/haproxy-ingress
kubectl apply -f echo-service.yaml
kubectl apply -f external-services.yaml
```

If you will open file `values.yaml` very important properties to make haproxy work are:

```yaml
controller:
  podAnnotations:
    kuma.io/gateway: enabled
  [...]
  config:
    service-upstream: "true"
```
