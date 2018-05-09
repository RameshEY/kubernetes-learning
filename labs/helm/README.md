# Helm (헤ㄹ~음)

### Prerequistes

* brew cask install minikube
* brew install kubernetes-helm
* kubectl

### Tutorial

Download and install the latest Minikube:

```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 && \
  chmod +x minikube && \
  sudo mv minikube /usr/local/bin/
```

Install the xhyve driver and set its permissions:

```sh
brew install docker-machine-driver-xhyve
sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
```

Start the Minikube cluster:

```sh
minikube start --vm-driver=xhyve
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
WARNING: The xhyve driver is now deprecated and support for it will be removed in a future release.
Please consider switching to the hyperkit driver, which is intended to replace the xhyve driver.
See https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#hyperkit-driver for more information.
To disable this message, run [minikube config set WantShowDriverDeprecationNotification false]
Downloading Minikube ISO
 150.53 MB / 150.53 MB [============================================] 100.00% 0s

Getting VM IP address...
Moving files into cluster...
Downloading kubelet v1.10.0
Downloading kubeadm v1.10.0
Finished Downloading kubeadm v1.10.0
Finished Downloading kubelet v1.10.0
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
Loading cached images from config file.
```

Open the Kubernetes dashboard in a browser:

```
minikube dashboard
```

Install the Helm client:

```sh
brew install kubernetes-helm
```

Setup the Helm:

```sh
helm init --upgrade
Creating /Users/#####/.helm
Creating /Users/#####/./.helm/repository
Creating /Users/#####/.helm/repository/cache
Creating /Users/#####/.helm/repository/local
Creating /Users/#####/.helm/plugins
Creating /Users/#####/.helm/starters
Creating /Users/#####/.helm/cache/archive
Creating /Users/#####/.helm/repository/repositories.yaml
Adding stable repo with URL: https://kubernetes-charts.storage.googleapis.com
Adding local repo with URL: http://127.0.0.1:8879/charts
$HELM_HOME has been configured at /Users/#####/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy```````.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
Happy Helming!
```

Switch to the Minikube context:

```
kubectl use-context minicube
```

Create the example Kubernetes:

```
mkdir manifests
kubectl run nginx-example --image=nginx:1.13.5-alpine -o yaml > manifests/deployment.yaml
kubectl expose deployment example --port=80 --type=NodePort -o yaml > manifests/service.yaml
```

Clean up Kubernetes environment

```
kubectl delete -f manifests
```

### Fix the latest verion of Helm issue

```
$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈

$ kubectl create clusterrolebinding tiller-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
kube-system:default
clusterrolebinding "tiller-cluster-admin" created

$ kubectl -n kube-system patch deployment tiller-deploy -p '{"spec": {"template": {"spec": {"automountServiceAccountToken": true}}}}'
deployment "tiller-deploy" patched
```

Edit Chart.yaml and values.yaml

And install your first helm chart:

```sh
$ helm install -n my-super-fantastic-helm-chart
NAME:   my-super-fantastic-helm-chart
LAST DEPLOYED: Thu May 10 00:20:08 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME           TYPE      CLUSTER-IP      EXTERNAL-IP  PORT(S)       AGE
nginx-example  NodePort  10.106.154.226  <none>       80:31208/TCP  0s

==> v1beta1/Deployment
NAME           DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
nginx-example  1        0        0           0          0s

==> v1/Pod(related)
NAME                           READY  STATUS   RESTARTS  AGE
nginx-example-bf4d94c5f-lcrss  0/1    Pending  0         0s
```

```
minikube service nginx-example --url
http://192.168.64.2:31208
```

```
$ helm del --purge my-super-fantastic-helm-chart
release "my-super-fantastic-helm-chart" deleted
```

Edit it again and install the second version of Chart:

```
$ helm install -n second helm
NAME:   second
LAST DEPLOYED: Thu May 10 00:40:49 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME           TYPE      CLUSTER-IP      EXTERNAL-IP  PORT(S)       AGE
nginx-example  NodePort  10.106.154.226  <none>       80:31208/TCP  0s

==> v1beta1/Deployment
NAME    DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
second  1        0        0           0          0s
```

### Links

- https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/
- https://kubernetes.io/docs/getting-started-guides/minikube/
- http://tech.paulcz.net/blog/getting-started-with-helm/
- https://daemonza.github.io/2017/02/20/using-helm-to-deploy-to-kubernetes/
- https://cloudacademy.com/blog/deploying-kubernetes-applications-with-helm/-
