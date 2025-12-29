# Longhorn Installation

## Prerequisites
- knode206 and knode207 have /data mounted (150GB each)
- kubectl access from knode204

## Install
````bash
helm repo add longhorn https://charts.longhorn.io
helm install longhorn longhorn/longhorn \
  --namespace longhorn-system \
  --create-namespace \
  -f longhorn-values.yaml
````

## Access UI
http://knode204:30880
http://knode206:30880
http://knode207:30880

## Verify
kubectl -n longhorn-system get pods
kubectl -n longhorn-system get svc
````
