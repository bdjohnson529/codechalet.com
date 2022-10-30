---
title: "Helm Commands"
layout: blog
order: 3
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

Helm commands

<hr>

List all resources
```
helm list --all-namespaces
```

Install a release
```
helm install <release-name> -n <namespace> --set clusterName=<cluster-name>
```

Uninstall a release
```
helm uninstall <release-name> -n <namespace>