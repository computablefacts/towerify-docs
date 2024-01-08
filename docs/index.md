# Towerify

## Introduction

Towerify est une plateforme extensible et adaptée au déploiement de tout type d'applications. Towerify utilise des
méthodes éprouvées pour assurer le déploiement de vos applications les plus critiques, que celles-ci soient développées
en interne ou proviennent de notre [catalogue](cloud/catalog.md). En centralisant la gestion de vos serveurs, Towerify
simplifie le maintien en condition opérationnelle de votre système d'information.

L'objectif de Towerify est de simplifier la vie des développeurs et des administrateurs systèmes pour que ceux-ci
puissent se concentrer sur l'innovation et la création de valeur, en rendant simple le déploiement d'applications quel
qu'en soit l'environnement d'exécution. Avec Towerify, les développeurs et les administrateurs systèmes n'ont plus
besoin de perdre un temps précieux à automatiser les tâches de déploiement ou à devenir des experts des différents
fournisseurs d'infrastructure cloud ou bare metal.

## Le problème

Avec l'introduction continue de nouvelles réglementations telles la Réglementation Générale sur la Protection des
Données (RGPD), de nouvelles lois telles que la loi sur la cyberrésilience (CRA) et la mise en place de labels tels que
SecNumCloud, de plus en plus d'organisations font faces à un besoin croissant de déployer une même application dans de
nombreux environnements d'exploitations différents.

La multiplication de ces environnements et l'évolution rapide des besoins métiers oblige les organisations à déployer en
continu des mises à jour applicatives pour fournir aussi bien des patchs de sécurité que de nouvelles fonctionnalités
aux utilisateurs finaux.

Towerify permet à une organisation de s'assurer que ses ressources restent tournées vers l'innovation tout en conservant
la certitude que le code développé peut-être déployé partout où cela s'avèrerait nécessaire.

## La solution Towerify

Towerify est constitué de deux projets:

- [**Towerify Cloud**](cloud/overview.md) est l'application en charge de la gestion de l'infrastructure: provisionner
  des serveurs, déployer des applications du [catalogue](cloud/catalog.md), gérer l'accès aux applications, etc.
- [**Towerify CLI**](cli/getting-started.md) est une ligne de commande permettant de déployer des applications hors
  catalogue, i.e. développées par vos soins, au moyen d'un processus d'intégration continue.

!!! note

    Il n'y a aucune dépendance entre Towerify Cloud et Towerify CLI. L'utilisation de l'un n'implique pas l'utilisation 
    de l'autre.
