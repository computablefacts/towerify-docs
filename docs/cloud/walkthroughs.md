# Pas à pas

## Mise en place d'un environnement de développement avec Towerify CLI

[Towerify CLI](../cli/) est une ligne de commande permettant l'automatisation de la publication d'applications ad hoc
dans différents environnements.

1. Si vous n'en possédez pas déjà un, instanciez un nouveau serveur à l'aide de Towerify Cloud. Dans la suite, nous
   supposerons que les requêtes HTTP/HTTPS à destination de `*.acme.towerify.io` seront routées vers ce serveur.
   ![](../img/towerify-cloud-list-of-servers.png)
2. Téléchargez et installez Towerify CLI sur votre poste de travail :
   ```console
   $ curl -sL https://cli.towerify.io/install.sh | bash
   
   Towerify CLI est maintenant installé!
   
   Pour configurer votre identifiant et mot de passe, exécutez la commande :
      towerify configure
   ```
3. Vous allez maintenant devoir configurer Towerify CLI pour être en mesure de vous connecter à votre instance :
   ```console
   $ towerify configure
   
   ? Quel est le domaine associé à votre instance Towerify ?
   > acme.towerify.io
   
   ? Quel est votre identifiant Towerify ?
   > john.doe
   
   ? Quel est votre mot de passe Towerify ?
   (Par sécurité, les caractères que vous tapez ne s'afficheront à l'écran)
   >
   ```
   Quand l'opération de configuration se déroule avec succès, le message suivant s'affiche alors à l'écran :
   ```console
   Tentative de connexion à votre instance Towerify... ==> Connexion réussie.
   
   Towerify CLI est maintenant configuré!
   
   Pour déployer une première application, rendez-vous dans le répertoire contenant celle-ci et exécutez la commande :
       towerify init
   ```
   Dans le cas contraire, un message d'erreur s'affiche.
4. Créez un répertoire `hello-world/` et déplacez-vous dans celui-ci :
   ```bash
   $ mkdir hello-world
   $ cd hello-world/
   ```
   Créez ensuite dans ce répertoire un fichier `index.html` dont le contenu est le suivant :
   ```html
   <!DOCTYPE html>
   <html>
       <head>
           <title>Example</title>
       </head>
       <body>
           <p>This is an example of a simple HTML page with one paragraph.</p>
       </body>
   </html>
   ```
5. Vous allez maintenant devoir configurer le processus de déploiement de cette page web :
   ```console
   $ towerify init
   
   ? Choisissez le nom de l'application à déployer ?
   > hello-world
   
   ? Sélectionnez le type d'application à déployer ?
   1) static
   2) laravel-10
   3) laravel-9
   > Votre choix : 1
   ```
   Quand l'opération de configuration se déroule avec succès, le message suivant s'affiche alors à l'écran :
   ```console
   L'application hello-world est prête à être déployée!

   Vous pouvez maintenant déployer celle-ci en exécutant la commande :
       towerify deploy
   ```
   Dans le cas contraire, un message d'erreur s'affiche.
6. Vous êtes maintenant prêt à déployer votre application :
   ```console
   $ towerify deploy
   
   Déploiement de l'application hello-world en cours...
   
   L'application a été déployée en dev avec succès!
   
   Votre application est accessible ici :
       https://dev.hello-world.acme.towerify.io/
   ```
7. Pour terminer, rendez-vous à l'adresse `https://dev.hello-world.acme.towerify.io` à l'aide de votre navigateur.
   Vous devriez y apercevoir la page HTML créée lors de l'étape 4.