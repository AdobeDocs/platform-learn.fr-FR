---
title: Prise en main d’Agent Orchestrator
description: Prise en main d’Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: 121cbb5ea8f8b713c6ebae008f7f0d9b3a79e476
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# 1.1.1 Prise en main d’Agent Orchestrator

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3477257?quality=12&learn=on)

## 1.1.1.1 Définir le contexte dans Agent Orchestrator

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Cliquez sur la fenêtre **context**.

![Agent Orchestrator](./images/ao2.png)

Définissez le contexte sur :

- **Documentation Source** : **Journey Optimizer**

Le paramètre Source de la documentation permet de donner la préférence à l’ensemble de documents Experience League à vérifier pour les questions relatives à la connaissance du produit/Experience League.

- **Sandbox** : **Prod - Accélérer (VA7)**

Le paramètre Sandbox permet d’identifier le sandbox que l’assistant AI doit examiner lorsqu’il pose des questions.

- **Vue de données** : **Accélérer le B2C 2026**

Le paramètre Vue de données permet d’identifier l’assistant AI de vue de données à examiner lors de la pose de questions.

Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2 Commencez par les tendances d’achat globales pour ancrer le contexte et zoomer sur la fibre

**Intention**

Obtenez une impulsion de niveau supérieur sur la demande de catégorie (mobile, fixe, Internet, télévision, fibre optique), en particulier pour les 60 derniers jours. Cela définit des niveaux de référence pour la saisonnalité, les effets de promotion et la variance régionale après le déploiement à New York.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao5.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/ao6.png)

Vous devriez ensuite voir ceci, qui examine les tendances spécifiques à la fibre optique.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Corréler les commandes avec les préférences de contenu

**Intention**

Testez l&#39;hypothèse selon laquelle une préférence pour un genre spécifique (p. ex., science-fiction, sports, dramatique) prédit le comportement de mise à niveau de la large bande, en particulier pour les besoins en bande passante élevée.

Tout d’abord, vous devez déterminer quel champ est utilisé pour stocker la préférence de genre.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/ao7a.png)

Vous devriez alors voir ceci, qui indique que le champ utilisé pour le genre est **_experienceplatform.individualFeatures.preferences.preferences.preferencesGenre**.

![Agent Orchestrator](./images/ao7b.png)

Avec ces informations, vous pouvez commencer à analyser en profondeur les données d’achat.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Vous devriez alors voir ceci. Cliquez sur l’icône du bloc **Raisonnement terminé** pour comprendre ce qui se passe en coulisses dans Agent Orchestrator.

![Agent Orchestrator](./images/ao9.png)

Une explication similaire devrait s’afficher.

![Agent Orchestrator](./images/ao10.png)

## 1.1.1.4 Identifier Les Parcours Fibre Existants

**Intention**

Découvrez quels parcours actifs ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Vous devriez alors voir ceci. Cliquez sur **Afficher plus**.

![Agent Orchestrator](./images/ao13.png)

Vous devriez alors voir une liste plus grande de parcours actifs ou passés. Cliquez sur l’icône **télécharger** pour télécharger une liste de ces parcours.

![Agent Orchestrator](./images/ao13a.png)

Un fichier CSV contenant toutes les sorties de l’assistant d’IA est alors généré.

![Agent Orchestrator](./images/ao13b.png)

Cliquez pour fermer le volet de droite. Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Vous devriez alors voir ceci. Cliquez sur le lien de l’un des parcours et sélectionnez **Détails du Parcours**.

![Agent Orchestrator](./images/ao15.png)

Une nouvelle fenêtre s’ouvre et vous accédez immédiatement à l’aperçu des détails du Parcours.

![Agent Orchestrator](./images/ao15a.png)

## 1.1.1.5 Vérifier quelle audience est utilisée

**Intention** :

Comprenez la définition de départ du parcours « CitiSignal - Promotion de lancement Fibre Max » : les caractéristiques qui ont motivé le ciblage (par exemple, « Préférence de genre SciFi », « Appareils 4+ », « Diffusion ≥ 300GB/mois »).

Saisissez ce qui suit **Invite** :

```javascript
What was the initial audience in the journey named 
```

Saisissez ensuite manuellement les `+CitiSignal fib` pour activer la saisie automatique. Sélectionnez le parcours **Promotion de lancement CitiSignal - Fibre max**.

![Agent Orchestrator](./images/ao16.png)

Vous devriez alors voir ceci. Cliquez sur le bouton **envoyer**.

![Agent Orchestrator](./images/ao17.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validation des performances du parcours via l’analyse des abandons

**Intention**

Vous souhaitez comprendre l’abandon des performances du parcours pour déterminer s’il existe des nœuds ou des conditions dans le parcours qui enregistrent un pourcentage élevé de profils abandonnés. Cela permet de comprendre si des ajustements supplémentaires sont nécessaires dans le parcours.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/ao20.png)

Faites défiler l’écran vers le bas. Vous pouvez maintenant consulter le tableau en examinant chaque nœud et ses numéros d’entrée, numéros d’abandon et taux d’abandon respectifs.

L’assistant d’IA vous fournit des observations et des recommandations.

Cliquez sur la phrase **Voici comment j&#39;ai obtenu les résultats**.

![Agent Orchestrator](./images/ao21.png)

Vous pouvez ensuite afficher les étapes suivies par l’assistant AI pour obtenir les résultats.

![Agent Orchestrator](./images/ao22.png)

## 1.1.1.7 Créer une audience

**Intention**

