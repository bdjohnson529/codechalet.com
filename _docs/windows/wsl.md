---
title: "Windows Subsystem for Linux"
layout: blog
parent: Windows
parent_path: windows/
---
Our apps will typically be deployed on Linux machines. To streamline deployment, it is recommended that the apps are tested on Ubuntu before attempting to deploy them on an external machine via Azure Pipelines or Azure App Service. Fortunately, Microsoft has released a contanerized version of Linux, called the Windows Subsystem for Linux, which can be installed on Windows machines. The WSL is available for installation through the Microsoft Store, free of cost. Surprisingly enough, the majority of Linux computers in the world are actually deployed by Microsoft, so they have plenty of experience containerizing the Linux OS.

## Mounted Drives
Access Windows filesystem from Linux
```
/mnt/c
```
Access Linux filesystem from Windows
```
\\wsl$\Ubuntu-18.04\
``` 


## Add an SSH key for Azure DevOps
To clone repositories from Azure DevOps, you'll need to create an SSH key with WSL2, and add the key to your DevOps account. [Follow this tutorial.](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops)


# Troubleshooting
If you're having trouble pinging `google.com` from the WSL, try the following. Edit `/etc/resolv.conf` and add the following nameserver:
```bash
nameserver 1.1.1.1
```


## Further Reading
* [Heroku Buildpack: Python](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-python)
* [Docker on WSL2](https://hinty.io/ivictbor/simple-way-to-docker-on-windows-10-home-with-wsl-2/)
* [Create a Running Docker Container With Gunicorn and Flask](https://medium.com/better-programming/create-a-running-docker-container-with-gunicorn-and-flask-dcd98fddb8e0)
* [You Still Should Have Anti-Virus With Windows Subsystem For Linux](https://www.phoronix.com/scan.php?page=news_item&px=Windows-Defender-WSL-Needed)
* [FIX Avast Service High CPU Usage Windows 10/8/7](https://www.youtube.com/watch?v=-f_V3wrpLXA)