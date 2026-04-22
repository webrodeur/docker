![stirling](https://www.it-connect.fr/wp-content-itc/uploads/2024/05/Stirling-PDF-Fonctionnalites-800x294.jpg.webp)

## Sources web et Tutos liés au service
https://www.stirlingpdf.com/

https://mariushosting.com/how-to-install-web-pdf-on-your-synology-nas/

https://pdf.adminforge.de/?lang=fr_FR

https://blog.raspot.in/fr/blog/installation-et-configuration-de-stirling-pdf

https://docs.stirlingpdf.com/

https://github.com/Stirling-Tools/Stirling-PDF


## Explication du service
Stirling-PDF est une plate-forme Web de manipulation de PDF robuste, hébergée localement et optimisée par Docker. Cette application offre un large éventail de fonctionnalités, depuis les opérations de base telles que la fusion et le fractionnement de PDF jusqu'aux fonctionnalités avancées telles que la compression, l'OCR et les conversions.


## Docker Compose

```yaml
services:
  stirling-pdf:
    container_name: Stirling-PDF
    image: docker.stirlingpdf.com/stirlingtools/stirling-pdf
    mem_limit: 4g
    cpu_shares: 1024
    security_opt:
      - no-new-privileges:true
    healthcheck:
      test: timeout 10s bash -c ':> /dev/tcp/127.0.0.1/8080' || exit 1
      interval: 10s
      timeout: 5s
      retries: 3
      start_period: 90s
    ports:
      - 7890:8080
    volumes:
      - /volume2/docker/stirling/data:/usr/share/tessdata:rw # Required for extra OCR languages
      - /volume2/docker/stirling/config:/configs:rw
      - /volume2/docker/stirling/logs:/logs:rw
    environment:
     PUID: 1000
     PGID: 10
     DOCKER_ENABLE_SECURITY: true # or false
     SECURITY_ENABLELOGIN: true #or false
     SECURITY_INITIALLOGIN_USERNAME: webrodeur
     SECURITY_INITIALLOGIN_PASSWORD: fidesenclos 
     INSTALL_BOOK_AND_ADVANCED_HTML_OPS: false #or true
     SECURITY_CSRFDISABLED: true #or false
     SYSTEM_DEFAULTLOCALE: fr_FR # 
     UI_APPNAME: webrodeurPDF
     UI_HOMEDESCRIPTION: webrodeur PDF Description
     UI_APPNAMENAVBAR: webrodeur PDF
     SYSTEM_MAXFILESIZE: 5000 # Set the maximum file size in MB
     METRICS_ENABLED: true
     SYSTEM_GOOGLEVISIBILITY: false # or true
    restart: on-failure:5
```
