---
title: Prise en main d’Agent Orchestrator
description: Prise en main d’Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: ffdc6b34a82c945c142f433f65a4f2f8d5cdcd18
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---

# 1.1.1 Prise en main d’Agent Orchestrator

## 1.1.1.1 Définir le contexte dans Agent Orchestrator

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Cliquez sur la fenêtre **context**.

![Agent Orchestrator](./images/ao2.png)

Définissez le contexte sur :

- **Documentation Source** : **Customer Journey Analytics**
- **Sandbox** : **Accélérer**
- **Vue de données** : **Accélérer le B2C 2026**

Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/ao3.png)

>[!NOTE]
>
>Dans cet atelier, vous allez passer d’une analyse à une orchestration et changer de contexte.

## 1.1.1.2 Commencez par les tendances d’achat globales pour ancrer le contexte et zoomer sur la fibre

**Intention** : prenez une bonne idée de la demande de la catégorie (mobile, fixe, Internet, télévision, fibre optique), en particulier au cours des 60 derniers jours. Cette option définit des niveaux de référence pour la saisonnalité, les effets de promotion et la variance régionale après le déploiement à New York.

**Réflexion** :

« Est-ce que Fibre gagne des parts postNY ? Est-ce que nous assistons à la cannibalisation de l&#39;Internet cuivre/DSL ? Quelle est la répartition par rapport aux offres groupées TV ? »

« Cela m’aidera à déterminer le public auquel je peux m’adresser à Vienne et à fixer des objectifs réalistes. »

**Le spécialiste marketing s’attend à obtenir des lectures exploitables** :

Graphique à barres empilées/en courbes des achats par catégorie principale (grain quotidien/hebdomadaire).

Pourcentage de part des achats par catégorie par rapport à la période précédente.

Pics notables corrélés aux dates promotionnelles.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Vous devriez alors voir ceci :

>[!NOTE]
>
>Gardez un œil sur l’attribution tardive : les commandes de fibres peuvent être capturées sous « Internet » dans certains schémas hérités. Si tel est le cas, réconciliez la taxonomie avant les décisions.

![Agent Orchestrator](./images/ao5.png)

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Vous devriez ensuite voir ceci, qui examine les tendances spécifiques à la fibre optique.

**Action** : Notez la courbe de croissance et les pics régionaux.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Corréler les commandes avec les préférences de contenu

**Intention** : testez l’hypothèse selon laquelle la préférence de contenu (SciFi, Sports, Drama, par exemple) prédit le comportement de mise à niveau du haut débit, en particulier pour les besoins en bande passante élevée.

**Réflexion**

« Les fans de science-fiction regardent souvent la 4K et la diffusion en continu à partir de plusieurs appareils, ce qui est susceptible d&#39;augmenter la faible latence. »

« Quantifions si la science-fiction (et peut-être les sports) sont en corrélation avec les commandes récentes. »

**Résultats escomptés**

Un pivot de Commandes (filtre cumulé sur l’exercice en cours appliqué) divisé par genre préféré, limité à 2 mois.

Classez les genres par taux de conversion d’ordre et AOV (valeur d’ordre moyenne).

Décision : Si SciFi affiche un signal fort, cela devient un pilier créatif principal pour le lancement de Fibre Max à Vienne (par exemple, des messages « plus jamais de tampon », des forfaits premium).

**Intention**

Analysez la conversion par genre (par exemple, science-fiction, sports).

**Objectif** Vérifiez si les fans de Sci-Fi surindexent pour les mises à niveau de la technologie Fibre.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identifier Les Parcours Fibre Existants

Cliquez sur la fenêtre **context**.

![Agent Orchestrator](./images/ao10.png)

Définissez le contexte sur :

- **Documentation Source** : **Adobe Journey Optimizer**
- **Sandbox** : **Accélérer**
- **Vue de données** : **Accélérer le B2C 2026**

![Agent Orchestrator](./images/ao11.png)

**Intention** Découvrez quels parcours en cours ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

**Réflexion**

« Lequel de ces parcours a donné de bons résultats et quels en ont été les déclencheurs ? »

« Puis-je réutiliser la logique d’orchestration gagnante pour Vienne ? »

**Résultats escomptés**

Liste des parcours avec le statut (actif, en pause, terminé), les périodes, les segments cibles, les KPI (taux d’ouverture, CTR, conversion).

Prochaine étape : présélectionnez un ou deux parcours de fibre réussis pour le clonage/adaptation.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao13.png)

