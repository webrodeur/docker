## Sites web pour Calibre-web


### Code docker pour Calibre

```yaml
services:
  calibre-web-automated:
    image: crocodilestick/calibre-web-automated:latest
    container_name: Calibre-WEB-AUTOMATED
    healthcheck:
      test: ["CMD-SHELL", "nc -z 127.0.0.1 8083 || exit 1"]
      interval: 10s
      timeout: 5s
      retries: 3
      start_period: 90s
    environment:
       PUID: 0
       PGID: 0
       TZ: Europe/Bucharest
    volumes:
      - /volume2/docker/autocalibreweb/config:/config:rw
      - /volume2/docker/autocalibreweb/ingest:/cwa-book-ingest:rw
      - /volume2/docker/autocalibreweb/library:/calibre-library:rw
    ports:
      - 8213:8083 
    restart: on-failure:5
```