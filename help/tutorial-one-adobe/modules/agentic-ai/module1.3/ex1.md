---
title: Prise en main d’Agent Orchestrator
description: Prise en main d’Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Prise en main d’Agent Orchestrator

## 1.3.1 Définition du contexte dans Agent Orchestrator

Accédez à l’assistant d’IA et placez-le en mode Grand .

Vérifiez que vous vous trouvez dans le contexte CJA pour les tâches d’analyse.

>[!NOTE]
>
>Utilisez le changement de contexte lorsque vous passez d’une analyse (CJA) à une orchestration (JO).

## 1.3.2 Commencez par les tendances d&#39;achat globales pour ancrer le contexte et zoomer sur la fibre

**Invite** :

```javascript
Show me purchases by mainCategory over the last 2 month
```

**Intention** : prenez une bonne idée de la demande de la catégorie (mobile, fixe, Internet, télévision, fibre optique), en particulier au cours des 60 derniers jours. Cette option définit des niveaux de référence pour la saisonnalité, les effets de promotion et la variance régionale après le déploiement à New York.

Réflexion :

« Est-ce que Fibre gagne des parts postNY ? Est-ce que nous assistons à la cannibalisation de l&#39;Internet cuivre/DSL ? Quelle est la répartition par rapport aux offres groupées TV ? »

« Cela m’aidera à déterminer le public auquel je peux m’adresser à Vienne et à fixer des objectifs réalistes. »

Lectures exploitables attendues par le spécialiste marketing :

Graphique à barres empilées/en courbes des achats par catégorie principale (grain quotidien/hebdomadaire).

Pourcentage de part des achats par catégorie par rapport à la période précédente.

Pics notables corrélés aux dates promotionnelles.

>[!NOTE]
>
>Gardez un œil sur l’attribution tardive : les commandes de fibres peuvent être capturées sous « Internet » dans certains schémas hérités. Si tel est le cas, réconciliez la taxonomie avant les décisions.

 

**Invite** :

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**Invite suivante**

`Show me purchases by mainCategory = Fiber over the last 2 months`

Explorez les tendances spécifiques aux fibres.

**Action** Notez la courbe de croissance et les pics régionaux.

## 1.3.3 Corréler les commandes avec les préférences de contenu

**Invite** :

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**Intention** Testez l’hypothèse selon laquelle les préférences de contenu (SciFi, sports, théâtre, etc.) prédisent le comportement de mise à niveau de la large bande passante, en particulier pour les besoins en bande passante élevée.

**Réflexion**

« Les fans de science-fiction regardent souvent la 4K et la diffusion en continu à partir de plusieurs appareils, ce qui est susceptible d&#39;augmenter la faible latence. »

« Quantifions si la science-fiction (et peut-être les sports) sont en corrélation avec les commandes récentes. »

**Résultats escomptés**

Un pivot de Commandes (filtre cumulé sur l’exercice en cours appliqué) divisé par genre préféré, limité à 2 mois.

Classez les genres par taux de conversion d’ordre et AOV (valeur d’ordre moyenne).

Décision : Si SciFi affiche un signal fort, cela devient un pilier créatif principal pour le lancement de Fibre Max à Vienne (par exemple, des messages « plus jamais de tampon », des forfaits premium).

**Invite**

`Show me ordersYTD by preferred genre for the last 2 months`

**Intention**

Analysez la conversion par genre (par exemple, science-fiction, sports).

**Objectif** Vérifiez si les fans de Sci-Fi surindexent pour les mises à niveau de la technologie Fibre.

## 1.3.4 Identification Des Parcours De Fibres Existants

**Invite** :

```javascript
What journey was running and had Fiber in the name
```

**Intention** Découvrez quels parcours en cours ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

**Réflexion**

« Lequel de ces parcours a donné de bons résultats et quels en ont été les déclencheurs ? »

« Puis-je réutiliser la logique d’orchestration gagnante pour Vienne ? »

**Résultats escomptés**

Liste des parcours avec le statut (actif, en pause, terminé), les périodes, les segments cibles, les KPI (taux d’ouverture, CTR, conversion).

Prochaine étape : présélectionnez un ou deux parcours de fibre réussis pour le clonage/adaptation.

**Invite**

`What journey was running and had Fiber in the name?`

Répertorier les parcours actifs ou passés avec messagerie Fibre.

Action : sélectionnez les parcours les plus performants pour le clonage.

## 1.3.5 Vérifier l&#39;audience de départ pour une promotion historique pertinente

**Invite** :

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**Intention** comprendre la définition de départ du parcours « SciFi Promo 2024 - jl », c’est-à-dire les caractéristiques qui ont conduit au ciblage (par exemple, « SciFi Genre Preference », « 4+ appareils », « flux ≥ 300GB/mois »).

**Réflexion**

« Je veux combiner la créativité SciFi éprouvée avec la messagerie de performance Fibre Max. »

« Si l’audience chevauche des téléchargeurs volumineux, nous pouvons cumuler la propension. »

**Résultats escomptés**

Critères d’audience (inclusion/exclusion), taille d’audience, filtres régionaux, récence, seuils de fréquence.

