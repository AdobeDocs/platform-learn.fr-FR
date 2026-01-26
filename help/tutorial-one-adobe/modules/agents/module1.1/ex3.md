---
title: Adobe Marketing Agent for Microsoft 365 Copilot
description: Adobe Marketing Agent pour Microsoft 365 CopilotCopilot
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 5%

---

# 1.1.3 Adobe Marketing Agent for Microsoft 365 Copilot

>[!IMPORTANT]
>
>Ce Lab utilise une fonctionnalité qui n&#39;a pas encore été publiée. La fonctionnalité est toujours en cours de développement, elle n’est donc pas encore disponible pour tous.

[!BADGE Beta]

+++Détails Beta
En utilisant le Adobe Marketing Agent avec Microsoft 365 Copilot Beta, vous reconnaissez que le Beta est fourni « en l’état », sans garantie d’aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce Beta et/ou des éléments qui l’accompagnent. Le Beta est considéré comme des informations confidentielles d’Adobe.  Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts que vous rencontrez lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ce commentaire.

+++

## Conditions préalables

Pour suivre les étapes de cet atelier, comme indiqué ci-dessous, vous devez disposer des droits d’accès suivants :

- Accès à Real-Time CDP, Journey Optimizer et Customer Journey Analytics
- Accès à l’assistant d’IA dans Adobe Experience Cloud
- Accès à AEP Agent Orchestrator
- Accès à Microsoft 365 Copilot

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1 Ajouter Adobe Marketing Agent à Microsoft 365 Teams &amp; Copilot

Ouvrez Microsoft Teams et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci.

Cliquez sur **Applications**.

![ChatGPT](./images/copilot1.png)

Sélectionnez **Gérer vos applications**.

![ChatGPT](./images/copilot2.png)

Sélectionnez **Charger une application**.

![ChatGPT](./images/copilot3.png)

Sélectionnez **Charger une application personnalisée**.

![ChatGPT](./images/copilot4.png)

Sélectionnez le fichier manifeste qui vous a été fourni par votre instructeur et cliquez sur **Ouvrir**.

![ChatGPT](./images/copilot5.png)

Cliquez sur **Ajouter**.

![ChatGPT](./images/copilot6.png)

Cliquez sur **Ouvrir avec Copilote**.

![ChatGPT](./images/copilot7.png)

Adobe Marketing Agent est maintenant chargé.

![ChatGPT](./images/copilot8.png)

Saisissez le `login` d’invite et cliquez sur le bouton **envoyer**.

![ChatGPT](./images/copilotlogin1.png)

Cliquez sur **Connexion à Adobe Marketing Agent**.

![ChatGPT](./images/copilotlogin2.png)

Une nouvelle fenêtre s’ouvre, vous demandant de vous connecter à l’aide des informations d’identification de votre compte Adobe.

![ChatGPT](./images/copilotlogin3.png)

Une fois l’authentification réussie, vous devrez peut-être sélectionner l’instance spécifique que vous souhaitez utiliser. Si cet écran s’affiche, sélectionnez l’instance —aepImsOrgName—.

![ChatGPT](./images/copilotlogin4.png)

Un code similaire est alors généré. Cliquez sur **Copier** pour copier le code.

![ChatGPT](./images/copilotlogin5.png)

Collez le code dans la fenêtre Adobe Marketing Agent de Copilot et cliquez sur le bouton **send**.

![ChatGPT](./images/copilotlogin6.png)

Vous devriez alors voir quelque chose de similaire à ceci. Vous êtes maintenant connecté à Adobe Marketing Agent dans Microsoft 365 Copilot.

![ChatGPT](./images/copilotlogin7.png)

## 1.1.3.2 Définir le contexte dans Adobe Marketing Agent

Avant d’interagir davantage avec Adobe Marketing Agent via Copilot, le contexte doit être défini.

Pour cet exercice, le contexte doit être défini pour utiliser :

