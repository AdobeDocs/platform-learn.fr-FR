---
title: Prise en main de Brand Concierge
description: Prise en main de Brand Concierge
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: 1f4b945658834b7fd4f52f297fe761c49edd28fe
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 1%

---

# 1.4.1 Prise en main de Brand Concierge

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

Choisissez le sandbox qui vous a été affecté. Ce sandbox doit être nommé `--aepUserLdap-- - bc`.

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

Vous devriez alors voir ceci. Renseignez les champs suivants à l’aide du texte ci-dessous.

**Que doit savoir le concierge sur le produit ou le public avant de faire des recommandations ?**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**Existe-t-il des règles ou des limites que le concierge doit respecter lorsqu’il formule des recommandations ?**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**Existe-t-il des mots-clés ou des expressions spécifiques que le concierge doit suivre ou éviter ?**

```
Competitor pricing, competitor products
```

Vos mises à jour sont automatiquement enregistrées. Cliquez sur la **flèche** pour revenir à l’écran précédent.

![Brand Concierge](./images/bc13.png)

Vous devriez alors voir ceci. Cliquez sur **Commencer** pour personnaliser l’expression de votre marque.

![Brand Concierge](./images/bc14.png)

Vous pouvez effectuer vos propres choix sur la page **Expression de marque** et vérifier qu’une option est sélectionnée pour chaque question.

![Brand Concierge](./images/bc15.png)

Faites défiler vers le bas et sélectionnez n’importe quel paramètre pour le champ **Longueur de la réponse**.

Vos mises à jour sont automatiquement enregistrées.

![Brand Concierge](./images/bc16.png)

Faites défiler l’écran vers le haut et cliquez sur la **flèche** pour revenir à l’écran précédent.

![Brand Concierge](./images/bc17.png)

Tu seras de retour ici. Cliquez sur **Sources de connaissances**.

![Brand Concierge](./images/bc18.png)

Cliquez sur **Créer vos sources de connaissances**.

![Brand Concierge](./images/bc19.png)

Sélectionnez **Catalogue de produits** puis cliquez sur **Continuer**.

![Brand Concierge](./images/bc20.png)

Vous devriez alors voir ceci. Saisissez `CitiSignal Products` comme nom pour votre source de connaissances.

![Brand Concierge](./images/bc21.png)

Vous devez maintenant télécharger un fichier csv contenant les liens de votre site Web. Téléchargez le [catalogue de produits CitiSignal](./assets/CitiSignal-catalog.json.zip) sur votre bureau et décompressez-le.

![Brand Concierge](./images/bc26.png)

Cliquez sur **Parcourir les fichiers** puis sélectionnez **Parcourir sur votre appareil**.

![Brand Concierge](./images/bc22.png)

Sélectionnez le fichier **CitiSignal-catalog.json** et cliquez sur **Ouvrir**.

