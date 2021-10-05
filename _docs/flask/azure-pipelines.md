---
title: "Azure Pipelines"
layout: blog
order: 7
topic: Flask
topic_path: /docs/flask/index.html
---
Deploying an app can be a tedious process. In a basic deployment scenario, the developer needs to copy the app from a Github repository to the computer where the app is deployed. There are lots of configuration issues which can arise in this situation.

CI/CD is a method to automate software deployment. Azure Pipelines is a CI/CD tool which can be used to automate deployments on Azure. A file named azure-pipelines.yml defines the CI/CD pipeline.

A basic CI/CD pipeline might consist of three steps:

1.	Build a Docker image of the app
2.	Run a security scan
3.	Push the Docker image to the Kubernetes repository