- **Sandbox** : **Prod - Accélérer (VA7)**

  Le paramètre sandbox permet d’identifier le sandbox que l’assistant AI doit examiner lorsqu’il pose des questions.

- **Vue de données** : **Accélérer le B2C 2026**

  Le paramètre de vue de données permet d’identifier la vue de données que l’assistant AI doit examiner lors de la pose de questions.

![Agent Orchestrator](./images/copilotlogin7.png)

Pour modifier le sandbox, saisissez la commande suivante, puis cliquez sur le bouton **envoyer**.

```javascript
change sandbox
```

![Agent Orchestrator](./images/copilot9.png)

Vous devriez alors voir quelque chose de similaire à ceci. Sélectionnez le sandbox à utiliser, puis cliquez sur **sélectionner**.

![Agent Orchestrator](./images/copilot10.png)

Vous devriez alors voir ceci. Pour modifier la vue de données, saisissez la commande suivante puis cliquez sur le bouton **envoyer**.

```javascript
change dataview
```

![Agent Orchestrator](./images/copilot11.png)

Vous devriez alors voir quelque chose de similaire à ceci. Sélectionnez la vue de données à utiliser, puis cliquez sur **sélectionner**.

![Agent Orchestrator](./images/copilot12.png)

Vous devriez alors voir ceci. Le contexte est maintenant correctement défini afin que vous puissiez commencer à envoyer des invites spécifiques.

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3 Commencez par les tendances d’achat globales pour ancrer le contexte et zoomer sur la fibre

**Intention**

Obtenez une impulsion de niveau supérieur sur la demande de catégorie (mobile, fixe, Internet, télévision, fibre optique), en particulier pour les 60 derniers jours. Cela définit des niveaux de référence pour la saisonnalité, les effets de promotion et la variance régionale après le déploiement à New York.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory over the last 4 months.
```

![Agent Orchestrator](./images/copilot18.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/copilot19.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory = Fiber over the last 4 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

Vous devriez ensuite voir ceci, qui examine les tendances spécifiques à la fibre optique.

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4 Corréler les commandes avec les préférences de contenu

**Intention**

Testez l&#39;hypothèse selon laquelle une préférence pour un genre spécifique (p. ex., science-fiction, sports, dramatique) prédit le comportement de mise à niveau de la large bande, en particulier pour les besoins en bande passante élevée.

Tout d’abord, vous devez déterminer quel champ est utilisé pour stocker la préférence de genre.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

Vous devriez alors voir ceci, qui indique que le champ utilisé pour le genre est **_experienceplatform.individualFeatures.preferences.preferences.preferencesGenre**.

![Agent Orchestrator](./images/copilot23.png)

Avec ces informations, vous pouvez commencer à analyser en profondeur les données d’achat.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me ordersYTD by preferredGenre for the last 4 months
```

![Agent Orchestrator](./images/copilot24.png)

Vous devriez alors voir ceci. Cliquez sur **Afficher les données**.

![Agent Orchestrator](./images/copilot25.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/copilot26.png)

## 1.1.3.5 Identifier Les Parcours Fibre Existants

**Intention**

Découvrez quels parcours actifs ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

Vous devriez alors voir une liste des parcours.

![Agent Orchestrator](./images/copilot29.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/copilot33.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6 Validation des performances du parcours via l’analyse des abandons

**Intention**

Vous souhaitez comprendre l’abandon des performances du parcours pour déterminer s’il existe des nœuds ou des conditions dans le parcours qui enregistrent un pourcentage élevé de profils abandonnés. Cela permet de comprendre si des ajustements supplémentaires sont nécessaires dans le parcours.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/copilot38.png)

Faites défiler la page vers le bas pour afficher les observations et les recommandations. Cliquez sur le **de 3 points...**, puis sélectionnez **Détails du Parcours** pour ouvrir le parcours spécifique dans Adobe Journey Optimizer.

![Agent Orchestrator](./images/copilot40.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/copilot41.png)

Vous avez maintenant terminé ce Lab.

Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}