## Sites web pour Kavita
https://www.kavitareader.com/

https://github.com/Kareadita/Kavita

### Explication

Ci dessous la version du docker-compose que j utilise
Tous les comics sont dans le dossier "data"

```yaml
version: "3.9"
services:
  kavita:
    image: jvmilazz0/kavita:latest
    container_name: Kavita
    hostname: kavita
    mem_limit: 4g
    cpu_shares: 768
    security_opt:
      - no-new-privileges:true
    ports:
      - 5000:5000
    volumes:
      - /volume2/docker/kavita/config:/kavita/config:rw
      - /volume2/docker/kavita/data:/manga:rw
    restart: on-failure:5
```

Librement inspiré du site web : https://mariushosting.com/synology-install-kavita-with-portainer/
