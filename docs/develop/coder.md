# Comment coder Towerify CLI

## Idéal

Nous avons écrit cette documentation en ayant en tête un démarrage idéal pour nos clients.

C'est-à-dire un démarrage :

- qui leur permet d'être opérationel le plus rapidement possible
- sans avoir besoin de connaître les composants utilisés par Towerify (Docker, Jenkins, etc)
- sans avoir besoin de configurer manuellement ces composants


## CLI

Pour la partie CLI, nous allons utiliser [Bashly](https://bashly.dannyb.co/) qui va gérer pour nous
les commandes, les options, l'affichage de l'aide, etc.

Nous avons besoin de coder 2 scripts :

- `install.sh` qui sera téléchargé par le client grâce à un `curl`
- `towerify` qui sera l'outil principal permettant de piloter le déploiement des applications
  grâce à ses commandes (`towerify init`, `towerify deploy`)

Les 2 applications se trouvent dans la même repo :

[https://github.com/computablefacts/towerify-cli](https://github.com/computablefacts/towerify-cli)


### `install.sh`

!!! warning "Le diagramme ci-dessous doit être mis à jour"

``` mermaid
sequenceDiagram
  autonumber
  box Local PC
    participant User
    participant Install as Install.sh
    participant CLI
  end

  box Towerify
    participant AppCLI as CLI App
    participant Jenkins
  end

  par curl -L https://acme.towerify.io/cli/install.sh | sh
    User ->> AppCLI: Installe Towerify CLI
    AppCLI ->> Install: Télécharge install.sh

    Install ->> User: Demande le token Jenkins
    User ->> Jenkins: Se connecte à Jenkins avec ses login/pwd
    Jenkins ->> User: Récupère son Token
    User ->> Install: Donne le Token Jenkins

    Install ->> CLI: Copie towerify
    Install ->> CLI: Stocke l'URL et le Token
  end
```


* [X] Vérifie que `towerify` n'est pas déjà installé
* [X] Demande le login Towerify
* [X] Demande le password Towerify
* [X] Vérifie la connexion au Jenkins => si non, affiche une erreur
* [ ] Télécharge le package et le décompresse dans le répertoire d'installation
    * Pour l'instant, copie le fichier towerify depuis la repo locale
* [X] Ajoute `towerify` dans le PATH
* [X] Stocke les paramètres dans `config.ini`

### `towerify`

#### `towerify --help`

Codé automatiquement par Bashly :-)

#### `towerify version`

Codé automatiquement par Bashly :-)

#### `towerify init`

``` mermaid
sequenceDiagram
  autonumber
  box Local PC
    participant User
    participant CLI
    participant App as App directory
  end

  box Towerify
    participant AppCLI as CLI App
    participant Jenkins
  end

  par towerify init
    User ->> CLI: towerify init

    CLI ->> User: Demande le nom de l'application
    CLI ->> User: Demande le type de l'application

    CLI ->> App: Crée le fichier de config .towerify.yaml
  end
```

* Pose 2 questions :
    * [X] Nom de l'app
    * [X] Type de l'app
        * 2 types affichés et un seul géré par `towerify deploy`
            * [X] Supprimer le type "en trop" pour ne garder que `static`
* [X] Crée le fichier de configuration `.towerify.yaml`
* [X] Gère le cas où un fichier de configuration existe déjà => affiche une erreur

Les options possibles de `.towerify.yaml` dépendent du type d'app. Ca pourrait être
instéressant d'avoir une commande qui ajoute toutes les options possibles (avec leur
valeur par défaut ou des valeurs exemples et des commentaires pour les expliquer) 
afin que l'utilisateur n'est pas besoin de lire cette doc pour les trouver.

* [ ] Ajouter une option `--add-all-options` pour faire ça

#### `towerify deploy`

!!! warning "Le diagramme ci-dessous doit être mis à jour"

``` mermaid
sequenceDiagram
  autonumber
  box Local PC
    participant User
    participant CLI
    participant App as App directory
  end

  box Towerify
    participant AppCLI as CLI App
    participant Jenkins
  end

  par towerify deploy
    User ->> CLI: towerify deploy

    CLI ->> Jenkins: Lance le Job de création de domaine (my-app.acme.towerify.io)
    CLI ->> App: Compresse le répertoire de l'app
    CLI ->> Jenkins: Envoi le fichier compressé au Job Jenkins
    CLI ->> Jenkins: Attend la fin du Job
    CLI ->> User: Affiche l'URL de l'app
  end
```

* [ ] Vérifie qu'il a bien accès au Jenkins (credentials dans le fichier `config.ini`) => Affiche une erreur
* [ ] Créer le pipeline Jenkins s'il n'existe pas
* [ ] Compresse le répertoire de l'app (crée un fichier .tarignore qui permettra de ne pas compresser des 
      fichiers ou des répertoires, comme `.git`)
