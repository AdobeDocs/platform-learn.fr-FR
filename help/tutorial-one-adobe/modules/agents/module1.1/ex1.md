---
title: Prise en main d’Agent Orchestrator
description: Prise en main d’Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
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

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Vous devriez ensuite voir ceci, qui examine les tendances spécifiques à la fibre optique.

**Action** : Notez la courbe de croissance et les pics régionaux.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Corréler les commandes avec les préférences de contenu

**Intention**

Testez l’hypothèse selon laquelle la préférence de contenu (science-fiction, sports, théâtre, etc.) prédit le comportement de mise à niveau de la large bande passante, en particulier pour les besoins en bande passante élevée.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identifier Les Parcours Fibre Existants

**Intention**

Découvrez quels parcours actifs ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao13.png)

Répertorier les parcours actifs ou passés avec messagerie Fibre.

Action : sélectionnez les parcours les plus performants pour le clonage.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Vérifier l&#39;adresse

**Intention** :

Comprenez la définition de départ du parcours « CitiSignal - Promotion de lancement Fibre Max » : les caractéristiques qui ont motivé le ciblage (par exemple, « Préférence de genre SciFi », « Appareils 4+ », « Diffusion ≥ 300GB/mois »).

Saisissez ce qui suit **Invite** puis saisissez **+CitiSignal fib** pour activer la saisie automatique. Sélectionnez le parcours **Promotion de lancement CitiSignal - Fibre max**.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

Vous devriez alors voir ceci. Cliquez sur le bouton **envoyer**.

![Agent Orchestrator](./images/ao17.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validation des performances du parcours via l’analyse des abandons

**Intention**

Création d’un funnel pas à pas dans Customer Journey Analytics

Livré → ouvert → cliqué → Landed → Product View → Add to Cart → Checkout → Order Complete

Incluez les vues de SKU associées à Fibre comme branche.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 Créer une audience

**Intention**

Sur la base des résultats ci-dessus, il existe une corrélation entre les clients qui consomment beaucoup de données et qui ont un genre préféré de science-fiction ou de fantaisie. Vous allez maintenant combiner ces attributs dans une audience.

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

>[!NOTE]
>
>Veuillez vérifier que le contexte de l’assistant pointe vers le sandbox **Accélérer** et la vue de données **Accélérer 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Examinez le plan. Saisissez `yes` et cliquez sur **Envoyer**.

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
>Lors de la création d’une audience, il faudra 24 heures avant que l’audience ne soit disponible pour l’assistant à des fins d’utilisation.

## 1.1.1.8 Rechercher les audiences existantes alignées sur une utilisation élevée et vérifier si elles sont en cours d’utilisation

**Intention** :

Localisez toute audience dont le nom comporte des « téléchargeurs volumineux », définis par des seuils mensuels d’utilisation des données.

>[!NOTE]
>
>À l’étape précédente, vous avez créé une nouvelle audience. Gardez à l’esprit qu’il faudra 24 heures avant que l’audience ne soit disponible pour l’assistant à des fins d’utilisation ultérieure. Vous devez maintenant utiliser une autre audience, déjà existante.

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

>[!NOTE]
>
>Veuillez vérifier que le contexte de l’assistant pointe vers le sandbox **Accélérer** et la vue de données **Accélérer 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/ao31.png)

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
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

Vous devriez alors voir quelque chose de similaire à ceci. Ce parcours ne fonctionne pas en ce moment.

![Agent Orchestrator](./images/ao53.png)

Pour le lancement prochain de Fibre Max, vous devez maintenant créer un nouveau parcours.

## 1.1.1.9 Créer un nouveau Parcours pour Fibre Max Launch

**Intention** :

Créez un nouveau parcours ciblant l’audience composée :

Téléchargements lourds ∩ Préférence SciFi (kbaa_5207bf clé d’audience).

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

>[!NOTE]
>
>Veuillez vérifier que le contexte de l’assistant pointe vers le sandbox **Accélérer** et la vue de données **Accélérer 2026 B2C**

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

## Gestion des conflits de Parcours 1.1.1.10

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

>[!NOTE]
>
>Veuillez vérifier que le contexte de l’assistant pointe vers la source de documentation **Journey Optimizer**, le sandbox **Accélérer** et la vue de données **Accélérer 2026 B2C**

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
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

Consultez les informations de conflit de parcours.

![Agent Orchestrator](./images/aocj71.png)

Faites défiler la page vers le bas pour rechercher plus de détails sur les conflits de parcours.

![Agent Orchestrator](./images/aocj72.png)

## Expériences 1.1.1.11

Accédez à [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Vous devriez alors voir ceci. Vérifiez que vous êtes dans l’organisation **Experience Platform International**.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

>[!NOTE]
>
>Veuillez vérifier que le contexte de l’assistant pointe vers le sandbox **Accélérer** et la vue de données **Accélérer 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/aoea1.png)

Cliquez sur la suggestion pour comparer les taux de conversion de chaque traitement, puis cliquez sur **envoyer**.

![Agent Orchestrator](./images/aoea2.png)

Vous devriez alors voir une comparaison détaillée comme celle-ci :

![Agent Orchestrator](./images/aoea4.png)

Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}