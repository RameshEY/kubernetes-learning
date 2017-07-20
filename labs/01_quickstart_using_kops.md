## Prerequisites

- Free Domain: k8s.coolbrain.ml (https://freenom.com)
- [Kubernetes Install](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-via-curl)
- [Kops](https://github.com/kubernetes/kops)

### Querying the AWS for identifing all regions to access
Output:

    aws ec2 describe-availability-zones | jq '.AvailabilityZones | .[] | .ZoneName' --raw-output
    ap-northeast-2a
    ap-northeast-2c

### Cluster Setup on AWS using kops
    kops create cluster --name=k8s.coolbrain.ml --state=s3://kops-state-xxxx --zones=ap-northeast-2a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=k8s.coolbrain.ml

Output:

    I0720 23:54:04.745560   56580 create_cluster.go:654] Inferred --cloud=aws from zone "ap-northeast-2a"
    I0720 23:54:04.745660   56580 create_cluster.go:833] Using SSH public key: /Users/randy/.ssh/id_rsa.pub
    I0720 23:54:05.897704   56580 subnets.go:183] Assigned CIDR 172.20.32.0/19 to subnet ap-northeast-2a
    Previewing changes that will be made:

    ...

    Kops has set your kubectl context to k8s.coolbrain.ml

    Cluster is starting.  It should be ready in a few minutes.

    Suggestions:
     * validate cluster: kops validate cluster
     * list nodes: kubectl get nodes --show-labels
     * ssh to the master: ssh -i ~/.ssh/id_rsa admin@api.k8s.coolbrain.ml
    The admin user is specific to Debian. If not using Debian please use the appropriate user based on your OS.
     * read about installing addons: https://github.com/kubernetes/kops/blob/master/docs/addons.md

### Get the status of nodes
	kubectl get node

Output:

	ip-172-20-51-193.ap-northeast-2.compute.internal   Ready,node     2m        v1.6.2
	ip-172-20-54-156.ap-northeast-2.compute.internal   Ready,master   5m        v1.6.2
	ip-172-20-59-11.ap-northeast-2.compute.internal    Ready,node     2m        v1.6.2

### Run a simple program

	kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
	deployment "hello-minikube" created

 	kubectl expose deployment hello-minikube --type=NodePort
	service "hello-minikube" exposed

	kubectl get service
	NAME             CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
	hello-minikube   100.70.130.45   <nodes>       8080:31275/TCP   11s
	kubernetes       100.64.0.1      <none>        443/TCP          23m

