# Variables Towerify

Dans la plupart des fichiers de configuration de Towerify, vous pouvez utiliser
des variables qui seront remplacées par leur valeur au moment de l'utiilisation
du fichier par Towerify.

## Fichier `docker-compose.yaml`

`__DOCKER_IMAGE_NAME__`

:   Le nom de l'image Docker de votre application générée par Jenkins.

    Par défaut les images Docker produites par Towerify sont stockées sur notre registry
    Docker Hub. L'image aura un nom du type : `computablefacts/customer-my-app`.

`__DOCKER_IMAGE_TAG__`

:   Le tag de l'image Docker. Ce tag est généré par le pipeline Jenkins a chaque déploiement
    de votre application par Towerify. En changeant ce tag, Jenkins déclenche la mise à jour
    de votre application.

    Le tag aura une valeur du type : `twr-jenkins-my-app-develop-15`.

`__PORT__`

:   Le port interne que Towerify a attribué à votre application.

    Ce port est utilisé pour exposer le container de votre application.

Exemple :

``` yaml hl_lines="4 8"
version: "3"
services:
  myapp:
    image: __DOCKER_IMAGE_NAME__:__DOCKER_IMAGE_TAG__
    ports:
    - target: 80
      host_ip: 127.0.0.1
      published: "__PORT__"
      protocol: tcp
      mode: host
``` 


