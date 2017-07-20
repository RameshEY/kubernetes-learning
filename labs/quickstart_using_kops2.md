## Prerequisites

- AWS Free Tier
- AWS Route53 Hosted Zones (ex. k8s.coolbrain.ml http://freenom.com)
- S3 buckets
- [AWS CLI](https://aws.amazon.com/cli/)
- [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-via-curl)
- [Kops](https://github.com/kubernetes/kops)

### Querying AWS to identify accessible regions

    > aws ec2 describe-availability-zones | jq '.AvailabilityZones | .[] | .ZoneName' --raw-output
    ap-northeast-2a
    ap-northeast-2c

### Create a cluster configuration on AWS using Kops
    > kops create cluster --name=k8s.coolbrain.ml --state=s3://kops-state-xxxx --zones=ap-northeast-2a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=k8s.coolbrain.ml

Output:

	I0723 00:36:42.842574   27024 create_cluster.go:654] Inferred --cloud=aws from zone "ap-northeast-2a"
	I0723 00:36:42.843015   27024 create_cluster.go:833] Using SSH public key: /Users/randy/.ssh/id_rsa.pub
	I0723 00:36:43.988631   27024 subnets.go:183] Assigned CIDR 172.20.32.0/19 to subnet ap-northeast-2a
	Previewing changes that will be made:

	I0723 00:36:48.964672   27024 executor.go:91] Tasks: 0 done / 63 total; 34 can run
	I0723 00:36:50.984838   27024 executor.go:91] Tasks: 34 done / 63 total; 12 can run
	I0723 00:36:51.466561   27024 executor.go:91] Tasks: 46 done / 63 total; 15 can run
	I0723 00:36:51.667974   27024 executor.go:91] Tasks: 61 done / 63 total; 2 can run
	I0723 00:36:51.694211   27024 executor.go:91] Tasks: 63 done / 63 total; 0 can run
	Will create resources:
	  AutoscalingGroup/master-ap-northeast-2a.masters.k8s.coolbrain.ml
		MinSize                 1
		MaxSize                 1
		Subnets                 [name:ap-northeast-2a.k8s.coolbrain.ml]
		Tags                    {k8s.io/role/master: 1, Name: master-ap-northeast-2a.masters.k8s.coolbrain.ml, KubernetesCluster: k8s.coolbrain.ml}
		LaunchConfiguration     name:master-ap-northeast-2a.masters.k8s.coolbrain.ml

	  AutoscalingGroup/nodes.k8s.coolbrain.ml
		MinSize                 2
		MaxSize                 2
		Subnets                 [name:ap-northeast-2a.k8s.coolbrain.ml]
		Tags                    {k8s.io/role/node: 1, Name: nodes.k8s.coolbrain.ml, KubernetesCluster: k8s.coolbrain.ml}
		LaunchConfiguration     name:nodes.k8s.coolbrain.ml

	  DHCPOptions/k8s.coolbrain.ml
		DomainName              ap-northeast-2.compute.internal
		DomainNameServers       AmazonProvidedDNS

	  EBSVolume/a.etcd-events.k8s.coolbrain.ml
		AvailabilityZone        ap-northeast-2a
		VolumeType              gp2
		SizeGB                  20
		Encrypted               false
		Tags                    {Name: a.etcd-events.k8s.coolbrain.ml, KubernetesCluster: k8s.coolbrain.ml, k8s.io/etcd/events: a/a, k8s.io/role/master: 1}

	  EBSVolume/a.etcd-main.k8s.coolbrain.ml
		AvailabilityZone        ap-northeast-2a
		VolumeType              gp2
		SizeGB                  20
		Encrypted               false
		Tags                    {k8s.io/etcd/main: a/a, k8s.io/role/master: 1, Name: a.etcd-main.k8s.coolbrain.ml, KubernetesCluster: k8s.coolbrain.ml}

	  IAMInstanceProfile/masters.k8s.coolbrain.ml

	  IAMInstanceProfile/nodes.k8s.coolbrain.ml

	  IAMInstanceProfileRole/masters.k8s.coolbrain.ml
		InstanceProfile         name:masters.k8s.coolbrain.ml id:masters.k8s.coolbrain.ml
		Role                    name:masters.k8s.coolbrain.ml

	  IAMInstanceProfileRole/nodes.k8s.coolbrain.ml
		InstanceProfile         name:nodes.k8s.coolbrain.ml id:nodes.k8s.coolbrain.ml
		Role                    name:nodes.k8s.coolbrain.ml

	  IAMRole/masters.k8s.coolbrain.ml
		ExportWithID            masters

	  IAMRole/nodes.k8s.coolbrain.ml
		ExportWithID            nodes

	  IAMRolePolicy/masters.k8s.coolbrain.ml
		Role                    name:masters.k8s.coolbrain.ml

	  IAMRolePolicy/nodes.k8s.coolbrain.ml
		Role                    name:nodes.k8s.coolbrain.ml

	  InternetGateway/k8s.coolbrain.ml
		VPC                     name:k8s.coolbrain.ml
		Shared                  false

	  Keypair/kops
		Subject                 o=system:masters,cn=kops
		Type                    client

	  Keypair/kube-controller-manager
		Subject                 cn=system:kube-controller-manager
		Type                    client

	  Keypair/kube-proxy
		Subject                 cn=system:kube-proxy
		Type                    client

	  Keypair/kube-scheduler
		Subject                 cn=system:kube-scheduler
		Type                    client

	  Keypair/kubecfg
		Subject                 o=system:masters,cn=kubecfg
		Type                    client

	  Keypair/kubelet
		Subject                 o=system:nodes,cn=kubelet
		Type                    client


	  SecurityGroupRule/ssh-external-to-master-0.0.0.0/0
        SecurityGroup           name:masters.k8s.coolbrain.ml
        CIDR                    0.0.0.0/0
        Protocol                tcp
        FromPort                22
        ToPort                  22
	...

	  SecurityGroupRule/ssh-external-to-node-0.0.0.0/0
		SecurityGroup           name:nodes.k8s.coolbrain.ml
		CIDR                    0.0.0.0/0
		Protocol                tcp
		FromPort                22
		ToPort                  22

	  Subnet/ap-northeast-2a.k8s.coolbrain.ml
		VPC                     name:k8s.coolbrain.ml
		AvailabilityZone        ap-northeast-2a
		CIDR                    172.20.32.0/19
		Shared                  false
		Tags                    {KubernetesCluster: k8s.coolbrain.ml, Name: ap-northeast-2a.k8s.coolbrain.ml, kubernetes.io/cluster/k8s.coolbrain.ml: owned}

	  VPC/k8s.coolbrain.ml
		CIDR                    172.20.0.0/16
		EnableDNSHostnames      true
		EnableDNSSupport        true
		Shared                  false
		Tags                    {Name: k8s.coolbrain.ml, kubernetes.io/cluster/k8s.coolbrain.ml: owned, KubernetesCluster: k8s.coolbrain.ml}

	  VPCDHCPOptionsAssociation/k8s.coolbrain.ml
		VPC                     name:k8s.coolbrain.ml
		DHCPOptions             name:k8s.coolbrain.ml

	Must specify --yes to apply changes

	Cluster configuration has been created.

	Suggestions:
	 * list clusters with: kops get cluster
	 * edit this cluster with: kops edit cluster k8s.coolbrain.ml
	 * edit your node instance group: kops edit ig --name=k8s.coolbrain.ml nodes
	 * edit your master instance group: kops edit ig --name=k8s.coolbrain.ml master-ap-northeast-2a

	Finally configure your cluster with: kops update cluster k8s.coolbrain.ml --yes