### Delete a cluster using kops

	kops delete cluster --name k8s.coolbrain.ml --state=s3://kops-state-xxxx

	TYPE                    NAME                                                                            ID
	autoscaling-config      master-ap-northeast-2a.masters.k8s.coolbrain.ml-20170720150956                  master-ap-northeast-2a.masters.k8s.coolbrain.ml-20170720150956
	autoscaling-config      nodes.k8s.coolbrain.ml-20170720150956                                           nodes.k8s.coolbrain.ml-20170720150956
	autoscaling-group       master-ap-northeast-2a.masters.k8s.coolbrain.ml                                 master-ap-northeast-2a.masters.k8s.coolbrain.ml
	autoscaling-group       nodes.k8s.coolbrain.ml                                                          nodes.k8s.coolbrain.ml
	dhcp-options            k8s.coolbrain.ml                                                                dopt-32c62c5a
	iam-instance-profile    masters.k8s.coolbrain.ml                                                        masters.k8s.coolbrain.ml
	iam-instance-profile    nodes.k8s.coolbrain.ml                                                          nodes.k8s.coolbrain.ml
	iam-role                masters.k8s.coolbrain.ml                                                        masters.k8s.coolbrain.ml
	iam-role                nodes.k8s.coolbrain.ml                                                          nodes.k8s.coolbrain.ml
	instance                master-ap-northeast-2a.masters.k8s.coolbrain.ml                                 i-0f513dcd32f4b52c4
	instance                nodes.k8s.coolbrain.ml                                                          i-076022ad47c812cfc
	instance                nodes.k8s.coolbrain.ml                                                          i-08f37b5a8735fdb40
	internet-gateway        k8s.coolbrain.ml                                                                igw-64bfc30d
	keypair                 kubernetes.k8s.coolbrain.ml-c1:9c:23:09:4e:d6:ac:a6:cb:05:c4:4f:33:65:0f:a1     kubernetes.k8s.coolbrain.ml-c1:9c:23:09:4e:d6:ac:a6:cb:05:c4:4f:33:65:0f:a1
	route-table             k8s.coolbrain.ml                                                                rtb-82aa56ea
	route53-record          api.internal.k8s.coolbrain.ml.                                                  ZBO038WB5KJ1O/api.internal.k8s.coolbrain.ml.
	route53-record          api.k8s.coolbrain.ml.                                                           ZBO038WB5KJ1O/api.k8s.coolbrain.ml.
	route53-record          etcd-a.internal.k8s.coolbrain.ml.                                               ZBO038WB5KJ1O/etcd-a.internal.k8s.coolbrain.ml.
	route53-record          etcd-events-a.internal.k8s.coolbrain.ml.                                        ZBO038WB5KJ1O/etcd-events-a.internal.k8s.coolbrain.ml.
	security-group          masters.k8s.coolbrain.ml                                                        sg-6aeabe02
	security-group          nodes.k8s.coolbrain.ml                                                          sg-c0eabea8
	subnet                  ap-northeast-2a.k8s.coolbrain.ml                                                subnet-7ed23c16
	volume                  a.etcd-events.k8s.coolbrain.ml                                                  vol-0345ce94c688247fb
	volume                  a.etcd-main.k8s.coolbrain.ml                                                    vol-07bf774db2d59da85
	vpc                     k8s.coolbrain.ml                                                                vpc-915845f8


### Kops API

https://api.k8s.coolbrain.ml/ (Login required)

Output

```json
{
	paths: [
		"/api",
		"/api/v1",
		"/apis",
		"/apis/apps",
		"/apis/apps/v1beta1",
		"/apis/authentication.k8s.io",
		"/apis/authentication.k8s.io/v1",
		"/apis/authentication.k8s.io/v1beta1",
		"/apis/authorization.k8s.io",
		"/apis/authorization.k8s.io/v1",
		"/apis/authorization.k8s.io/v1beta1",
		"/apis/autoscaling",
		"/apis/autoscaling/v1",
		"/apis/autoscaling/v2alpha1",
		"/apis/batch",
		"/apis/batch/v1",
		"/apis/batch/v2alpha1",
		"/apis/certificates.k8s.io",
		"/apis/certificates.k8s.io/v1beta1",
		"/apis/extensions",
		"/apis/extensions/v1beta1",
		"/apis/policy",
		"/apis/policy/v1beta1",
		"/apis/rbac.authorization.k8s.io",
		"/apis/rbac.authorization.k8s.io/v1alpha1",
		"/apis/rbac.authorization.k8s.io/v1beta1",
		"/apis/settings.k8s.io",
		"/apis/settings.k8s.io/v1alpha1",
		"/apis/storage.k8s.io",
		"/apis/storage.k8s.io/v1",
		"/apis/storage.k8s.io/v1beta1",
		"/healthz",
		"/healthz/ping",
		"/healthz/poststarthook/bootstrap-controller",
		"/healthz/poststarthook/ca-registration",
		"/healthz/poststarthook/extensions/third-party-resources",
		"/logs",
		"/metrics",
		"/swaggerapi/",
		"/ui/",
		"/version"
	]
}
```

## Epilogue
Easy peasy, right?

- [Terraform](https://www.terraform.io/)
- [Building Kubernetes clusters with Terraform](https://github.com/kubernetes/kops/blob/master/docs/terraform.md)
