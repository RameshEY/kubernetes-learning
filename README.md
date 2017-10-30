# kubernetes-learning

## Commands
- List pods sort by restart count
```
kubectl get pods --all-namespaces --sort-by='.status.containerStatuses[0].restartCount' | awk '$5 > 0 {print $0}' | (read -r; printf "%s\n" "$REPLY"; sort -k5 -nr)
```


## Links
- [kubectl Cheat Sheet](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)
- [Kubernetes at GitHub](https://githubengineering.com/kubernetes-at-github/) (17.08.16)
