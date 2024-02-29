# Workflows

## Equipes

Une _équipe_ permet de fédérer des utilisateurs autours d'un ensemble d'actifs, i.e. des DNS ou des IPs, à surveiller.
Une équipe par défaut est automatiquement créée lors de l'activation de votre compte. Un même utilisateur peut
appartenir à une ou plusieurs équipes.

### Changement d'équipe

Pour afficher les actifs associés à une équipe, ouvrir le menu déroulant situé en haut à droite de l'écran. Sélectionner
ensuite l'équipe idoine. Les données affichées à l'écran sont alors mises à jour pour correspondre aux actifs associés à
l'équipe sélectionnée.

![](../img/adversarymeter/select-team.png)

??? note "Bon à savoir..."

    Il n'est actuellement pas possible d'afficher dans l'interface utilisateur l'ensemble des actifs appartenant à 
    plusieurs équipes simultanément. Cependant, il est possible de configurer un dashboard Superset permettant cela. 
    Pour en savoir plus, contacter <a href="mailto:engineering@computablefacts.com">engineering@computablefacts.com</a>.

### Création d'équipe

Pour créer une équipe :

- Ouvrir le menu déroulant situé en haut à droite de l'écran puis sélectionner l'entrée de menu "Créer équipe"
  ![](../img/adversarymeter/create-team-1.png)
- Saisir un nom d'équipe puis appuyer sur le bouton "Créer"
  ![](../img/adversarymeter/create-team-2.png)
- Si la création réussit, une équipe est ajoutée à la liste des "Equipes actuelles" en bas de l'écran ainsi qu'au
  menu situé en haut à droite de l'écran
  ![](../img/adversarymeter/create-team-3.png)

### Invitation d'utilisateur

Pour inviter un utilisateur à accéder aux données d'une équipe :

