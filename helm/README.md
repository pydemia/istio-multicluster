# Istio

## Install

See: https://istio.io/latest/docs/setup/install/helm/

```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update
helm search repo istio
```

```bash
# helm install <release> <chart> --namespace <namespace> --create-namespace [--set <other_parameters>]
kubectl create namespace istio-system
helm upgrade --install \
  istio-base \
  istio/base \
  -n istio-system
helm upgrade --install \
  istiod \
  istio/istiod \
  -n istio-system \
  --wait
helm status istiod -n istio-system
helm upgrade --install \
  istio-cni \
  istio/cni \
  -n istio-system

helm upgrade --install \
  istio-gateway \
  istio/gateway \
  -n istio-system


# # Optional
# helm install istio-ingress istio/gateway -n istio-ingress --wait
```


```bash
$ kubectl -n istio-system get svc
NAME            TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)                                      AGE
istio-gateway   LoadBalancer   x.x.x.x       x.x.x.x         15021:31363/TCP,80:30680/TCP,443:30727/TCP   10m
istiod          ClusterIP      x.x.x.x       x.x.x.x         15010/TCP,15012/TCP,443/TCP,15014/TCP        15m
```


## Delete


### (Optional) Delete CRDs by istio

```bash
kubectl get crd -oname | grep --color=never 'istio.io' | xargs kubectl delete
```