---
title: Prise en main de Brand Concierge
description: Prise en main de Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 6642acb3fdce2c9d3a9b919d5c9457191e4780a6
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 1.4.1 Prise en main de Brand Concierge

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

## Présentation d’1.4.1.1 Brand Concierge

Lors de la configuration de Brand Concierge, vous utiliserez principalement les 2 éléments suivants :

- **Compositeur d’agent (couche de configuration)**

  Objectif : principale plateforme d’interface utilisateur utilisée pour créer et configurer des expériences d’IA conversationnelle.

  Responsabilités clés :

   - Définir et gérer les sources de données et les bases de connaissances
   - Définir l’expression de la marque (ton, style, mécanismes de sécurisation)
   - Configurer l&#39;agent de réservation de réunion

- **Agent Orchestrator (moteur d’exécution)**

  Objectif : moteur de raisonnement et d’orchestration qui interprète les requêtes des utilisateurs et exécute les actions d’agent appropriées.

  Responsabilités clés :

   - Interprétation des modes d’utilisation du langage naturel
   - Générer et exécuter des plans de raisonnement en plusieurs étapes
   - Sélectionner et appeler les opérateurs/outils appropriés
   - Application du contexte, de la conformité et des mécanismes de sécurisation de la marque
   - Coordination de workflows à plusieurs agents
   - Agréger et composer des réponses provenant de plusieurs sources de données

- **Brand Concierge Conversation Runtime (Couche De Service)**

  Objectif : couche de service de conversation face au client qui gère les sessions de conversation, le contexte et les interactions du client.

  Composants clés :

   - Agent Web (client) : interface utilisateur de navigateur ou de conversation mobile intégrée à l’aide de Web SDK
   - Service de conversation (serveur principal) : gère l’état de la session et agit comme la passerelle d’orchestration

  Responsabilités clés :

   - Gérer les sessions utilisateur et les transcriptions de conversation
   - Gérer l’authentification des utilisateurs et des profils
   - Acheminer les messages entre le client et l’Agent Orchestrator
   - Conserver le contexte de conversation
   - Enregistrer les événements comportementaux et opérationnels dans AEP pour Analytics
   - Application de configurations spécifiques à une surface

## Configuration d’une instance 1.4.1.2 Brand Concierge

Pour commencer à créer votre propre instance Brand Concierge, procédez comme suit.

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Brand Concierge**.

![Brand Concierge](./images/bc1.png)

Vous devriez alors voir ceci. Cliquez sur le menu **sélection du sandbox**.

![Brand Concierge](./images/bc2.png)

Choisissez le sandbox qui vous a été affecté. Ce sandbox doit être nommé `--aepUserLdap--`.

![Brand Concierge](./images/bc3.png)

Cliquez sur **Commencer**.

![Brand Concierge](./images/bc4.png)

Pour le nom de votre instance Brand Concierge, utilisez : `--aepUserLdap-- - CitiSignal Brand Concierge`.

Saisissez le texte suivant sous **Que souhaitez-vous que le concierge fasse ?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

Cliquez sur **Créer**.

![Brand Concierge](./images/bc5.png)

Vous devriez alors voir ceci. Cliquez sur **Commencer** pour ajouter une source de connaissances.

![Brand Concierge](./images/bc6.png)

Sélectionnez **Liens de site web** puis cliquez sur **Continuer**.

![Brand Concierge](./images/bc7.png)

Vous devriez alors voir ceci. Saisissez `CitiSignal website` comme nom pour votre source de connaissances.

Vous devez maintenant télécharger un fichier csv contenant les liens de votre site Web. Téléchargez [le site Web CitiSignal lie le fichier CSV](./assets/citisignal-website-links.csv) sur votre bureau.

Cliquez sur **Parcourir les fichiers**.

![Brand Concierge](./images/bc8.png)

Ouvrez le fichier **citisignal-website-links.csv** et mettez à jour les liens pour qu’ils pointent vers votre propre site Web CitiSignal.

![Brand Concierge](./images/bc8a.png)

Sélectionnez le fichier **citisignal-website-links.csv** que vous venez de télécharger et de modifier. Cliquez sur **Ouvrir**.

![Brand Concierge](./images/bc9.png)

Votre fichier est maintenant ajouté à cette source de connaissances. Cliquez sur **Ajouter**.

![Brand Concierge](./images/bc10.png)

Vous devriez alors voir ceci. Cliquez sur **Ramener à la maison**.

![Brand Concierge](./images/bc11.png)

Vous devriez alors voir ceci. Cliquez sur **Commencer** dans la carte **Avis produit pour les consommateurs**.

![Brand Concierge](./images/bc12.png)



```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

```
Competitor pricing, competitor products
```

Vos mises à jour sont automatiquement enregistrées. Cliquez sur la **flèche** pour revenir à l’écran précédent.

![Brand Concierge](./images/bc13.png)

Vous devriez alors voir ceci. Cliquez sur **Commencer** pour personnaliser l’expression de votre marque.

![Brand Concierge](./images/bc14.png)

Vous pouvez effectuer vos propres choix sur la page **Expression de marque**.

![Brand Concierge](./images/bc15.png)

Faites défiler vers le bas et sélectionnez n’importe quel paramètre pour le champ **Longueur de la réponse**.

Vos mises à jour sont automatiquement enregistrées.

![Brand Concierge](./images/bc16.png)

Faites défiler l’écran vers le haut et cliquez sur la **flèche** pour revenir à l’écran précédent.

![Brand Concierge](./images/bc17.png)


Revenir à [Brand Concierge](./brandconcierge.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}