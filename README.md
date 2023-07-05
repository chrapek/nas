```shell
docker network create proxy
docker network create media-network
```

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /data/docker-config/portainer:/data portainer/portainer-ce:latest
```


If you try to run AdGuardHome on a system where the resolved daemon is started, docker will fail to bind on port 53, because resolved daemon is listening on 127.0.0.53:53. Here's how you can disable DNSStubListener on your machine:

Deactivate DNSStubListener and update the DNS server address. Create a new file, /etc/systemd/resolved.conf.d/adguardhome.conf (creating the /etc/systemd/resolved.conf.d directory if needed) and add the following content to it:

[Resolve]
DNS=127.0.0.1
DNSStubListener=no
Specifying 127.0.0.1 as the DNS server address is necessary because otherwise the nameserver will be 127.0.0.53 which doesn't work without DNSStubListener.

Activate a new resolv.conf file:

mv /etc/resolv.conf /etc/resolv.conf.backup
ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
Stop DNSStubListener:

systemctl reload-or-restart systemd-resolved


traefik:

copy traefik.yml to ${FOLDER_FOR_CONFIGS:?err}/traefik/traefik.yml