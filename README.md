# kubernetes-learning

## Commands

- Version between Kubernetes master(server) and kubectl(client)
```
kubectrl version
```

- Show status fot kube-system
```
kubectl get po -n all -o wide
kubectl -n kube-system get po -o wide
```

- Get logs for kube-controller-manager
```
PODS=$(kubectl -n kube-system get pod -l component=kube-controller-manager -o jsonpath='{.items[0].metadata.name}')
kubectl -n kube-system logs $PODS --tail 100
```

- Get logs for kube-scheduler
```
PODS=$(kubectl -n kube-system get pod -l component=kube-scheduler -o jsonpath='{.items[0].metadata.name}')
kubectl -n kube-system logs $PODS --tail 100
```

- Get logs for dns
```
PODS=$(kubectl -n kube-system get pod -l k8s-app=kube-dns -o jsonpath='{.items[0].metadata.name}')
kubectl -n kube-system logs $PODS -c kubedns
```

- Turn validation off
```
kubectl create -f file.yaml --validate=false
```

- Deploy Kubernetes Dashboard
```
kubectl proxy
(then, open an url with browser http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard/proxy/)
```

- List pods sort by restart count
```
kubectl get pods --all-namespaces --sort-by='.status.containerStatuses[0].restartCount' | awk '$5 > 0 {print $0}' | (read -r; printf "%s\n" "$REPLY"; sort -k5 -nr)
```


## Links
- [kubectl Cheat Sheet](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)
- [Kubernetes at GitHub](https://githubengineering.com/kubernetes-at-github/) (17.08.16)