Répertorier les parcours actifs ou passés avec messagerie Fibre.

Action : sélectionnez les parcours les plus performants pour le clonage.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Vérifier l&#39;adresse

**Intention** :

Comprenez la définition de départ du parcours « CitiSignal - Promotion de lancement Fibre Max » : les caractéristiques qui ont motivé le ciblage (par exemple, « Préférence de genre SciFi », « Appareils 4+ », « Diffusion ≥ 300GB/mois »).

**Réflexion**

« Je veux combiner la créativité SciFi éprouvée avec la messagerie de performance Fibre Max. »

« Si l’audience chevauche des téléchargeurs volumineux, nous pouvons cumuler la propension. »

**Résultats escomptés**

Critères d’audience (inclusion/exclusion), taille d’audience, filtres régionaux, récence, seuils de fréquence.

>[!NOTE]
>
>Remplacer le contexte par CJA

À partir de là, le marketeur passe en mode Analytics pour garantir un compte rendu des performances correct.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
What was the initial audience in the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/ao16.png)
Examinez les critères d’audience (habitudes de diffusion en continu, nombre d’appareils).

**Objectif** : comprendre les caractéristiques pour les besoins en bande passante élevée.

## 1.1.1.6 Validation des performances du parcours via l’analyse des abandons

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

>[!NOTE]
>
>Modifier le contexte en (CJA)

**Intention** :

Création d’un funnel pas à pas dans Customer Journey Analytics

Livré → ouvert → cliqué → Landed → Product View → Add to Cart → Checkout → Order Complete

Incluez les vues de SKU associées à Fibre comme branche.

**Réflexion** :

« Où perdons-nous des utilisateurs (ouverture d’e-mail, chargement de page de destination, PDP, friction de passage en caisse) ? »

« Les utilisateurs de SciFi rebondissent-ils plus ou moins que la moyenne sur le PDP Fibre ? »

**Résultats escomptés** :

Une visualisation des abandons avec des taux de dépôt à chaque étape.

Recouvrements de segments (SciFi vs Sports vs Autre).

Répartition appareil/navigateur pour le frottement technique.

**Décisions** :

Si le taux de passage en caisse est élevé, assurez-vous de collaborer avec le produit/l’expérience utilisateur pour corriger le flux de paiement.

