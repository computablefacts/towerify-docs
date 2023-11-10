# Application statique

Cet article vous explique les options que vous pouvez modifier pour changer le comportement
par défaut de Towerify pour votre application statique.

Le reste de ce document considère que le domaine principal de votre serveur Towerify 
est `acme.towerify.io` et que vous avez nommé votre application statique `my-app`.

Towerify a donc créé un fichier de configuration `.towerify.yaml` qui contient :

``` yaml 
name: my-app
type: static
```

C'est en modifiant ce fichier que vous pouvez changer le comportement de Towerify.

## Répertoire de vos fichiers statiques

Par défaut, Towerify considère que les fichiers statiques de votre application se 
trouvent dans le sous-répertoire `./src`.

Si vos fichiers se trouvent dans le sous-répertoire `./statique` vous pouvez modifier
la configuration de cette façon :

``` yaml 
name: my-app
type: static
config:
    webroot: ./statique 
```

!!! warning "TODO: cette option n'existe pas pour le moment"

## Environnements

Par défaut, Towerify publie votre application dans un environnement appelé `dev` (comme développement).
Votre application est publiée à la racine (`/`) du domaine `dev.my-app.acme.towerify.io`. Son URL est donc
`https://dev.my-app.acme.towerify.io/`.

### Ajouter un environnement

Vous pouvez publier votre application dans autant d'environnements que vous le souhaitez en précisant
le nom de l'environnement de cette façon :

``` bash
towerify deploy --env production
```

Dans l'exemple ci-dessus, l'application de votre environnement `production` aura l'URL 
`https://production.my-app.acme.towerify.io/`.

Donc, de façon générique, si vous ajouter un environnement `<env-name>` pour une application
`<app-name>` en déployant l'application avec `towerify deploy --env <env-name>` alors l'URL
de l'application sera `https://<env-name>.<app-name>.acme.towerify.io/`.

### Personnaliser l'URL d'un environnement

Si vous préférez publier `dev` avec l'URL `https://my-app.acme.towerify.io/dev/`, modifiez
la configuration de cette façon :

``` yaml 
name: my-app
type: static
config:
  envs:
    dev:
      domain: my-app.acme.towerify.io
      path: dev
```

!!! warning "Un environnement ne peut pas être contenu dans un autre" 

    Si votre environnement `production` a comme URL https://my-app.acme.towerify.io/ alors
    vous ne pouvez pas avoir l'environnement `dev` avec l'URL https://my-app.acme.towerify.io/dev/

Vous pouvez donc personnaliser le domaine et le chemin de l'URL. Le domaine peut être n'importe
quel sous domaine du domaine principal de votre serveur Towerify. Par exemple :

* `www.my-app.acme.towerify.io`
* `my-app.acme.towerify.io`
* `new-name.acme.towerify.io`
* `very.complicated.domain.for.my-app.acme.towerify.io`

Le chemin peut être n'importe quel chemin. Par exemple :

* dev
* my-app
* my-app/prod
* very/complicated/path/for/my-app

Vous pouvez paramétrer les domaines et les chemins de plusieurs environnements dans le fichier
de configuration. Par exemple :

``` yaml 
name: my-app
type: static
config:
  envs:
    dev:
      domain: dev.my-app.acme.towerify.io
      path: dev
    test:
      domain: dev.my-app.acme.towerify.io
      path: test
    prod:
      domain: my-app.acme.towerify.io
```

Vous aurez alors 3 environnements :

* `dev` avec l'URL `https://dev.my-app.acme.towerify.io/dev/`
* `test` avec l'URL `https://dev.my-app.acme.towerify.io/test/`
* `prod` avec l'URL `https://my-app.acme.towerify.io/`

### Avoir votre propre domaine

Vous pouvez avoir votre propre domaine également (contactez-nous, nous vous dirons comment
paramétrer votre DNS).

Imaginons que vous ayez le domaine `my-app.com` paramétré correctement, vous pouvez alors
utiliser n'importe quel sous domaine de ce domaine. Par exemple :

``` yaml 
name: my-app
type: static
config:
  envs:
    dev:
      domain: dev.my-app.acme.towerify.io
    v1:
      domain: v1.my-app.com
    v2:
      domain: v2.my-app.com
    preprod:
      domain: preprod.my-app.com
    prod:
      domain: my-app.com
```


## Personnalisation Dockerfile

Towerify génère une image par défaut qui permet de publier les pages statiques de votre application
sur un site Internet.

Cette image par défaut utilise [l'image Docker officielle](https://hub.docker.com/_/nginx) de 
[nginx](https://nginx.org/) depuis un `Dockerfile` comme celui-ci :

``` Dockerfile
FROM nginx
COPY ./src /usr/share/nginx/html
```

Vous pouvez avoir besoin de modifier cette image, par exemple, si vous voulez utiliser Apache plutôt
que nginx pour publier votre site statique. Dans ce cas, créer un fichier `Dockerfile` puis modifiez
la configuration de cette façon :

``` yaml 
name: my-app
type: static
config:
    dockerfile: ./towerify/Dockerfile
```

Changer nginx par apache n'est pas le meilleur exemple. Vous pouvez avoir besoin de modifier le
`Dockerfile` car vous avez besoin de générer les fichiers statiques de votre site avant de
pouvoir les publier. Ce serait le cas si vous utiliser Material for MkDocs pour écrire une documentation.
Dans ce cas, vous pouvez utiliser un `Dockerfile` de ce type :

``` Dockerfile
FROM python:3 AS build
WORKDIR /usr/src/app
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir mkdocs-material
COPY . .
RUN mkdocs build

FROM nginx AS publish
COPY --from=build /usr/src/app/site/ /usr/share/nginx/html/
```
