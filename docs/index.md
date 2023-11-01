# Towerify

## C'est quoi ?

Towerify est notre tour de contrôle. 
Il facilite l'emballage, le déploiement et la réutilisation des applications et des services. 
Enregistrez votre application et regardez Towerify tout tenir à jour et en bonne santé.

Towerify met à votre disposition un ensemble d'outils vous permettant de publier vos applications
dans plusieurs environnements.

!!! warning "TODO"

    Lien vers une page décrivant les outils mis à disposition (Jenkins, phpMyAdmin, Portainer, etc).


## Objectif

Towerify vous permet d'automatiser la publication de votre application
dans 3 environnements en fonction du code que vous mettez à jour dans votre repo Git.


## Prérequis

Avoir le code de votre application dans une repo Git.

## Principe

Pour bénéficier de Towerify, vous devez ajouter un répertoire `towerify` à votre repo Git afin d'y mettre
les differents fichiers de configuration nécessaires pour packager, tester et publier votre application
avec Towerify.

Les grandes étapes du fonctionnement de Towerify sont :

* Towerify packagera votre application dans une image Docker. Vous devrez donc ajouter un `Dockerfile` à votre repo Git.
* Towerify publiera votre application grâce à Docker Compose. Vous devrez donc ajouter un `docker-compose.yaml` à votre repo Git.
* Towerify automatisera la création de l'image Docker et sa publication avec Docker Compose grâce à un pipeline Jenkins.
  Vous devrez donc ajouter un `Jenkinsfile` à votre repo Git.

## Et maintenant ?

Après cette présentation, vous vous dîtes certainement : 

> Très bien. Tout cela est intéressant mais je ne connais ni Docker, ni Jenkins, donc encore moins comment 
> écrire un `Dockerfile`, un `Jenkinsfile` ou un `docker-compose.yaml`.

Pas de panique, cette documentation de Towerify va vous guidez pas à pas pour créer les fichiers de configuration dont 
votre application va avoir besoin. Ces fichiers dépendent du type de votre application et nous avons une documentation
pour chacun des cas les plus courants :

* Mon application est [un ensemble de pages statiques](demarrage-rapide/app-statique.md)
* Mon application est [une API écrite en Python](demarrage-rapide/app-api-python.md)
* Mon application est écrite en PHP
* Mon application est écrite en PHP avec Laravel
