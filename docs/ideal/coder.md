# Comment coder l'outil Towerify CLI

## Architecture

### Installation de Towerify CLI

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

### Initialisation d'une application

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

### Déploiement d'une application

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


## CLI

Pour la partie CLI, nous pourrions faire un script bash et le faire
en utilisant [Bashly](https://bashly.dannyb.co/).

## Jenkins

Pour la partie automatisation (CI/CD), nous allons utiliser Jenkins.

Voir [ce billet](https://bootvar.com/how-to-create-jenkins-job-using-api/) 
pour la création d'un Job Jenkins grâce à son API.

## Une app YunoHost

Pour déployer Towerify CLI, nous voulons faire une app YunoHost.

C'est elle qui répondra pour l'installation (curl -L https://acme.towerify.io/cli/install.sh | sh).

!!! tip

    D'ailleurs, on pourrait y mettre la personnalisation Towerify (celle qui est dans cf_custom pour l'instant).

!!! question

    Peut-on faire en sorte que cette app installe (et configure) Jenkins et Portainer ? (et d'autres apps au
    fur et à mesure de nos besoins)