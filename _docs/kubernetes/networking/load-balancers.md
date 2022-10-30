---
title: "Load Balancers"
layout: blog
order: 1
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

* [What is an Application Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
* [Application Load Balancing on Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/alb-ingress.html)
* [Set up ALB on AWS](https://aws.amazon.com/premiumsupport/knowledge-center/eks-alb-ingress-controller-setup/)

<hr>

## Instructions
Install load balancer controller
```
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=<cluster-name>
```

Validate installation
```
kubectl get deployment -n kube-system aws-load-balancer-controller
kubectl describe deployment aws-load-balancer-controller -n kube-system
```