>[!NOTE]
>
>Remplacer le contexte par CJA

À partir de là, le marketeur passe en mode Analytics pour garantir un compte rendu des performances correct.

**Invite** :

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

Examinez les critères d’audience (habitudes de diffusion en continu, nombre d’appareils).

Objectif : comprendre les caractéristiques pour les besoins en bande passante élevée.

## 1.3.6 Validation des performances du parcours via l’analyse des abandons

**Invite** :

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>Modifier le contexte en (CJA)

**Intention** créer un funnel par étapes dans Customer Journey Analytics

Livré → ouvert → cliqué → Landed → Product View → Add to Cart → Checkout → Order Complete

Incluez les vues de SKU associées à Fibre comme branche.

Réflexion :

« Où perdons-nous des utilisateurs (ouverture d’e-mail, chargement de page de destination, PDP, friction de passage en caisse) ? »

« Les utilisateurs de SciFi rebondissent-ils plus ou moins que la moyenne sur le PDP Fibre ? »

Résultats escomptés :

Une visualisation des abandons avec des taux de dépôt à chaque étape.

Recouvrements de segments (SciFi vs Sports vs Autre).

Répartition appareil/navigateur pour le frottement technique.

Décisions :

Si le taux de passage en caisse est élevé, assurez-vous de collaborer avec le produit/l’expérience utilisateur pour corriger le flux de paiement.

Si la sortie PDP est élevée, la clarté de la demande de reprise (vitesses, temps d&#39;installation, valeur du lot).

>[!NOTE]
>
>Remplacer le contexte par JO

Le marketeur passe maintenant à Adobe Journey Optimizer pour les opérations d’orchestration et d’audience.

**Invite** :

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

Visualisation Build funnel : diffusée → ouverte → sur laquelle vous avez cliqué → passer → commande.

Action : identifier les points de dépôt et optimiser la messagerie ou l’expérience utilisateur.


## 1.3.7 Trouver des audiences existantes qui correspondent à une utilisation élevée

**Invite** :

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Remplacer le contexte par Adobe Journey Optimizer

Objectif : localisez toute audience de JO nommée avec des « téléchargeurs intensifs », probablement définis par des seuils mensuels d’utilisation des données, des heures de diffusion en continu ou la simultanéité des appareils.

Réflexion :

« Si une audience comme Heavy Downloaders existe, elle est parfaite pour le positionnement Fibre Max : vitesse, fiabilité, niveaux illimités. »

Résultats escomptés :

Métadonnées d’audience : critères de définition, taille, dernière actualisation, balises de gouvernance, disponibilité de la région.

**Invite** :

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

Localiser les audiences avec une utilisation élevée des données.

Objectif : combiner avec la préférence Sci-Fi pour le ciblage Fibre Max.

## 1.3.8 Déterminer si ces audiences sont déjà utilisées

**Invite** :

```javascript
Which of the above are used in a journey? 
```

Intention : vérifiez la liaison entre l’audience et le parcours afin de vous assurer que nous ne doublons pas de messages ou n’entrons pas en conflit avec les programmes actuels.

Réflexion :

« Si Heavy Downloaders est déjà dans un parcours de rétention, nous avons besoin d&#39;une logique de suppression ou d&#39;un capping de la fréquence pour éviter la fatigue. »

Résultats escomptés :

Mappages : audience → nom du parcours, statut, politique de contact, dernier envoi, performances.

Décision :

Si vous l’utilisez, créez des exclusions ou des suppressions partagées pour le lancement de Vienne.

S&#39;il n&#39;est pas utilisé, autoriser le nouveau parcours.

Invite :

lequel des éléments ci-dessus est utilisé dans un parcours ?

Veillez à ce qu’il n’y ait aucun chevauchement avec les campagnes actives.

Action : appliquez la suppression si nécessaire.

## 1.3.9 Création d&#39;un nouveau Parcours pour Fibre Max Launch

**Invite** :

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

Intention : créez un parcours JO ciblant l’audience composée :

Téléchargements lourds ∩ Préférence SciFi (kbaa_5207bf clé d’audience).

Réflexion :

« C&#39;est le point d&#39;orgue de Fibre Max : propension élevée + pertinence créative. »

« Nous allons orchestrer une expérience multipoint liée à la disponibilité de Vienne. »

Conception de parcours (JO) :

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

Plan de mesure (CJA) :

Suivi : diffusion, ouverture, clic, affichage PDP, début du passage en caisse, fin de la commande.

KPI : Taux de conversion vers Fibre Max, augmentation/contrôle, horaire d&#39;installation.

Diagnostics : rapport sur les abandons par segment d’appareil/de genre.

Forme

Comment tout cela s’intègre (modèle mental du professionnel du marketing)

Diagnostiquer la demande (catégories générales → Fibre en particulier).

Démontrez le contenu au signal de conversion (commandes par genre).

Mes parcours réussis (trouvez les parcours FibreName et l&#39;audience de promotion SciFi).

Validez les points de friction (abandon de CJA sur le parcours SciFi).

Activez par rapport aux segments à forte propension (téléchargeurs lourds ∩ SciFi).


Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}