---
title: "Kubernetes Ingress"
layout: blog
order: 4
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

This post deploys the [game 2048](https://play2048.co/) on EKS, using an [ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/). Ingress is a Kubernetes abstraction which routes traffic to services within the cluster. Within AWS, ingress encapsulates the [application load balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) resource in order to route requests from outside the cluster to services inside the cluster.

The best source of truth for configuring an ingress is [Amazon's instructions](https://docs.aws.amazon.com/eks/latest/userguide/alb-ingress.html) for configuring an application load balancer on Amazon EKS. This guide presents an abridged set of instructions, with commentary to provide color for readers who may be new to Kubernetes concepts.

## Prerequisites
This guide assumes you have the configured the following assets :
* an EKS cluster
* kubectl on your local machine
* helm on your local machine

## ALB controller
The Kubernetes ingress resource needs to be capable of provisioning ALBs and supplemental AWS resources. The ingress resource will create the ALB with rules to route requests to the proper destination, based on ingress manifest (manifests are the yaml files used to define Kubernetes infrastructure). To create the necessary AWS resources, the ingress resource relies on the [AWS Load Balancer Controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/deploy/installation/).

The ALB controller is a Kubernetes service capable of provisioning ALBs in our AWS instance. We will need to provision the cluster nodes with permissions so the ALB controller can create and destroy AWS infrastructure.

1. Identify your cluster node role within the IAM console. The cluster node role uses the following naming convention : `eksctl-myclustername-nod-NodeInstanceRole-XXXXX`.

2. Next, attach the following policy to the cluster node role.
```
{
    "Statement": [
        {
            "Action": [
                "ec2:DescribeVpcs",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeInstances",
                "elasticloadbalancing:DescribeTargetGroups",
                "elasticloadbalancing:DescribeTargetHealth",
                "elasticloadbalancing:ModifyTargetGroup",
                "elasticloadbalancing:ModifyTargetGroupAttributes",
                "elasticloadbalancing:RegisterTargets",
                "elasticloadbalancing:DeregisterTargets"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ],
    "Version": "2012-10-17"
}
```

3. Add the AWS EKS repo to Helm.
```
helm repo add eks https://aws.github.io/eks-charts
```

4. Finally, install the load balancer controller.
```
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=<cluster-name>
```

## Deploy ingress
Now, let's deploy 2048 on the cluster. There is a [complete manifest](https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.4/docs/examples/2048/2048_full.yaml) which defines the application, and the ingress. Let's apply this manifest.
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.4/docs/examples/2048/2048_full.yaml
```

After a few minutes, you should see the ingress resource. Verify the creation of the ingress with the following command.
```
kubectl get ingress
```

Within the AWS EKS console, you can view the ingress under the **Service and networking** tab.

<img src="{{ site.baseurl }}/assets/img/docs/kubernetes/ingress.png" alt="Ingress">
