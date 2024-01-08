# Fonctionnement

Ce document détail comment les commandes émises par Towerify Cloud circulent dans le système. Plus spécifiquement, ce
document couvre:

- Les catalogues de serveurs, d'apps et de permissions ainsi que leur utilité respective ;
- Le mécanisme d'émission des commandes par [la tour de contrôle](#la-tour-de-contrle).
- Le mécanisme d'exécution des commandes par [les hôtes](#les-htes).

Il est fortement conseillé de jeter un oeil au [diagramme d'architecture](overview.md#diagramme-darchitecture) de
Towerify Cloud avant de se lancer dans la lecture de ce document.

## La tour de contrôle

La tour de contrôle permet de provisionner de l'infrastructure, d'appliquer des mises à jour d'OS et de déployer des
applications via l'intermédiaire de commandes envoyées à des agents en charge d'exécuter celles-ci.

La tour de contrôle opère sur quatre types d'entités:

- Les __applications__ qui sont des programmes développés en interne ou provenant de
  notre [catalogue](archive/catalog.md) et servant à résoudre un problème métier ou technique ;
- Les __serveurs__ qui sont des machines physiques ou virtuelles à laquelle Towerify Cloud se connecte pour exécuter des
  commandes ;
- Les __utilisateurs__ qui opèrent Towerify Cloud ou utilisent les applications déployées ;
- Les __permissions__ qui permettent aux utilisateurs d'accéder aux applications déployées sous certaines conditions.

Ces entités sont regroupées au sein de catalogues permettant d'administrer celles-ci aisément:

- Le __catalogue de serveurs__ permet de lister le matériel disponible et de tracer les commandes exécutées, en cours
  d'exécution ou en attente d'exécution sur un serveur donné ;
- Le __catalogue d'applications__ permet de lister les applications déployées ou prêtes au déploiement et d'établir la
  liste des utilisateurs ayant accès à une application spécifique ;
- Le __catalogue d'utilisateurs__ permet de lister les utilisateurs du système et d'attribuer ou de révoquer les
  permissions d'accès d'un utilisateur particulier.

??? note "Bon à savoir..."

    Towerify Cloud est une application [multi-tenant](https://en.wikipedia.org/wiki/Multitenancy) et peut donc être 
    configurée pour être utilisée par plusieurs organisations simultanément.

## Les hôtes

Les hôtes sont des serveurs physiques ou virtualisés appartenant à une organisation. Ils permettent d'exécuter des
commandes émises par la tour de contrôle pour déployer de nouvelles applications ou mettre à jour le système
d'exploitation.

??? note "Bon à savoir..."

    Il n'est pas nécessaire que la tour de contrôle soit connectée à un hôte pour que celui-ci fonctionne! En effet, il 
    est tout à fait possible de déployer une ou plusieurs applications à l'aide de la tour de contrôle puis de couper 
    l'accès à l'hôte sans pour autant que les applications déployées ne cessent de fonctionner :-)

??? warning "Contraintes..."

    Les hôtes provisionnés par l'organisation doivent avoir [Linux Debian](https://www.debian.org/) pour système 
    d'exploitation. Les hôtes doivent être configurés pour être accessibles en SSH par la tour de contrôle. Lors de 
    l'enregistrement d'un hôte auprès de la tour de contrôle, celui-ci sera reformaté pour utiliser la distribution
    [YunoHost](https://yunohost.org/) basée sur Linux Debian.

## Orchestration des changements

A venir.

## Application des changements

A venir.