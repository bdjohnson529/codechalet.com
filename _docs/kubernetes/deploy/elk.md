---
title: "ELK Stack"
layout: blog
order: 4
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
---
{% assign pages = site.docs | sort: 'order' %}

The [ELK stack](https://www.elastic.co/what-is/elk-stack) includes Elasticsearch, Logstash and Kibana.
* Elasticsearch is a search and analytics engine
* Logstash is a server-side data processing pipeline
* Kibana is a UI for the stack

Each of these products is open-source, which means we can host them on Kubernetes for free (the only cost is the cost of hosting the cluster).

1. [Deploy Elastic cloud on Kubernetes](https://www.elastic.co/guide/en/cloud-on-k8s/2.5/k8s-deploy-eck.html)

2. [Create an Elasticsearch cluster.](https://www.elastic.co/guide/en/cloud-on-k8s/2.5/k8s-deploy-elasticsearch.html) Save the following file as `elastic.yml`.
```yml
apiVersion: elasticsearch.k8s.elastic.co/v1
kind: Elasticsearch
metadata:
  name: quickstart
spec:
  version: 8.5.1
  nodeSets:
  - name: default
    count: 1
    config:
      node.store.allow_mmap: false
```

    Apply the manifest.
    ```
    kubectl apply -f elastic.yml
    ```

    Verify creation
    ```
    kubectl get elasticsearch
    ```

3. [Create a Kibana instance](https://www.elastic.co/guide/en/cloud-on-k8s/2.5/k8s-deploy-kibana.html). Save the following file as `kibana.yml`.
```yml
apiVersion: kibana.k8s.elastic.co/v1
kind: Kibana
metadata:
  name: quickstart
spec:
  version: 8.5.1
  count: 1
  elasticsearchRef:
    name: quickstart
```

    Apply the manifest.
    ```
    kubectl apply -f kibana.yml
    ```

    Verify creation
    ```
    kubectl get kibana
    ```

<hr>

#### Resources
* [Elastic cloud on kubernetes](https://www.elastic.co/guide/en/cloud-on-k8s/2.5/index.html)