* [ ] Lance le job Jenkins en lui envoyant le fichier compressé
* [ ] Surveille l'avancement du job Jenkins (API toutes les 5 secondes, afficher le numéro de build)
* [ ] Affiche le résultat : succès ou échec
* [ ] Affiche les URL : lien vers l'app déployée, lien vers le détail du job Jenkins en cas d'échec      
* [ ] Ajouter l'option `--env` pour pouvoir déployer autant d'environnement que nécessaire. `dev` par défaut
    * [ ] Avertissement si on déploie dans un environnement autre que `dev` pour la première fois (permet 
          d'éviter les erreurs comme `--env prod` puis `--env production`)
    * [ ] On sait si un environnement a déjà été déployé en vérifiant l'existance du job Jenkins 
          correspondant (`<app_name>_<app_type>`).

#### `towerify delete`

Supprime une application pour un environnement donné. Exemple :

``` bash
towerify delete --env my_feature
```

* [ ] Demande confirmation (sauf si option `--force`)
* [ ] Supprime l'application (de YunoHost). Nécessitera un pipeline Jenkins pour le faire car `towerify`
      ne peut pas agir sur YunoHost directement.
* [ ] Supprime le job Jenkins de déploiement (`<app_name>_<app_type>`) et le job Jenkins de suppression
      crée à l'étape précédente

#### `towerify destroy`

Supprime tous les environnements de l'application et tous les jobs Jenkins de l'application.

``` bash
towerify destroy
```

* [ ] Demande confirmation (sauf si option `--force`)
* [ ] Supprime toutes les applications (de YunoHost). Nécessitera un pipeline Jenkins pour le faire car `towerify`
      ne peut pas agir sur YunoHost directement.
      On peut lister les apps car leur ID YunoHost commence par <app_name>.
* [ ] Supprime tous les jobs Jenkins (nom commençant par `<app_name>_`).

#### `towerify update`

Permet de mettre à jour `towerify`

* [ ] Télécharge le package sur le Towerify (app /cli) et la décompresse dans un répertoire temporaire
* [ ] Compare la version de ce package et avec celle qui est installée
* [ ] Si la version est la même (ou celle installée supérieure à celle du Towerify) => message Towerify est à jour
* [ ] Si la version est plus récente, remplace le `towerify` installé par le nouveau (avec les templates)

#### `towerify configure`

Permet de changer la configuration de son Towerify CLI i.e. modifier l'URL, le login et le pwd du serveur Towerify
avec lequel Towerify CLI va interagir.

* [ ] Avertissement : si l'utilisateur change de serveur, il va perdre sa conf actuelle
* [ ] Poser les questions : URL Towerfiy, login, pwd
* [ ] Vérifier la connexion au Jenkins
* [ ] Mettre à la `config.ini` avec les nouveaux paramètres

Dans un deuxième temps, nous pourrions gérer plusieurs serveurs Towerify avec, comme AWS CLI, une notion de
profil.

* [ ] Ajouter un paramètre `--profile`
* [ ] Si le paramètre n'est pas passé, on change les credentials par défaut
* [ ] Si le paramètre est passé, on crée ou on modifie les credentials de ce profile

Le fichier `config.ini` ressemblerait alors à ça :

``` ini
jenkins_domain = jenkins.myapps.addapps.io
towerify_domain = myapps.addapps.io
towerify_login = cfadmin
towerify_password = **********

[ista]
jenkins_domain = jenkins.apps.ista.computablefacts.com
towerify_domain = apps.ista.computablefacts.com
towerify_login = pbrisacier
towerify_password = **********

```

* [ ] Il faudra ajouter l'option `--profile` aux commandes de `towerify` pour en tenir compte


### Packaging

L'idée : faire une application YunoHost qui permettra à un utilisateur du YunoHost de télécharger
Towerify CLI.

Une fois cette app installé sur un YunoHost, le client peut faire la commande :

``` bash
curl -L https://acme.towerify.io/cli/install.sh | sh
```

* Adapter le script `build.sh` à la racine de la repo `towerify-cli` pour : 
    * [X] générer `install.sh` et `towerify` en mode production
    * [ ] packager (met dans un tar.gz ou un zip) `towerify` et ses fichiers (templates Jenkins pour l'instant)
    * [ ] mettre le tout dans un répertoire `./build`

* Créer une repo `towerify_cli_ynh` pour :
    * [ ] déployer un site statique sur le domaine principal du YunoHost et le répertoire `/cli` par défaut
    * [ ] mettre les fichiers buildés de `towerify-cli` :
        * [ ] `install.sh` (en utilisant le templating afin de mettre en place le domaine du YunoHost)
        * [ ] le fichier tar.gz

!!! tip

    D'ailleurs, on pourrait y mettre la personnalisation Towerify (celle qui est dans cf_custom pour l'instant).

!!! question

    Peut-on faire en sorte que cette app installe (et configure) Jenkins et Portainer ? (et d'autres apps au
    fur et à mesure de nos besoins)

### Etapes pour ajouter un nouveau type d'application

* L'ajouter dans la liste des types possibles de `towerify init`
* Faire un nouveau template Jenkins qui va gérer le déploiement du type
    * Copier le template d'un type existant
    * Modifier la partie pipeline
        * Changer le Dockerfile et le docker-compose.yaml générés
        * Prendre en charge les options spécifiques à ce type
* A priori `towerify deploy` n'a pas besoin d'être modifié (il cherche le template
  Jenkins en fonction du type du fichier de config, il crée le pipeline Jenkins avec
  `<app_name>_<app_type>`)
* Mettre à jour cette doc pour décrire le nouveau type et ses options

## Jenkins

Pour la partie automatisation (CI/CD), nous allons utiliser Jenkins.

Voir [ce billet](https://bootvar.com/how-to-create-jenkins-job-using-api/) 
pour la création d'un Job Jenkins grâce à son API.

Pour le pipeline Jenkins du type `static`, j'ai dû installer des plugins :

- [File Parameter](https://plugins.jenkins.io/file-parameters/) pour pouvoir passer le fichier compressé
  en paramètre du pipeline
- [Pipeline Utility Steps](https://plugins.jenkins.io/pipeline-utility-steps/) pour avoir readYaml (et 
  d'autres truc qui seront peut-être utile)

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