Sur la base des résultats et des recherches ci-dessus, il existe une corrélation entre les clients qui consomment beaucoup de données et qui ont un genre préféré de science-fiction ou de fantasy. Vous allez maintenant combiner ces attributs dans une audience.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Examinez le plan. Saisissez `yes` et cliquez sur **Envoyer**.

>[!NOTE]
>
>Ce plan est généré à partir d’un guide de référence dans le système. Les clients pourront éventuellement personnaliser les plans et ajouter leurs propres plans, mais pour l’instant, ils sont statiques.

![Agent Orchestrator](./images/ao33.png)

Vérifiez l’expression de requête de segment. Saisissez `yes` et cliquez sur le bouton **Envoyer**.

![Agent Orchestrator](./images/ao34.png)

Vérifiez l’estimation de la taille du segment. Saisissez `yes` et cliquez sur le bouton **Envoyer**.

![Agent Orchestrator](./images/ao35.png)

Cliquez sur **Vérifier**.

![Agent Orchestrator](./images/ao36.png)

Examinez la définition de segment. Cliquez sur **Créer**.

![Agent Orchestrator](./images/ao37.png)

Votre audience a maintenant été créée.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>Lors de la création d’une audience, il faudra 24 heures avant que l’audience ne soit disponible pour l’assistant d’IA à des fins d’utilisation ultérieure.

## 1.1.1.8 Rechercher les audiences existantes alignées sur une utilisation élevée et vérifier si elles sont en cours d’utilisation

**Intention** :

Localisez toute audience dont le nom comporte des « téléchargeurs volumineux », définis par des seuils mensuels d’utilisation des données.

>[!NOTE]
>
>À l’étape précédente, vous avez créé une nouvelle audience. Gardez à l’esprit qu’il faudra 24 heures avant que l’audience ne soit disponible pour l’assistant AI à des fins d’utilisation ultérieure. Vous devez maintenant utiliser une autre audience, déjà existante.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Vous devriez alors voir ceci. Vous souhaitez maintenant voir toutes vos audiences et à quel point elles ont changé au cours des derniers jours.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

Vous devriez alors voir ceci. Cliquez sur **Afficher plus**.

![Agent Orchestrator](./images/ao31a.png)

Vous devriez alors voir ceci. Cliquez pour fermer le volet de droite.

![Agent Orchestrator](./images/ao31b.png)

Faites défiler l’écran vers le bas pour passer en revue les étapes effectuées par l’assistant AI.

![Agent Orchestrator](./images/ao31c.png)

Il existe déjà certaines audiences pour les « téléchargeurs lourds ». Voyons s’ils sont déjà utilisés.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

Vous devriez alors voir quelque chose de similaire à ceci.

![Agent Orchestrator](./images/ao51.png)

Vous devez maintenant vérifier si ce parcours est actif. Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

Vous devriez alors voir quelque chose de similaire à ceci. Aucun de ces parcours n’est en cours d’exécution.

![Agent Orchestrator](./images/ao53.png)

Pour le lancement prochain de Fibre Max, vous devez maintenant créer un nouveau parcours.

## 1.1.1.9 Créer un nouveau Parcours pour Fibre Max Launch

**Intention** :

Créez un nouveau parcours ciblant l’audience composée :

Téléchargeurs lourds ∩ SciFi Preference.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj2.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Générer.

![Agent Orchestrator](./images/aocj3.png)

Vous devriez alors voir ceci. Saisissez `The first one` et cliquez sur Envoyer.

![Agent Orchestrator](./images/aocj4.png)

Vous devriez alors voir ceci. Saisissez `yes` et cliquez sur Envoyer.

![Agent Orchestrator](./images/aocj5.png)

Examinez la réponse. Saisissez `yes` et cliquez sur Envoyer.

![Agent Orchestrator](./images/aocj6.png)

Cliquez sur **Vérifier**.

![Agent Orchestrator](./images/aocj7.png)

Mettez à jour le nom du parcours avec votre LDAP pour le rendre unique. Cliquez sur **Enregistrer**.

![Agent Orchestrator](./images/aocj8.png)

Votre parcours a été créé en mode brouillon.

![Agent Orchestrator](./images/aocj9.png)

## Gestion des conflits de Parcours 1.1.1.10

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

Consultez les informations.

![Agent Orchestrator](./images/aocj81.png)

Faites défiler vers le bas et sélectionnez l’**Sources** pour vérifier que les informations proviennent d’Experience League.

![Agent Orchestrator](./images/aocj82.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
List any conflicts for the journey +CitiSignal Fiber Max
```

Sélectionnez ensuite manuellement le parcours **Promotion de lancement CitiSignal - Fibre max** dans la liste.

![Agent Orchestrator](./images/aocj70.png)

Vous devriez alors voir ceci. Cliquez sur **envoyer**.

![Agent Orchestrator](./images/aocj70a.png)

Consultez les informations de conflit de parcours.

![Agent Orchestrator](./images/aocj71.png)

Faites défiler la page vers le bas pour rechercher plus de détails sur les conflits de parcours.

![Agent Orchestrator](./images/aocj72.png)

## Expériences 1.1.1.11

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/aoea1.png)

Faites défiler vers le bas et cliquez sur l’une des suggestions. Cliquez sur **envoyer**.

>[!NOTE]
>
>Les suggestions sont dynamiques. Vous devez donc vous attendre à voir des suggestions différentes chaque fois qu’une réponse est générée. Vos suggestions seront probablement différentes de celles affichées dans cette capture d’écran.

![Agent Orchestrator](./images/aoea2.png)

Vous devriez alors voir une réponse détaillée liée à la suggestion qui a été choisie.

![Agent Orchestrator](./images/aoea4.png)

Vous avez maintenant terminé ce Lab.

Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}