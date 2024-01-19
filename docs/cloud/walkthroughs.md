# Pas à pas

## Mise en place d'un environnement de développement avec Towerify CLI

[Towerify CLI](../cli/) est une ligne de commande permettant l'automatisation de la publication d'applications ad hoc
dans différents environnements.

1. Si vous n'en possédez pas déjà un, instanciez un nouveau serveur à l'aide de Towerify Cloud. Dans la suite, nous
   supposerons que les requêtes vers `*.acme.towerify.io` seront routées vers ce serveur.
   ![](../img/towerify-cloud-list-of-servers.png)
2. Téléchargez et installez ensuite Towerify CLI sur votre poste de travail à l'aide de la commande:
   ```bash
   curl -sL https://cli.towerify.io/install.sh | bash
   ```
   En cas de succès, le message suivant s'affiche à l'écran:
   ```output
   Towerify CLI est maintenant installé!

   Pour configurer votre identifiant et mot de passe, exécutez la commande :
       towerify configure
   ```
3. Vous allez maintenant devoir configurer Towerify CLI au moyen de la commande `towerify configure` pour être en mesure
   de vous connecter à votre instance:
   ```output
   ? Quel est le domaine associé à votre instance Towerify ?
   > acme.towerify.io
   
   ? Quel est votre identifiant Towerify ?
   > john.doe
   
   ? Quel est votre mot de passe Towerify ?
   (Par sécurité, les caractères que vous tapez ne s'afficheront à l'écran)
   >
   ```
   Si tout s'est bien passé, Towerify CLI confirme alors le succès de l'opération:
   ```output
   Tentative de connexion à votre instance Towerify... ==> Connexion réussie.
   
   Towerify CLI est maintenant configuré!
   
   Pour déployer une première application, rendez-vous dans le répertoire contenant celle-ci et exécutez la commande :
       towerify init
   ```
4. Déplacez-vous maintenant dans le répertoire de l'application que vous souhaitez déployer et exécutez la
   commande `towerify init` pour en paramétrer le déploiement:
   ```output
   ? Choisissez le nom de l'application à déployer ?
   > hello-world
   
   ? Sélectionnez le type d'application à déployer ?
   1) static
   2) laravel-10
   3) laravel-9
   > Votre choix : 1
   ```
   Si tout s'est bien passé, Towerify CLI confirme alors le succès de l'opération:
   ```output
   L'application hello-world est maintenant prête à être déployée!

   Vous pouvez maintenant déployer votre application en exécutant la commande :
       towerify deploy
   ```
5. Vous êtes maintenant prêt à déployer votre application en exécutant la commande `towerify deploy` dans le répertoire
   de l'application à déployer:
   ```output
   Déploiement de l'application hello-world en cours...
   
   L'application a été correctement déployée en dev!
   
   Vous pouvez maintenant accéder à votre application au moyen de cette URL :
       https://dev.hello-world.acme.towerify.io/
   ```
