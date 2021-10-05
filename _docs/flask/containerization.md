---
title: "Containerization of Flask apps"
layout: blog
order: 8
topic: Flask
topic_path: /docs/flask/index.html
---
Developers often experience problems when deploying software. For every app, there are tens or hundreds of libraries which need to be installed, sometimes in a particular order and with specific version numbers. Each operating system is slightly different, so the process of deploying an app on a new computer can be quite difficult.

Container deployment solves a lot of these configuration issues. The app runs in a container, which is a virtualized environment. The container will execute the exact same way on every machine. In theory, this makes it easier to deploy since you can choose any machine to use as the server. There is no configuration necessary - your app should simply run on the machine you’ve chosen.

Docker is the most popular tool for containerizing apps. Docker images are created using a Dockerfile. Buildpacks can be used to generate a Dockerfile for a Python application.


## Setup
Install buildpacks.
```bash
curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.15.0/pack-v0.15.0-linux.tgz" | sudo tar -C /usr/local/bin/ --no-same-owner -xzv pack
```

Build the Python app image. After the following command completes, you should be able to view the app image in the Docker GUI.
```bash
pack build testrepo/testcontainer:1.0.0.0 --builder heroku/buildpacks:18
```

Run the app image, using Docker.
```bash
docker run --rm -p 8080:8080 testrepo/testcontainer:1.0.0.0
```

# Further reading
* [Python like a pro - build Docker containers](https://tanzu.vmware.com/developer/guides/python/cnb-gs-python/)
* [How to remove docker images containers and volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)