### Start a cluster

	> kops update cluster k8s.coolbrain.ml --yes --state=s3://kops-state-xxxx
	
	I0723 00:44:30.629996   27375 executor.go:91] Tasks: 0 done / 63 total; 34 can run
	I0723 00:44:31.310438   27375 vfs_castore.go:422] Issuing new certificate: "kubelet"
	I0723 00:44:31.351347   27375 vfs_castore.go:422] Issuing new certificate: "master"
	I0723 00:44:31.417583   27375 vfs_castore.go:422] Issuing new certificate: "kops"
	I0723 00:44:31.451425   27375 vfs_castore.go:422] Issuing new certificate: "kube-scheduler"
	I0723 00:44:31.483335   27375 vfs_castore.go:422] Issuing new certificate: "kube-controller-manager"
	I0723 00:44:31.636077   27375 vfs_castore.go:422] Issuing new certificate: "kube-proxy"
	I0723 00:44:32.307178   27375 vfs_castore.go:422] Issuing new certificate: "kubecfg"
	I0723 00:44:33.047062   27375 executor.go:91] Tasks: 34 done / 63 total; 12 can run
	I0723 00:44:34.971088   27375 executor.go:91] Tasks: 46 done / 63 total; 15 can run
	I0723 00:44:36.436823   27375 launchconfiguration.go:319] waiting for IAM instance profile "nodes.k8s.coolbrain.ml" to be ready
	I0723 00:44:36.453260   27375 launchconfiguration.go:319] waiting for IAM instance profile "masters.k8s.coolbrain.ml" to be ready
	I0723 00:44:46.717908   27375 executor.go:91] Tasks: 61 done / 63 total; 2 can run
	I0723 00:44:47.146754   27375 executor.go:91] Tasks: 63 done / 63 total; 0 can run
	I0723 00:44:47.146798   27375 dns.go:152] Pre-creating DNS records
	I0723 00:44:49.664052   27375 update_cluster.go:229] Exporting kubecfg for cluster
	Kops has set your kubectl context to k8s.coolbrain.ml
	
	Cluster is starting.  It should be ready in a few minutes.
	
	Suggestions:
	 * validate cluster: kops validate cluster
	 * list nodes: kubectl get nodes --show-labels
	 * ssh to the master: ssh -i ~/.ssh/id_rsa admin@api.k8s.coolbrain.ml
	The admin user is specific to Debian. If not using Debian please use the appropriate user based on your OS.
	 * read about installing addons: https://github.com/kubernetes/kops/blob/master/docs/addons.md


	

### Get the status of nodes
	> kubectl get node

Output:

	ip-172-20-51-193.ap-northeast-2.compute.internal   Ready,node     2m        v1.6.2
	ip-172-20-54-156.ap-northeast-2.compute.internal   Ready,master   5m        v1.6.2
	ip-172-20-59-11.ap-northeast-2.compute.internal    Ready,node     2m        v1.6.2
	
	

### Run a simple program

	> kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
	deployment "hello-minikube" created

 	> kubectl expose deployment hello-minikube --type=NodePort
	service "hello-minikube" exposed

	> kubectl get service
	NAME             CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
	hello-minikube   100.70.130.45   <nodes>       8080:31275/TCP   11s
	kubernetes       100.64.0.1      <none>        443/TCP          23m

### Delete a cluster using kops

	> kops delete cluster --name k8s.coolbrain.ml --state=s3://kops-state-xxxx

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
	"paths": [
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

- [Terraform](https://www.terraform.io/)
- [Building Kubernetes clusters with Terraform](https://github.com/kubernetes/kops/blob/master/docs/terraform.md)
