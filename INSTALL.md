# Longhorn Installation

## v1.33 cluster (knode204-207)
- Storage nodes: knode206 (dell1), knode207 (dell2)
- Data disk: 150GB qcow2 at /home/longhorn/knodeXXX-data.qcow2 on KVM host, mounted at /data inside VM
- Data path: /data/longhorn

## v1.36 cluster (knode208-211) — installed June 2026
- Storage nodes: knode210 (dell1), knode211 (dell2) — knode209 excluded intentionally
- Data disk: 50GB qcow2 at /home/longhorn/knodeXXX-data.qcow2 on KVM host, mounted at /data inside VM
- Data path: /data/longhorn
- Node label required: node.longhorn.io/create-default-disk=true (set on knode210, knode211)

## Prerequisites
- Storage nodes have /data mounted (vdb partition, ext4, UUID in /etc/fstab)
- open-iscsi and nfs-common installed, iscsid enabled
- kubectl access
- Node labels applied before helm install:
  kubectl label node knode210 node.longhorn.io/create-default-disk=true
  kubectl label node knode211 node.longhorn.io/create-default-disk=true

## Install
````bash
helm repo add longhorn https://charts.longhorn.io
helm repo update longhorn
helm install longhorn longhorn/longhorn \
  --namespace longhorn-system \
  --create-namespace \
  -f longhorn-values.yaml
````

## Access UI
http://192.168.100.210:30880
http://192.168.100.211:30880

## Verify
kubectl -n longhorn-system get pods
kubectl -n longhorn-system get nodes.longhorn.io
kubectl get storageclass
