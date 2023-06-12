```shell
docker network create proxy
docker network create media-network
```

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /data/docker-config/portainer:/data portainer/portainer-ce:latest
```