![Brand Concierge](./images/bc23.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter**.

![Brand Concierge](./images/bc24.png)

Tu seras de retour ici.

![Brand Concierge](./images/bc25.png)

Après 10 à 20 minutes, le **Statut** des deux sources de connaissances doit être **Terminé**. Cliquez sur **Accueil**.

![Brand Concierge](./images/bc27.png)

Vous devriez alors voir ceci. Cliquez sur **+ Connexion** sur la carte **Liens de site web**.

![Brand Concierge](./images/bc28.png)

Sélectionnez la source de connaissances **Site Web CitiSignal** et cliquez sur **Enregistrer**.

![Brand Concierge](./images/bc29.png)

Vous devriez alors voir ceci. Cliquez sur **+ Connexion** sur la vignette **Catalogue de produits**.

![Brand Concierge](./images/bc30.png)

Sélectionnez la source de connaissances **Produits CitiSignal** et cliquez sur **Enregistrer**.

![Brand Concierge](./images/bc31.png)

Vous devriez alors voir ceci. Cliquez sur **Aperçu** pour commencer à interagir avec votre Brand Concierge.

![Brand Concierge](./images/bc32.png)

Vous pouvez maintenant commencer à poser des questions relatives aux sources de connaissances fournies.

![Brand Concierge](./images/bc33.png)

## 1.4.1.3 les étapes d’intégration à AEP

Brand Concierge utilise Adobe Experience Platform pour stocker les données d’interaction des conversations. La connexion entre Brand Concierge et Experience Platform nécessite qu’un flux de données soit configuré et utilisé par Brand Concierge.

### Train de données

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Assurez-vous d’avoir sélectionné la sandbox appropriée, qui doit être nommée `--aepUserLdap-- - bc`. Dans le menu de gauche, faites défiler l’écran vers le bas et sélectionnez **Flux de données**.

![Brand Concierge](./images/aep2.png)

Cliquez sur **Nouveau flux de données**.

![Brand Concierge](./images/aep3.png)

Saisissez le **** Nom du flux de données `--aepUserLdap-- - Brand Concierge`, puis sélectionnez le **** Schéma de mappage`cja-brand-concierge-sb-XXX`.

Cliquez sur **Enregistrer**.

![Brand Concierge](./images/aep4.png)

Votre flux de données est maintenant configuré. Copiez le nom du flux de données et l’identifiant du flux de données et notez-les dans un fichier texte sur votre ordinateur.

![Brand Concierge](./images/aep5.png)

### Gestion de la configuration des flux de données

L’étape suivante consiste à activer l’API Brand Concierge Configuration Management pour configurer le flux de données que vous venez de créer. Cela est nécessaire pour résoudre des éléments tels que les détails de l’ID d’organisation IMS et du sandbox pendant le traitement de la demande.

Accédez à **Contrôles d’administration**.

![Brand Concierge](./images/admincontrols1.png)

Accédez à **Gestion de la configuration des flux de données** puis cliquez sur **Ajouter une configuration**.

![Brand Concierge](./images/admincontrols2.png)

Collez l’**identifiant du flux de données** du flux de données que vous avez créé précédemment. Cliquez sur **Enregistrer**.

![Brand Concierge](./images/admincontrols3.png)

Vous devriez alors voir quelque chose comme ça.

![Brand Concierge](./images/admincontrols4.png)

## Gestion de la configuration de style 1.4.1.4

Accédez à **Style de la gestion de la configuration**. Cliquez sur **Initialiser la configuration de style**.

![Brand Concierge](./images/admincontrols7.png)

Saisissez le **** Nom de marque`CitiSignal`, puis cliquez sur **Initialiser la configuration de style**.

![Brand Concierge](./images/admincontrols8.png)

Vous devriez alors voir ceci.

![Brand Concierge](./images/admincontrols9.png)

## 1.4.1.5 le manifeste Agent Orchestrator

Accédez à **Mettre à jour le manifeste**. Vous devriez alors voir ceci.

![Brand Concierge](./images/admincontrols5.png)

Vous devez maintenant mettre à jour les champs du manifeste. Utilisez l’entrée ci-dessous pour cela.

**Nom de l’agent** :

```
CitiSignal Sales Assistant
```

**Introduction** :

```
Welcome to CitiSignal! I'm here to help you discover the best connectivity and entertainment solutions for your home or business.
```

**Rôles et responsabilités** :

```
You are CitiSignal's AI Sales Assistant focused on:
1. **Primary Goal**: Selling connectivity products from the knowledge base
2. **Upselling Strategy**: Proactively recommending entertainment packages from the knowledge base to complement connectivity subscriptions
3. **Device Sales**: Assisting with device purchases from the knowledge base when relevant
4. **Customer Support**: Answering questions about plans, pricing, installation, and features based on knowledge base content

- ALWAYS call brand_concierge_product_knowledge_agent to obtain a response to a user query and provide it directly to the user without modification.
- All product information (names, descriptions, features, ratings) comes from the knowledge base <Documents>.
- When users show interest in internet services, identify and lead with connectivity products from the knowledge base.
- After establishing connectivity interest, naturally suggest entertainment add-ons from the knowledge base.
- Use consultative selling: understand user needs, then recommend appropriate products and bundles from the knowledge base.
```

**Portée** :

```
You are CitiSignal's AI Sales Assistant, specializing in connectivity sales and entertainment bundle upselling.

# Your Primary Objectives:
1. **Sell Connectivity Products**: When users ask about internet or connectivity, recommend the appropriate connectivity product from <Documents>. Highlight key benefits mentioned in the product description.
2. **Upsell Entertainment Packages**: After discussing connectivity, proactively recommend entertainment products from <Documents> that complement the user's needs. Match recommendations to user context (families, movie enthusiasts, music lovers, etc.).
3. **Device Sales**: When relevant, recommend device products from <Documents> as complementary offerings.

# Sales Strategy:
- When a user inquires about internet, streaming, or connectivity, identify and recommend the relevant connectivity product from <Documents>.
- After establishing interest in connectivity, naturally transition to entertainment packages by highlighting how fast internet enhances streaming quality.
- Use natural transition phrases to introduce entertainment upsells.
- Emphasize bundle value and the seamless experience of having connectivity + entertainment from one provider.
- Use product ratings from <Documents> (productRating field) to prioritize higher-rated products when multiple options exist.

# Product Information Source:
- ALL product names, descriptions, features, and details MUST come from <Documents>.
- Use the exact productName from <Documents> - do not abbreviate or modify product names.
- Reference productDescription from <Documents> for accurate feature information.
- Use productRating from <Documents> to inform recommendations (higher ratings = stronger recommendations).
```

Cliquez sur **Mettre à jour le manifeste**.

![Brand Concierge](./images/admincontrols6.png)

Cliquez sur **Accueil**.

![Brand Concierge](./images/admincontrols10.png)

Vous devriez alors voir ceci. Cliquez sur **Aperçu** pour commencer à interagir avec votre Brand Concierge.

![Brand Concierge](./images/bc101.png)

Vous pouvez maintenant commencer à poser des questions relatives aux sources de connaissances fournies. Saisissez le `what products do you sell?` de la question et cliquez sur **Envoyer**.

![Brand Concierge](./images/bc102.png)

Vous devriez alors obtenir une réponse similaire.

![Brand Concierge](./images/bc103.png)

Votre instance de Brand Concierge est maintenant prête à être implémentée sur votre site web.

Étape suivante : [ Implémentation de Brand Concierge sur votre site web ](./ex2.md){target="_blank"}

Revenir à [Brand Concierge](./brandconcierge.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
