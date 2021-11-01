---
title: "Web app primer"
layout: blog
order: 0
topic: Flask
topic_path: /docs/flask/index.html
---
This guide is intended to explain basic web application architecture to a non-technical audience.

## Clients and servers
Computers connected to the web are called clients and servers. Clients make requests, and servers fulfill those requests as responses. Your laptop is the client, and the computer which hosts the website is the server.

* **Static web servers** send files to the client, as-is. This website is hosted on a static web server.
* **Dynamic web servers** update files before sending them to a client, usually using a database. Google Maps is hosted on a dynamic web server.

## App development
An app begins its life as code written on a developer's machine. The developer probably uses their laptop as both the client and the server. The developer's laptop will serve the app at a URL accessible on the laptop. The developer adds features, and views the app by accessing the URL.

## Container deployment
Developers often experience problems setting up a computer to run an app. For every app, there are tens or hundreds of libraries which need to be installed, sometimes in a particular order and with particular version numbers. Each operating system is slightly different, so the process of deploying an app on a new computer can be quite difficult.

Container deployment solves a lot of these configuration issues. The app runs in a container, which is a virtualized environment. The container will execute the exact same way on every machine. In theory, this makes it easier to deploy since you can choose any machine to use as the server. There is no configuration necessary - your app should simply run on the machine you've chosen.

How does an app become a container? Most developers use [Docker](https://www.docker.com/resources/what-container) to containerize their apps. This tutorial uses [Buildpacks](https://buildpacks.io/docs/app-journey/) to generate Docker containers.

## Kubernetes
In the early days of the web, organizations ran applications on physical servers. That architecture caused several problems, the most notable being resource allocation issues. If you are using the same server to run two apps, they will compete for resources.

These days, many apps are run in virtualized containers which run on clusters. The app is not tied to any one physical machine, which solves a lot of the resource allocation issues. [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) is an open-source platform for deploying containerized apps.

## Further reading
* [How the web works](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works)
* [What is a web server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)
* [An app's brief journey from source to image](https://buildpacks.io/docs/app-journey/)
* [What is Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)