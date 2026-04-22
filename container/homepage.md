![homepage](https://gethomepage.dev/assets/homepage_demo_clip.webp)
## Sources web et Tutos liés au service


## Explication du service
Homepage Un tableau de bord d'application moderne, entièrement statique, rapide, sécurisé, entièrement proxy et hautement personnalisable avec des intégrations pour plus de 100 services et des traductions dans plusieurs langues. Facilement configurable via des fichiers YAML ou via la découverte d'étiquettes Docker.

## Docker Compose
```yaml
version: "3.3"
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    ports:
      - 3000:3000
    volumes:
      - /volume2/docker/homepage/config:/app/config # Chemin pour les fichiers de configuration
      - /volume2/docker/homepage/images:/app/public/images # Chemin pour stocker les images et icônes
      - /var/run/docker.sock:/var/run/docker.sock:ro # Intégration Docker (optionnel)
    environment:
      PUID: 1000 # ID utilisateur (non-root)
      PGID: 10 # ID groupe (non-root)
      HOMEPAGE_ALLOWED_HOSTS: 192.168.1.106:3000 # Remplacez par l'URL de votre instance
    restart: unless-stopped
```
