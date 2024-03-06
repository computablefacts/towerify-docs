# Honeypots

Les honeypots déployés par AdversaryMeter ont pour objectif de :

- Catégoriser les attaques : manuelles vs automatisées, ciblées vs aléatoires, persistantes vs changeantes ;
- Catégoriser les attaquants : création de profils, suivi de l’activité, évaluation du niveau.

Ils ont été spécialement conçus pour être attractifs aux yeux d'attaquants humains. Les honeypots sont créés par groupe
de trois : un pour le protocole HTTP, un pour le protocole HTTPS et un pour le protocole SSH.

## Configuration des honeypots

Pour créer des honeypots :

1. Afficher le tableau de bord puis cliquer sur un des boutons "+ Configurer un honeypot" :
   ![](../img/adversarymeter/add-honeypot-1.png)

2. Choisir trois noms de domaines ou de sous-domaines __vous appartenant mais non utilisés__. Saisir ces noms de
   domaines ou de sous-domaines au-dessus du protocole désiré. Cliquer ensuite sur le bouton "étape suivante" pour
   continuer la configuration des honeypots.
   ![](../img/adversarymeter/add-honeypot-2.png)

3. Après quelques instants, les informations à ajouter à votre configuration DNS s'affichent :
   ![](../img/adversarymeter/add-honeypot-3.png)

4. Connectez-vous à la console d'administration de votre fournisseur de noms de domaines et configurez les DNS choisis
   précédemment en utilisant les informations affichées à l'écran.
   ![](../img/adversarymeter/add-honeypot-7.png)

5. Une fois la configuration DNS terminée, cliquer sur le bouton "terminer >" situé en bas à droite de l'écran :
   ![](../img/adversarymeter/add-honeypot-8.png)

6. La création des honeypots est alors lancée. En attendant que ceux-ci soient pleinement opérationnels, vous pouvez
   continuer utiliser AdversaryMeter pour surveiller vos actifs en cliquant sur le bouton "Accéder au tableau de bord".
   ![](../img/adversarymeter/add-honeypot-9.png)
