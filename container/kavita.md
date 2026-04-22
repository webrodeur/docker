
![Kavita](https://geek-cookbook.funkypenguin.co.nz/images/kavita.png)

## Sources web et Tutos liés au service
https://www.kavitareader.com/

https://github.com/Kareadita/Kavita

Librement inspiré du site web : https://mariushosting.com/synology-install-kavita-with-portainer/

## Explication du service
Kavita est une bibliothèque numérique auto-hébergée propulsée par une fusée qui prend en charge une vaste gamme de formats de fichiers. Installez pour commencer à lire et partager votre serveur avec vos amis.

## Docker Compose
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
***