- Ouvrir le menu déroulant situé en haut à droite de l'écran puis sélectionner l'entrée de menu "Vos paramètres"
  ![](../img/adversarymeter/invite-user-1.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Equipes". Sélectionner ensuite l'équipe à laquelle vous
  souhaitez ajouter un utilisateur
  ![](../img/adversarymeter/invite-user-2.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Adhésions"
  ![](../img/adversarymeter/invite-user-3.png)
- Saisir l'email de l'utilisateur à inviter puis appuyer sur le bouton "Envoyer l'invitation"
  ![](../img/adversarymeter/invite-user-4.png)
- Si l'envoie de l'invitation réussit, un utilisateur est ajouté à la liste des "Invitations envoyées"
  ![](../img/adversarymeter/invite-user-5.png)
- Une fois l'invitation acceptée par l'utilisateur, son nom sera supprimé de la liste des "Invitations envoyées" pour
  être ajouté à la liste des "Membres de l'équipe"

### Annulation d'invitation

Pour annuler une invitation envoyée par erreur à un utilisateur :

- Ouvrir le menu déroulant situé en haut à droite de l'écran puis sélectionner l'entrée de menu "Vos paramètres"
  ![](../img/adversarymeter/invite-user-1.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Equipes". Sélectionner ensuite l'équipe à laquelle vous
  souhaitez ajouter un utilisateur
  ![](../img/adversarymeter/invite-user-2.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Adhésions"
  ![](../img/adversarymeter/invite-user-3.png)
- Dans la liste des "Invitations envoyées", sélectionner un utilisateur puis cliquer sur la "poubelle" qui apparaît à
  droite de son nom pour supprimer celui-ci
  ![](../img/adversarymeter/cancel-invite-user-4.png)

### Suppression d'utilisateur

Pour empêcher un utilisateur d'accéder aux données d'une équipe :

- Ouvrir le menu déroulant situé en haut à droite de l'écran puis sélectionner l'entrée de menu "Vos paramètres"
  ![](../img/adversarymeter/invite-user-1.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Equipes". Sélectionner ensuite l'équipe à laquelle vous
  souhaitez ajouter un utilisateur
  ![](../img/adversarymeter/invite-user-2.png)
- Dans le menu de gauche, sélectionner l'entrée de menu "Adhésions"
  ![](../img/adversarymeter/invite-user-3.png)
- Dans la liste des "Membres de l'équipe", appuyer sur la croix rouge pour révoquer l'accès aux données de l'équipe à
  l'utilisateur
  ![](../img/adversarymeter/remove-user-4.png)

## Actifs

Un _actif_ représente une adresse IP, une plage d'adresses IP ou un DNS vous appartenant. Il est possible d'importer de
nouveaux actifs de trois manières différentes :

- via un ajout manuel
- via une recherche de sous-domaine
- via un import CSV

!!! warning "Bon à savoir..."

    Les actifs ajoutés __ne sont pas__ automatiquement mis sous surveillance! La mise sous surveillance d'un actif est 
    une action à réaliser manuellement.

### Ajout manuel

Pour ajouter manuellement un actif :

- Sélectionner l'onglet "Mes actifs" puis cliquer sur le bouton "+ Ajouter un actif" en haut à droite de l'écran :
  ![](../img/adversarymeter/add-asset.png)
- Dans la liste déroulante, sélectionner l'option "Ajouter un domaine, un sous-domaine ou une adresse IP"
  ![](../img/adversarymeter/add-asset-manual-1.png)
- Saisir le domaine, le sous-domaine ou l'adresses IP que vous souhaitez ajouter à la liste de vos actifs puis cliquer
  sur le bouton "+ Ajouter"
  ![](../img/adversarymeter/add-asset-manual-2.png)
- En cas de succès, une notification s'affiche à l'écran. Il vous est alors possible d'ajouter un autre domaine ou de
  revenir à la liste de vos actifs en cliquant sur le lien "< revenir à mes actifs" en haut à droite de l'écran
  ![](../img/adversarymeter/add-asset-manual-3.png)
- L'actif ajouter est maintenant visible dans la liste de vos actifs
  ![](../img/adversarymeter/add-asset-manual-4.png)

### Recherche de sous-domaine

Pour rechercher un sous-domaine à partir d'un domaine racine :

- Sélectionner l'onglet "Mes actifs" puis cliquer sur le bouton "+ Ajouter un actif" en haut à droite de l'écran :
  ![](../img/adversarymeter/add-asset.png)
- Dans la liste déroulante, sélectionner l'option "Rechercher des sous-domaines à partir d'un TLD"
  ![](../img/adversarymeter/add-asset-from-tld-1.png)
- Saisir le domaine racine que vous souhaitez énumérer puis cliquer sur le bouton "Rechercher"
  ![](../img/adversarymeter/add-asset-from-tld-2.png)
- Après quelques instants de recherche (de 30s à 1mn), une liste de sous-domaines du domaine racine apparaît. Vous
  pouvez alors sélectionner le ou les domaines à importer puis cliquer sur le bouton "+ Ajouter" en bas à droite de
  l'écran pour ajouter ceux-ci à la liste de vos actifs. Si vous souhaitez importer l'ensemble des sous-domaines d'un
  coup, cocher la case située en haut à droite dans l'en-tête du tableau.
  ![](../img/adversarymeter/add-asset-from-tld-3.png)
- En cas de succès, vous serez automatiquement redirigé vers la liste de vos actifs. Les actifs ajoutés sont maintenant
  visibles dans cette liste.
  ![](../img/adversarymeter/add-asset-from-tld-4.png)

### Import CSV

L'import CSV permet d'importer plusieurs milliers d'actifs d'un coup. De plus, l'import CSV rend possible l'ajout en
masse d'__étiquettes__ :

- Sélectionner l'onglet "Mes actifs" puis cliquer sur le bouton "+ Ajouter un actif" en haut à droite de l'écran :
  ![](../img/adversarymeter/add-asset.png)
- Dans la liste déroulante, sélectionner l'option "Importer un fichier CSV"
  ![](../img/adversarymeter/add-asset-from-csv-1.png)
- Vous pouvez ensuite télécharger le modèle de fichier CSV proposé et remplir celui-ci. La première colonne du fichier
  DOIT contenir la liste des domaines, sous-domaines ou adresses IP à importer. La seconde colonne PEUT contenir des
  étiquettes (séparées par un `|`) à ajouter automatiquement aux actifs importés.
  ![](../img/adversarymeter/add-asset-from-csv-template-1.png)
  ![](../img/adversarymeter/add-asset-from-csv-template-2.png)
- Une fois le modèle remplit, il ne reste plus qu'à téléverser celui-ci en cliquant sur le bouton "Importer"
  ![](../img/adversarymeter/add-asset-from-csv-2.png)
- Une prévisualisation du fichier est alors proposée pour vous permettre d'en vérifier le contenu. Sélectionner
  l'ensemble des actifs en cochant la case située en haut à droite dans l'en-tête du tableau. Cliquer sur le bouton "+
  Ajouter" en bas à droite de l'écran pour lancer le processus d'import.
  ![](../img/adversarymeter/add-asset-from-csv-3.png)
- En cas de succès, vous serez automatiquement redirigé vers la liste de vos actifs. Les actifs ajoutés sont maintenant
  visibles dans cette liste.
  ![](../img/adversarymeter/add-asset-from-tld-4.png)