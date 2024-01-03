# Fonctionnement

A l'origine, Towerify est né du besoins de déployer un produit en mode SaaS,
[AdversaryMeter](https://adversarymeter.io/), en appliance chez certains de nos clients. Après avoir évalué différentes
solutions du marché (allant de l'utilisation de scripts [Ansible](https://www.ansible.com/)
à [Cloudron](https://www.cloudron.io/) en passant par [Sandstorm](https://sandstorm.io/)) notre choix s'est porté
sur [YunoHost](https://yunohost.org/) pour deux raisons principales: sa configuration par défaut sensée et son
approche "[KISS](https://fr.wikipedia.org/wiki/Principe_KISS)" du packaging d'apps.

Cependant, à l'usage il s'avère que la console d'administration de YunoHost est mal adaptée à un contexte d'entreprise
où l'administration des différents composants techniques (provisionnement de l'infrastructure, gestion des utilisateurs,
déploiement des applications, etc.) est souvent réalisée par des personnes ou des équipes différentes.

Après avoir évalué nos besoins (par exemple la capacité à gérer un catalogue de serveurs ou encore la possibilité
d'administrer de manière centralisée plusieurs instances YunoHost), nous avons jugé préférable de développer une
nouvelle interface utilisateur plutôt que de forker la console d'administration actuellement mise à disposition
par la communauté YunoHost et de modifier celle-ci.

**Towerify permet donc de simplifier l'installation et l'administration de multiples instances YunoHost**. Il reste à
tout moment possible de déconnecter Towerify des instances administrées sans subir d'interruption de service. Towerify
est donc tout à fait adapté au déploiement et à la maintenance en condition opérationnelle d'applications dans un
environnement [Air Gap](https://en.wikipedia.org/wiki/Air_gap_(networking))!

## Architecture

Cette section donne un aperçu du fonctionnement de [Towerify Cloud](#towerify-cloud) et de
[Towerify CLI](#towerify-cli). Bien que cette vue d'ensemble contienne des approximations, l'objet est ici de donner une
image globale du fonctionnement de Towerify avant de détailler les différents aspects de l'architecture.

[**Towerify Cloud**](#towerify-cloud) est l'application en charge de la gestion de l'infrastructure: installer YunoHost,
configurer l'instance, déployer des [apps pré-packagées](/cloud/catalog), distribuer des accès aux apps, etc.

[**Towerify CLI**](#towerify-cli) est une ligne de commande permettant de déployer sur une instance YunoHost des
applications hors catalogue, i.e. développées par vos soins, au moyen d'un processus
d'[intégration continue](https://fr.wikipedia.org/wiki/Int%C3%A9gration_continue).

!!! note

    Il n'y a aucune dépendance entre Towerify Cloud et Towerify CLI. L'utilisation de l'un n'implique pas d'utiliser 
    l'autre.

### Towerify Cloud

![Schéma du fonctionnement de Towerify Cloud](/img/towerify-cloud.png)

### Towerify CLI

A venir.

## Sauvegardes

A venir.

## Sécurité

A venir.
