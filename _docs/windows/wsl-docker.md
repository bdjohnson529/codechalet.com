---
title: "Docker on WSL"
layout: blog
parent: Windows
parent_path: windows/
---

Docker is a utility which containerizes applications. To set up docker with the WSL, follow these steps:

1. Install [Docker for Windows.](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
2. Check the WSL version of your Ubuntu distro. In the Ubuntu command line,
```bash
wsl.exe -l -v
``` 
3. If the version of your Ubuntu distro is 1, you need to upgrade to WSL2. To do this, set the version in Windows Powershell.
```bash
wsl --set-version Ubuntu 2
```
4. Follow the instructions on the [Docker website](https://docs.docker.com/docker-for-windows/wsl/) to add your Ubuntu distro as a Docker resource.
5. Test the docker installation. In Ubuntu:
```bash
docker run -d -p 80:80 docker/getting-started
```
And verify the app by accessing the following URL:
```bash
http://localhost
```
You can also see the app running in the Docker GUI.