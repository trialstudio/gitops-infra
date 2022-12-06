# install

1. install crds

```bash
version=v1.10.0
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/${version}/cert-manager.crds.yaml
```
2. install chart

# uninstall

1. check existing crds and delete them

```bash
kubectl get Issuers,ClusterIssuers,Certificates,CertificateRequests,Orders,Challenges --all-namespaces
```

2. delete actual crds

```bash
version=v1.10.0 
kubectl delete -f https://github.com/cert-manager/cert-manager/releases/download/${version}/cert-manager.crds.yaml
```

# backup

1. 
```bash
backup=/tmp/z
echo '' > $backup
kubectl get -A secret | grep cm-tls | awk '{print "echo --- >> backup && kubectl get -o yaml -n "$1" secret/"$2" >> backup"}' | sed "s;backup;$backup;g" | xargs -tn1 -d'\n' bash -c
kubectl get --all-namespaces -oyaml issuer,clusterissuer,cert > backup.yaml
```
