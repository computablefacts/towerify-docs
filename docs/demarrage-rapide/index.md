# Publier votre première application

Cet article explique comment déployer une application de type statique. 

C'est le type le plus simple : l'application est un ensemble de pages Internet (HTML, CSS, JS, etc)
que vous souhaitez publier pour la rendre accessible à vos utilisateurs grâce à une URL
du type https://my-app.acme.towerify.io/.

??? warning "TODO: une application exemple"

    Nous pourrions créer une repo exemple avec une application statique.
    Notre client pourrait alors la cloner sur son PC puis dérouler cette procédure
    pour la publier sur son Towerify

    Ce pourrait être une app TODO list comme
    [comme celle-ci](https://www.w3schools.com/howto/howto_js_todolist.asp).



## Installation de l'outil

``` bash
curl -sL https://acme.towerify.io/cli/install.sh | bash
```

Towerify télécharge et installe notre outil en ligne de commande :

``` output
Installation de Towerify pour l'instance acme.towerify.io
##################################################################### 100,0%
```

Towerify confirme l'installation :

``` output
Towerify CLI est installé pour l'instance acme.towerify.io

Pour le configurer avec vos login et mot de passe, utilisez :
  towerify configure
```

!!! tips

    Ajoutez votre propre domaine Towerify au bout de la commande. Par exemple, si votre domaine
    est my-corp.towerify.io, faîtes :

    ``` bash
    curl -sL https://acme.towerify.io/cli/install.sh | bash -s -- my-corp.towerify.io
    ```

??? question "Comment on fait ça ?"

    - une application YunoHost qui déploie le /cli/ qui contient `install.sh` et l'application 
      Towerify CLI compressée (towerify.tar.gz)
    - le domaine peut être passé à `install.sh`
    - `install.sh` télécharge le CLI et le stocke dans $HOME/.towerify (ce répertoire contiendra aussi un fichier 
      de config avec l'URL du Towerify et les credentials)
    - `install.sh` ajoute `towerify` dans le PATH de l'utilisateur

    Voir [`install.sh`](../develop/coder.md#installsh) et [le packaging](../develop/coder.md#packaging).

## Configuration des paramètres d'accès

``` bash
towerify configure
```

Towerify vous demande votre domaine, votre login et votre mot de passe :

``` output
? Quel est le domaine de votre Towerify ?
> acme.towerify.io

? Quel est votre login Towerify ?
> 

? Quel est votre mot de passe Towerify ?
(Par sécurité, les caractères que vous tapez ne s'afficheront à l'écran)
> 
```

Towerify confirme l'installation :

``` output
Tentative de connexion à Towerify... ==> Connexion réussie.

Towerify CLI est correctement configuré pour l'instance Towerify acme.towerify.io

Pour déployer votre première application, allez dans le répertoire de votre 
application et utilisez :
  towerify init
```

!!! tips

    Vous pouvez donner vos paramètres d'accès directement dans la commande :

    ``` bash
    towerify configure --domain my-corp.towerify.io --login user --password P@ssw0rd
    ```


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
? Choissisez le type de votre application ?
1) static
2) laravel
Votre choix : 1

```

``` output
Application my-app initialisée

Vous pouvez maintenant déployer votre application avec :
    towerify deploy
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

    Toute la configuration de Towerify pour l'application sera stockée dans le fichier `towerify/config.yaml`
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
Application correctement déployée en dev.

Vous pouvez accéder à votre application avec :
https://dev.my-app.acme.towerify.io/
```

Vous pouvez visiter le lien fourni par Towerify (https://dev.my-app.acme.towerify.io/)
pour afficher votre application dans votre navigateur.

??? failure "Pas de fichier `towerify/config.yaml`"

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
    - Jenkins déploie en fonction du fichier de conf `towerify/config.yaml`

    Voir [le détail](develop/coder.md#towerify-deploy).


## Et maintenant ?

Vous pouvez personnaliser la configuration de votre [application statique](app-statique.md).
