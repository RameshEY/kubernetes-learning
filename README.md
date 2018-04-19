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

## Troubleshootings

See what happened. ex) 'CrashLoopBackOff'

```
kubectl logs --previous myapp-osaka-43-7mcsd
```

Delete it

```
kubectl delete pod --namespace=xxxx `kubectl get pods --namespace=xxxx | awk '$3 == "CrashLoopBackOff" {print $1}'
```

## API References
- [1.10](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/)
- [1.9](https://v1-9.docs.kubernetes.io/docs/api-reference/v1.9/)
- [1.8](https://v1-8.docs.kubernetes.io/docs/api-reference/v1.8/)
- [1.7](https://v1-7.docs.kubernetes.io/docs/api-reference/v1.7/)
- [1.6](https://v1-6.docs.kubernetes.io/docs/api-reference/v1.6/)

## Clustering
- [Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

## Plugins
- [Extend kubectl with plugins](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/)
- [CNCF Networking plugins](https://github.com/containernetworking/plugins)
- [CNI 3rd party plugins](https://github.com/containernetworking/cni#3rd-party-plugins)
- [Network plugins for kubernetes](https://www.slideshare.net/inwinstack/network-plugins-for-kubernetes)

## Tutorials
- [AWS Workshop for Kubernetes](https://github.com/aws-samples/aws-workshop-for-kubernetes)
- [Package your Kubernetes Applications with Helm](https://akomljen.com/package-kubernetes-applications-helm/)

## Articles
- [Kubernetes: First Beta Version of Kubernetes 1.10 is Here](https://kubernetes.io/blog/2018/03/first-beta-version-of-kubernetes-1-10)
- [쿠버네티스를 이용해 테스팅 환경 구현해보기](http://woowabros.github.io/experience/2018/03/13/k8s-test.html) (2018.03.13)
- [Kubernetes at GitHub](https://githubengineering.com/kubernetes-at-github/) (17.08.16)

## Links
- [kubectl Cheat Sheet](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)

