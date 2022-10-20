---
title: "Kubectl Commands"
layout: blog
order: 0
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

Create a manifest
```
kubectl apply -f ./manifest.yaml
```

Destroy a manifest
```
kubectl delete -f ./manifest.yaml
```

View assets
```
kubectl get deployments
kubectl get services
kubectl get pods
kubectl logs <pod>
```

Execute a command inside a pod
```
kubectl exec -it <pod> --container <container> -- /bin/bash
```

Port forward a service
```
kubectl port-forward service/api 3000:3000
```

Get cluster info
```
kubectl cluster-info
```

Describe endpoints of a service
```
kubectl describe endpoints service-2048
```

Check Kubernetes version
```
kubectl version
```