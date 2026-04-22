## Sources web et Tutos liés au service
https://www.navidrome.org/

https://mariushosting.com/synology-install-navidrome-with-portainer/

[Belginux - Navidrome](https://belginux.com/navidrome/)


## Explication du service
Navidrome est un serveur de streaming musical open source, gratuit et auto-hébergé qui agit comme une alternative personnelle à des services comme Spotify ou Apple Music.  
Il permet d'indexer une collection musicale locale (stockée sur un NAS, un Raspberry Pi ou un ordinateur) et de la rendre accessible via une interface web moderne ou des applications mobiles tierces.

## Docker Compose
```yaml
services:
  navidrome:
    container_name: navidrome
    image: deluan/navidrome
    mem_limit: 6g
    cpu_shares: 1024
    security_opt:
      - no-new-privileges:true
    restart: on-failure:5
    ports:
      - 4533:4533
    volumes:
      - /volume2/docker/navidrome:/data:rw
      - /volume3/Musiques:/music:rw
    environment:
      PUID: 1000
      PGID: 10
      ND_ENABLEINSIGHTSCOLLECTOR: false
```
***
