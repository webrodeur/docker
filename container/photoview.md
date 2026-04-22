
## Sources web et Tutos liés au service
[Github](https://photoview.github.io/)

[Mariushosting - Photoview](https://mariushosting.com/how-to-install-photoview-on-your-synology-nas/)

[Belginux - Photoview](https://belginux.com/installer-photoview-avec-docker/)

## Explication du service
Si vous avez déjà une collection de photos et vidéos bien rangée et que vous cherchez une application de galerie légère, 
qui peut supporter de grosses bibliothèques et qui ne s'encombre pas de 3500 fonctions parfois bien inutiles quand on veut un simple album photo, 
Photoview vaut très certainement un coup d’œil!

## Docker Compose
```yaml
version: "3"

services:
  db:
    image: mariadb:10.5
    restart: always
    environment:
      - MYSQL_DATABASE=photoview
      - MYSQL_USER=photoview
      - MYSQL_PASSWORD=photosecret
      - MYSQL_RANDOM_ROOT_PASSWORD=1
    volumes:
      - /volume2/docker/photoview/db:/var/lib/mysql

  photoview:
    image: viktorstrate/photoview:2.4.0
    restart: always
    ports:
      - "8410:80"
    depends_on:
      - db

    environment:
      - PHOTOVIEW_DATABASE_DRIVER=mysql
      - PHOTOVIEW_MYSQL_URL=photoview:photosecret@tcp(db)/photoview
      - PHOTOVIEW_LISTEN_IP=photoview
      - PHOTOVIEW_LISTEN_PORT=80
      - PHOTOVIEW_MEDIA_CACHE=/app/cache

    volumes:
      - /volume2/docker/photoview/api_cache:/app/cache
      - /volume3/photo:/photos:ro
```
***
