---
title: "Docker Networking"
layout: blog
topic: docker
order: 1
parent: Docker
parent_path: docker/
---
A Docker container has its own networking namespace, isolated from the machine it is running on. Your computer has its own networking namespace, which is a shared set of IP routing tables. To view your networking namespace,
```bash
ifconfig
```

Likely you will see at least two interfaces
```bash
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.17.192  netmask 255.255.240.0  broadcast 172.20.31.255

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
```

The loopback interface, `lo`, enables communication within your computer. Notice the loopback interface has an IP address of `127.0.0.1` - if you serve a web app at this IP address, you can access that app by entering the IP address into your browser. `lo` is an internal IP address - only your computer can communicate on this interface. This computer uses the IP address `172.20.17.192` to communicate externally.


## Docker namespaces
Docker containers have their own networking namespace. To view the networking namespace in a Docker container, use the following command and replace `123456` with your container ID
```
docker exec 123456 ifconfig
```

To run a Docker container on the `host` network, use the `--net host` flag
```bash
docker run --net host myapp
```


## External Resources
* [Docker connection refused](https://pythonspeed.com/articles/docker-connection-refused/)
* [How to get a docker container IP address](https://www.freecodecamp.org/news/how-to-get-a-docker-container-ip-address-explained-with-examples/)