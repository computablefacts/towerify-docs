# Getting started

Pour déployer une nouvelle application grâce à Towerify, vous devez utiliser notre
outil en ligne de commande.

## Installation de l'outil

``` bash
curl -L https://acme.towerify.io/cli/install.sh | sh
```

Towerify vous demande vos login et mot de passe :

``` output
Installation de Towerify pour l'instance acme.towerify.io

Pour vous authentifier auprès de Towerify, vous devez fournir votre login
et votre mot de passe.

? Quel est votre login Towerify ?
> 

? Quel est votre mot de passe Towerify ?
(Par sécurité, les caractères que vous tapez ne s'afficheront à l'écran)
> 
```

Towerify confirme l'installation :

``` output
Towerify CLI est installé

Il est configuré pour l'instance Towerify acme.towerify.io

Pour déployer votre première application, allez dans le répertoire de votre 
application et utilisez :
  towerify init
```

![towerify install](../img/towerify-install.gif)

??? question "Comment on fait ça ?"

    - une application YunoHost qui déploie le /cli/ qui contient `install.sh` (et certainement d'autres fichiers)
    - grâce au domaine du `curl` on connait le client (acme)
    - install.sh télécharge le CLI et le stocke dans $HOME/.towerify (ce répertoire contiendra aussi un fichier 
      de config avec l'URL du Towerify et le Token)

    Voir [le diagramme](coder.md#installation-de-towerify-cli).


## Initialisation de votre première application

Vous devez vous placer dans le répertoire de votre application avant de faire
la commande.

``` bash
towerify init
```

``` output
? Quel est le nom de votre application ?
> my-app
```

``` output
? Quel est le type de votre application ?
   > Statique
     LEMP
```

``` output
? Dans quel répertoire se trouvent les fichiers statiques [./src] ?
> 
```

``` output
Initialisation de l'application my-app dans Towerify...

L'application a été initialisée avec succès.

Vous pouvez maintenant déployer votre application avec :
    towerify app deploy
```




??? question "Choix de la repo ?"

    Nous avons décidé de pouvoir déployer des applications depuis un répertoire local sur
    le poste de l'utilisateur. Donc sans connaitre la repo Git, ni la repo d'un autre type
    ni même si ce répertoire est sous contrôle de source.

    Jenkins n'aura pas besoin de se connecter à la repo pour récupérer le code. Cela simplifie
    la configuration et cela permet de traiter le cas où la repo Git n'est accessible qu'en 
    interne à une entreprise (donc pas accessible par Jenkins).

    Pour que Jenkins puisse déployer le code, nous ferons un ZIP du répertoire que nous
    téléverserons à un Job Jenkins qui fera le déploiement.


??? question "Stockage de la configuration ?"

    Toute la configuration de Towerify pour l'application sera stockée dans le fichier `.towerify.yaml`
    dans le répertoire où la commande `towerify init` a été lancée.

    Ce fichier de configuration fera partie du ZIP transmis à Jenkins donc le Job Jenkins adaptera son
    comportement en fonction de cette configuration.

    Exemple de fichier de conf minimal :
    ``` yaml 
    name: my-app
    type: static
    ```

    Pour les cas plus complexes, le fichier de conf pourra référencer un fichier externe stocké dans le
    répertoire de l'application comme, par exemple, un `Dockerfile` spécifique.

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


## Déploiement de votre application

Vous devez vous placer dans le répertoire de votre application avant de faire
la commande.

``` bash
towerify app deploy
```

``` output
Déploiement de l'application my-app en cours...
Application correctement déployée en prod.

Vous pouvez accéder à votre application avec :
https://dev.my-app.acme.towerify.io/
```

!!! failure "Pas de fichier `.towerify.yaml`"

    Si le fichier de configuration n'existe pas, on affiche une erreur :
    ``` output
    Impossible de publier une application depuis ce répertoire.
    Vous devez d'abord initialiser votre application avec :
        towerify init
    ```


??? question "Comment on fait ça ?"

    - durant l'installation, Towerify CLI a stocké l'URL de l'instance et le token de Jenkins
    - on zippe le répertoire
    - on envoie le zip au Job Jenkins
    - Jenkins déploie en fonction du fichier de conf `.towerify.yaml`

    Voir [le diagramme](coder.md#deploiement-dune-application).



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

