# Getting started

Déployer une nouvelle application grâce à Towerify

Outil en ligne de commande

## Installation CLI

``` bash
curl -L https://acme.towerify.io/cli/install.sh | sh
```

Towerify vous demande votre token d'accès :

``` bash
? Token ? RQEKeY6QHoM1YddR6JNNr4D8IyWBjKXf
```

Towerify confirme l'installation :

``` bash
towerify est maintenant installé et relié à votre instance Towerify acme.towerify.io
```

??? question "Comment on fait ça ?"

    - une application YunoHost qui déploie le /cli/ qui contient `install.sh` (et certainement d'autres fichiers)
    - grâce au domaine du `curl` on connait le client (acme)
    - install.sh peut vérifier le token auprès de l'app /cli/
    - install.sh télécharge le CLI et le stocke dans $HOME/.towerify (ce répertoire pourra contenir nos libraries 
      bash, un fichier de config avec l'URL du Towerify et le token(?), etc)


## Création de votre première application

Prérequis = être dans le répertoire d'une repo Git

``` bash
towerify init
```

``` bash
? Quel est le nom de votre application ?
> my-app
```

``` bash
? Quel est le type de votre application ?
   > Statique
     LEMP
```

``` bash
Création de l'application dans Towerify...
Création du fichier de configuration dans votre repo...

L'application a été créée avec succès.

Vous devez maintenant committer le fichier de configuration avec :
    git add .towerify.yaml
    git commit -m "Towerify initial configuration"

Puis déployer avec :
    git push
```




??? question "Choix de la repo ?"

    1. Traiter le cas où `towerify init` est exécuté à la racine d'une repo ?
    2. La commande a-t-elle besoin de créer des fichiers dans la repo ?
        1. si oui, il faudra laisser le client faire un commit. Donc si le client donne l'URL, il faudra faire 
           un `git clone` avant d'y mettre les fichiers
        2. si non, où stocker les réponses du client ? Juste les envoyer vers Towerify qui fera tout le reste ?
            1. Dans ce cas, comment faire pour modifier la conf de l'app après coup ? Towerify stocke la 
               conf de son côté et le CLI lui passe les nouveaux paramètres ?

    Cela semble plus simple de mettre le fichier de conf dans la repo. Par exemple `.towerify.yaml`.

    1. Towerify (Jenkins) lit ce fichier de conf pour savoir quoi faire ?
    2. Toute la conf se trouve dans ce fichier ou on peut personnaliser avec un répertoire /towerify ?
       Ce serait bien de pouvoir personnaliser le `Dockerfile` par exemple. Dans ce cas on ajoute une clé
       à la config du type `dockerfile: towerify/Dockerfile`
    
    Exemple de fichier de conf :
    
    Minimal :
    ``` yaml 
    name: my-app
    type: static
    ```

    Avec une conf spécifique :
    ``` yaml 
    name: my-app
    type: static
    config:
      webroot: ./src 
      dockerfile: ./towerify/Dockerfile
      domain: my-app.autre-domaine.com 
      envs:
      - dev
      - prod  
    ```

    !!! tip
        On peut lire un YAML avec groovy dans Jenkins, voir [ce billet SO](https://stackoverflow.com/a/56675940)
        ou la [doc (très réduite) de Jenkins](https://www.jenkins.io/doc/pipeline/steps/pipeline-utility-steps/#readyaml-read-yaml-from-files-in-the-workspace-or-text)




## Inspirations

### Fly

Docs : [Hands-on with Fly.io](https://fly.io/docs/hands-on/)
    
Commandes :

- install : `curl -L https://fly.io/install.sh | sh`
- create : `fly launch`
- deploy : `fly deploy`


### Lando

Docs : [Getting Started](https://docs.lando.dev/platformsh/getting-started.html)

Commandes :

- install : 
    ``` bash
    wget https://files.lando.dev/installer/lando-x64-stable.deb
    sudo dpkg -i lando-x64-stable.deb
    ```
- create : `lando init`
- deploy : `lando start`


### serverless

Docs : [Tutorial](https://www.serverless.com/framework/docs/tutorial)

Commandes :

- install : `npm install -g serverless`
- create : `serverless`
- deploy : `serverless deploy`