Si la sortie PDP est élevée, la clarté de la demande de reprise (vitesses, temps d&#39;installation, valeur du lot).

>[!NOTE]
>
>Remplacer le contexte par JO

Le marketeur passe maintenant à Adobe Journey Optimizer pour les opérations d’orchestration et d’audience.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey 
```

Visualisation Build funnel : diffusée → ouverte → sur laquelle vous avez cliqué → passer → commande.

**Action** : identifier les points de dépôt et optimiser la messagerie ou l’expérience utilisateur.

## 1.1.1.7 Rechercher des audiences existantes alignées sur une utilisation élevée

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Remplacer le contexte par Adobe Journey Optimizer

**Intention** :

Localisez toute audience d’applications d’entreprise nommée avec des « téléchargeurs lourds », probablement définis par des seuils d’utilisation des données mensuels, des heures de diffusion en continu ou la simultanéité des appareils.

**Réflexion** :

« Si une audience comme Heavy Downloaders existe, elle est parfaite pour le positionnement Fibre Max : vitesse, fiabilité, niveaux illimités. »

**Résultats escomptés** :

Métadonnées d’audience : critères de définition, taille, dernière actualisation, balises de gouvernance, disponibilité de la région.

Localiser les audiences avec une utilisation élevée des données.

**Objectif** : combiner avec la préférence Sci-Fi pour le ciblage Fibre Max.

## 1.1.1.8 Déterminer si ces audiences sont déjà utilisées

**Intention** :

Vérifiez la liaison entre l’audience et le parcours afin de vous assurer que les messages ne sont pas doublés et qu’ils n’entrent pas en conflit avec les programmes actuels.

**Réflexion** :

« Si Heavy Downloaders est déjà dans un parcours de rétention, nous avons besoin d&#39;une logique de suppression ou d&#39;un capping de la fréquence pour éviter la fatigue. »

**Résultats escomptés** :

Mappages : audience → nom du parcours, statut, politique de contact, dernier envoi, performances.

**Décision** :

Si vous l’utilisez, créez des exclusions ou des suppressions partagées pour le lancement de Vienne.

S&#39;il n&#39;est pas utilisé, autoriser le nouveau parcours.

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Which of the above are used in a journey? 
```

Veillez à ce qu’il n’y ait aucun chevauchement avec les campagnes actives.

**Action** : appliquez la suppression si nécessaire.

## 1.1.1.9 Créer un nouveau Parcours pour Fibre Max Launch

**Intention** :

Créez un nouveau parcours ciblant l’audience composée :

Téléchargements lourds ∩ Préférence SciFi (kbaa_5207bf clé d’audience).

**Réflexion** :

« C&#39;est le point d&#39;orgue de Fibre Max : propension élevée + pertinence créative. »

« Nous allons orchestrer une expérience multipoint liée à la disponibilité de Vienne. »

**Conception de Parcours (JO)** :

Critères d’entrée :

Audience : Téléchargeurs lourds - Sci-Fi Preference_kbaa_5207bf

Géographie : Métro de Vienne (liste de codes postaux ou polygone géographique)

Éligibilité : Pas dans la campagne « Fibre Upgrade NYC - Sept » active ; pas un abonné Fibre actuel.

Déclencheur et minutage :

T14 jours avant le lancement de Vienne (janvier 2026) : Prévisualiser l’e-mail—« Fibre Max est à venir. »

Semaine de lancement : e-mail par Principal + bannière in-app + synchronisation de médias achetés (via la destination CDP).

T+3 jours : répartition des comportements : si aucun clic, rebond du SMS ; si l’utilisateur clique mais ne passe pas de commande, reciblage avec un CTA de disponibilité du programme d’installation.

T+10 jours : test de l’offre : installation gratuite contre remise du 1er mois (A/B).

PERSONALIZATION :

Copie dynamique pour les amateurs de SciFi (hooks de streaming latence/4K).

Revendications de vitesse/latence adaptées à la combinaison d’appareils (consoles de jeux, boîtiers de streaming).

Recommandation groupée : Fiber Max + pack de contenu spécial TV.

Gouvernance :

Limite de fréquence : 3 contacts max. par 10 jours.

Supprimez si l&#39;abonné Fibre actuel ou un ticket existe pour l&#39;installation.

Respectez les préférences d’opt-out.

**Plan de mesure (CJA)** :

Suivi : diffusion, ouverture, clic, affichage PDP, début du passage en caisse, fin de la commande.

KPI : Taux de conversion vers Fibre Max, augmentation/contrôle, horaire d&#39;installation.

Diagnostics : rapport sur les abandons par segment d’appareil/de genre.

Comment tout cela s’intègre (modèle mental du professionnel du marketing)

Diagnostiquer la demande (catégories générales → Fibre en particulier).

Démontrer le contenu au signal de conversion (commandes par genre).

Mes parcours réussis (trouvez les parcours FibreName et l&#39;audience de promotion SciFi).

Validez les points de friction (abandon de CJA sur le parcours SciFi).

Activez par rapport aux segments à forte propension (téléchargeurs lourds ∩ SciFi).

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Cliquez sur la fenêtre **context**.

![Agent Orchestrator](./images/ao2.png)

Définissez le contexte sur :

- **Documentation Source** : **Journey Optimizer**
- **Sandbox** : **Accélérer**
- **Vue de données** : **Accélérer le B2C 2026**

Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/aoea3.png)

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj2.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj3.png)

Vous devriez alors voir ceci. Saisissez `The first one` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj4.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj5.png)

Examinez la réponse. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj6.png)

Cliquez sur **Vérifier**.

![Agent Orchestrator](./images/aocj7.png)

Mettez à jour le nom du parcours avec votre LDAP pour le rendre unique. Cliquez sur **Enregistrer**.

![Agent Orchestrator](./images/aocj8.png)

Votre parcours a été créé en mode brouillon.

![Agent Orchestrator](./images/aocj9.png)

## Expériences 1.1.1.10

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Cliquez sur la fenêtre **context**.

![Agent Orchestrator](./images/ao2.png)

Définissez le contexte sur :

- **Documentation Source** : **Journey Optimizer**
- **Sandbox** : **Accélérer**
- **Vue de données** : **Accélérer le B2C 2026**

Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/aoea3.png)

Saisissez l’**invite** suivante, puis cliquez sur le bouton **générer**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/aoea1.png)

Cliquez sur la suggestion pour comparer les taux de conversion de chaque traitement, puis cliquez sur **générer**.

![Agent Orchestrator](./images/aoea2.png)

Vous devriez alors voir une comparaison détaillée comme celle-ci :

![Agent Orchestrator](./images/aoea4.png)

Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}