# kubernetes-learning

## API References
- [1.10](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/)
- [1.9](https://v1-9.docs.kubernetes.io/docs/api-reference/v1.9/)
- [1.8](https://v1-8.docs.kubernetes.io/docs/api-reference/v1.8/)
- [1.7](https://v1-7.docs.kubernetes.io/docs/api-reference/v1.7/)
- [1.6](https://v1-6.docs.kubernetes.io/docs/api-reference/v1.6/)

## Networking & Clustering & Federation
- [Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
- [Federation](https://kubernetes.io/docs/concepts/cluster-administration/federation/)
- [A cluster of clusters](https://netbears.com/blog/cross-cloud-kubernetes-cluster-of-clusters/), [repo](https://github.com/netbears/kubernetes-federation-cross-cloud)
- [Hybrid](https://schd.ws/hosted_files/kccncna17/7a/Kubecon%20-%20v0.2.pdf)
- [Multi Cloud](https://www.joyent.com/blog/triton-kubernetes-multicloud)
- [Linux Networking Explained](https://events.static.linuxfound.org/sites/events/files/slides/2016%20-%20Linux%20Networking%20explained_0.pdf)
- [Choosing a CNI Network Provider for Kubernetes](https://chrislovecnm.com/kubernetes/cni/choosing-a-cni-provider/)
- [A Hacker’s Guide to Kubernetes Networking](https://thenewstack.io/hackers-guide-kubernetes-networking/)
- [Kubernetes Networking: Achieving High Performance with Calico](https://platform9.com/blog/kubernetes-networking-achieving-high-performance-with-calico/)

## Plugins and Addons
- [Kubernetes Addons](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons)
- [Extend kubectl with plugins](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/)
- [CNCF Networking plugins](https://github.com/containernetworking/plugins)
- [CNI 3rd party plugins](https://github.com/containernetworking/cni#3rd-party-plugins)
- [Network plugins for kubernetes](https://www.slideshare.net/inwinstack/network-plugins-for-kubernetes)

## Packaging: Helm
- [Manage Helm repositories and deploy charts via REST](https://banzaicloud.com/blog/helm-rest-api/) (2018.04)
- [Automated rollback of Helm releases based on logs or metrics](http://container-solutions.com/automated-rollback-helm-releases-based-logs-metrics/) (2018.02)
- [Using Helm to Deploy Blockchain to Kubernetes](https://www.microsoft.com/developerblog/2018/02/09/using-helm-deploy-blockchain-kubernetes/) (2018.02)
- [Building Helm Charts From the Ground Up](https://youtu.be/vQX5nokoqrQ) (2017.12)

## Courses
- [Scalable Microservices with Kubernetes](https://classroom.udacity.com/courses/ud615) (Basic)
- [Learn DevOps: The Complete Kubernetes Course](https://www.udemy.com/learn-devops-the-complete-kubernetes-course/learn/v4/)
- [Learn DevOps: Advanced Kubernetes Usage](https://www.udemy.com/learn-devops-advanced-kubernetes-usage/learn/v4/overview)
- [Learn DevOps: On-Prem or Cloud Agnostic Kubernetes](https://www.udemy.com/learn-devops-on-prem-or-cloud-agnostic-kubernetes/)
- [Kubernetes On The Cloud & The CNCF CKA Certification](https://www.udemy.com/kubernetes-cka-on-cloud/)

## Tutorials
- [AWS Workshop for Kubernetes](https://github.com/aws-samples/aws-workshop-for-kubernetes)
- [GCP Kubernetes Workshops](https://github.com/GoogleCloudPlatform/kubernetes-workshops)
- [Package your Kubernetes Applications with Helm](https://akomljen.com/package-kubernetes-applications-helm/)

## Books
- [Manage Kubernetes](https://www.safaribooksonline.com/library/view/managing-kubernetes/9781492033905)

## Videos
- [Running Kubernetes with Amazon EKS - AWS Online Tech Talks](https://youtu.be/rV_NCvs9iGE) (2018.03)
- [Kubernetes ウェビナー](https://www.youtube.com/watch?v=dA6qa-6ekB0&list=PLlr4ZJV2uX-jS9mSLBvApQApuhkR6u5ES)
  - [01. Kubernetesのエコシステムとその影響](https://youtu.be/dA6qa-6ekB0)
  - [02. Kubernetesの導入事例と最新動向](https://youtu.be/ZOwNeeCVyZk)
- Mastering Series
  - [AWS Tel Aviv Summit 2018: Mastering Kubernetes on AWS](https://www.youtube.com/watch?v=mfx7whOKUH0) (2018.03)
  - [AWS re:Invent 2017: Mastering Kubernetes on AWS (CON308)](https://www.youtube.com/watch?v=w34txLmpEuM)  
- [Role based access control (RBAC) policies in Kubernetes](https://youtu.be/CnHTCTP8d48) (2018.06)
  
## Slides
- [Kubernetes in ZEPL](https://docs.google.com/presentation/d/1AGdDWxnTK2M2emhHis0IlxODngTY6xJycP3ygPvA9F8/) (DevOps Korea 2018)
- [Kubernetes at GitHub](https://schd.ws/hosted_files/kccncna17/44/kubernetes-at-github.pdf), [blog](https://githubengineering.com/kubernetes-at-github/)

## Articles
- [AWS EKS/ECS and Fargate: Understanding the Differences](https://logz.io/blog/aws-eks-ecs-and-fargate/)
- [Kubernetes: First Beta Version of Kubernetes 1.10 is Here](https://kubernetes.io/blog/2018/03/first-beta-version-of-kubernetes-1-10)
- [What’s New in Kubernetes 1.10](https://www.youtube.com/watch?v=EbfMEXnm1lo)
- [Kubernetes 01 – Pod](https://blog.2dal.com/2018/03/28/kubernetes-01-pod/) (2018.03.28)
- [쿠버네티스를 이용해 테스팅 환경 구현해보기](http://woowabros.github.io/experience/2018/03/13/k8s-test.html) (2018.03.13)
- [Kubernetes Federation With Google Global Load Balancer](https://ulam.io/blog/kubernetes-federation-with-google-global-load-balancer/) 
- [Global Kubernetes in 3 Steps](http://cgrant.io/tutorials/gcp/compute/gke/global-kubernetes-three-steps/) (2017.09)
- [Networking Approaches in a Container World](https://events.static.linuxfound.org/sites/events/files/slides/Networking%20approaches%20in%20a%20container%20world.pdf)

## Autoscaling
- [Kubernetes Event Based Auto-Scaler](https://help.spotinst.com/hc/en-us/articles/360000280405-Kubernetes-Event-Based-Auto-Scaler-)
- [Better autoscaling with Prometheus and the Kubernetes Metrics APIs](https://coreos.com/blog/autoscaling-with-prometheus-and-kubernetes-metrics-apis) (2018.01)
- [Horizontal Pod Autoscaling by memory](https://koudingspawn.de/kubernetes-autoscaling/) (2017.10)
- [Kubernetes autoscaling based on custom metrics without using a host port](https://medium.com/@marko.luksa/kubernetes-autoscaling-based-on-custom-metrics-without-using-a-host-port-b783ed6241ac) (2017.02)
- [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- [Kubernetes Horizontal Pod Autoscaler with Prometheus custom metrics](https://github.com/stefanprodan/k8s-prom-hpa)

## Security
- [Container Security & Kubernetes at DigitalOcean HQ](https://www.youtube.com/watch?v=j5Mp-VJ-erY)
- [Protecting APIs from the DDoS attacks by signing the resource identifiers](https://medium.com/@gajus/protecting-apis-from-the-ddos-attacks-by-signing-the-pks-c1eca7cc7725) (2017.02)
- [Datacenter Orchestration Security and Insecurity: Assessing Kubernetes, Mesos, and Docker at Scale
](https://youtu.be/lXggHTqznOI)

## Microservices
- [Mastering Chaos - A Netflix Guide to Microservices](https://youtu.be/CZ3wIuvmHeM) (2017.02)
- [Microservices at Netflix Scale: Principles, Tradeoffs & Lessons Learned • R. Meshenberg](https://www.youtube.com/watch?v=57UK46qfBLY) (2016.09)
- [Microservices • Martin Fowler](https://youtu.be/wgdBVIX9ifA) (2014)
- Martin Fowler on the [Pros](http://martinfowler.com/articles/microservices.html) and [Cons](http://martinfowler.com/articles/microservice-trade-offs.html) of Microservices
- [12 Fractured Apps](https://medium.com/@kelseyhightower/12-fractured-apps-1080c73d481c), [12factor.net](https://12factor.net/ko/)

## Tools
- [kEdge](https://github.com/improbable-eng/kedge)
- [Kubernetes Pod Chaos Monkey](https://github.com/jnewland/kubernetes-pod-chaos-monkey)
- [scope](https://github.com/weaveworks/scope)
- [gcp-live-k8s-visualizer](https://github.com/brendandburns/gcp-live-k8s-visualizer)

## Links
- [KubeWeekly](https://kube.news)
- [KubeCast](https://www.kubecast.com/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)
- [k8s DevStats](https://k8s.devstats.cncf.io/d/12/dashboards)
- [Certified Kubernetes Components](https://www.cncf.io/certification/software-conformance/)
- [Kubernetes Icons Set](https://github.com/octo-technology/kubernetes-icons)
