---
title: "DNS and SSL on EKS"
layout: blog
order: 2
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

Notes apply to deploying Retool on [AWS EKS](https://aws.amazon.com/eks/), using `kubectl`. First, verify that your application is running using port-forwarding. The Retool application is served on port 3000 of `service/api`.
```
kubectl port-forward service/api 3000:3000
```

Next, we will create an `ingress.yaml` manifest and apply it to our EKS cluster. Tod eploy the ingress resource
```
kubectl apply -f ingress.yaml
```

<hr>

## Notes
* [Application load balancing](https://docs.aws.amazon.com/eks/latest/userguide/alb-ingress.html)
* [Ingress specification](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/spec/)
* [AWS ALB - ingress annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.2/guide/ingress/annotations/)
* [How do I set up ExternalDNS with Amazon EKS?](https://aws.amazon.com/premiumsupport/knowledge-center/eks-set-up-externaldns/)
* [What is Ingress?](https://www.eksworkshop.com/beginner/130_exposing-service/ingress/)