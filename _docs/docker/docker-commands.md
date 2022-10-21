---
title: "Docker Commands"
layout: blog
order: 0
topic: Docker
topic_path: /docs/docker/index.html
---

View all images
```bash
docker images
```

View all containers
```bash
docker ps
```

Exec into container
```
docker exec -it <container> bash
```

View all active containers
```bash
docker ps -a
```

Run image
```bash
docker run myimage
```

Run image, with interactive TTY console
```bash
docker run -it myimage
```

Exit TTY console
```bash
CRTL-D
```

Remove all inactive containers
```bash
docker container prune
```

Inspect a container
```bash
docker inspect CONTAINERID
```

Stop a container
```bash
docker stop a7a0e504ca3e
```

Execute a command in a container
```bash
docker exec CONTAINERID cat /etc/hosts
```

View container ports
```bash
docker port container-name
```

View docker network interfaces
```bash
docker network ls
```

View container IP address
```bash
docker inspect 1eec29b9e4c3 --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```


## Resources
* [Docker connection refused](https://pythonspeed.com/articles/docker-connection-refused/)