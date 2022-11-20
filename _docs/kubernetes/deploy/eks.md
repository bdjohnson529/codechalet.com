---
title: "EKS"
layout: blog
order: 1
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

* [EKS security group requirements](https://docs.aws.amazon.com/eks/latest/userguide/sec-group-reqs.html)

List clusters
```
aws eks list-clusters
```