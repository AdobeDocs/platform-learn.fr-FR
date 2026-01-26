---
title: Adobe Marketing Agent pour ChatGPT Enterprise
description: Adobe Marketing Agent pour ChatGPT Enterprise
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# 1.1.2 Adobe Marketing Agent pour ChatGPT Enterprise

>[!IMPORTANT]
>
>Ce Lab utilise une fonctionnalité qui n&#39;a pas encore été publiée. La fonctionnalité est toujours en cours de développement, elle n’est donc pas encore disponible pour tous.

[!BADGE En développement]

+++Dans les détails du développement
En utilisant le Adobe Marketing Agent for ChatGPT Enterprise Beta, vous reconnaissez que le Beta est fourni « en l&#39;état » sans garantie d&#39;aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce Beta et/ou des éléments qui l’accompagnent. Le Beta est considéré comme des informations confidentielles d’Adobe.  Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts que vous rencontrez lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ce commentaire.

+++

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1 Créer une application personnalisée dans ChatGPT Enterprise pour Adobe Marketing Agent

>[!NOTE]
>
>L’utilisation de Adobe Marketing Agent dans ChatGPT nécessite ce qui suit :
>- une version payante du ChatGPT Enterprise d’OpenAI
>- en utilisant le client web ChatGPT Enterprise

Accédez à [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci. Cliquez sur votre nom d’utilisateur.

![ChatGPT](./images/chatgpt1.png)

Sélectionnez **Paramètres**.

![ChatGPT](./images/chatgpt2.png)

Accédez à **Applications** puis sélectionnez **Paramètres avancés**.

![ChatGPT](./images/chatgpt3.png)

Activez le **mode Développeur** puis cliquez sur **Précédent**.

![ChatGPT](./images/chatgpt4.png)

Cliquez sur **Créer une application**.

![ChatGPT](./images/chatgpt5.png)

Renseignez les champs comme suit :

- **Nom** : `Adobe Marketing Agent`
- **URL du serveur MCP** : vérifiez auprès de votre représentant Adobe
- **Authentification** : `OAuth`

Cochez la case **Je comprends et je souhaite continuer**.

Cliquez sur **Créer**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT va maintenant essayer de se connecter à votre compte Adobe. Sélectionnez **Autoriser l’accès** puis vous devrez vous connecter à l’aide de votre compte Adobe.

![ChatGPT](./images/chatgpt7.png)

Une fois la connexion établie, vous devriez voir que votre Adobe Marketing Agent est maintenant connecté.

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2 Définir le contexte dans Adobe Marketing Agent

Fermez cette fenêtre.

![Agent Orchestrator](./images/chatgpt9.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **+**, accédez à **Plus** puis sélectionnez **Adobe Marketing Agent**.

![Agent Orchestrator](./images/chatgpt10.png)

Avant d’interagir davantage avec Adobe Marketing Agent par le biais du ChatGPT, le contexte doit être défini.

Pour cet exercice, le contexte doit être défini pour utiliser :

- **Sandbox** : **Prod - Accélérer (VA7)**

Le paramètre Sandbox permet d’identifier le sandbox que le GPT de conversation doit examiner lorsqu’il pose des questions.

- **Vue de données** : **Accélérer le B2C 2026**

Le paramètre Vue de données permet d’identifier la vue de données que le GPT de conversation doit examiner lors de la pose de questions.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

Une liste similaire des sandbox disponibles devrait s’afficher. Le sandbox actuel de cet exemple est défini sur **prod**.

Pour le remplacer par le sandbox qui doit être utilisé, saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

Vous devriez alors voir ceci. Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/chatgpt13.png)

Vous devriez alors voir ceci. Saisissez l’élément suivant **Invite** et cliquez sur le bouton **envoyer** pour définir la vue de données à utiliser.

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

Vous devriez alors voir une liste similaire des vues de données disponibles.

Pour définir la vue de données à utiliser, saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

Vous devriez alors voir ceci. Cliquez sur **Définir le contexte**.

![Agent Orchestrator](./images/chatgpt16.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/chatgpt17.png)

Votre contexte est maintenant correctement défini, vous pouvez donc commencer à envoyer des invites spécifiques.

## 1.1.2.3 Commencez par les tendances d’achat globales pour ancrer le contexte et zoomer sur la fibre

**Intention**

Obtenez une impulsion de niveau supérieur sur la demande de catégorie (mobile, fixe, Internet, télévision, fibre optique), en particulier pour les 60 derniers jours. Cela définit des niveaux de référence pour la saisonnalité, les effets de promotion et la variance régionale après le déploiement à New York.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

Vous devriez alors voir ceci :

![Agent Orchestrator](./images/chatgpt19.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

Vous devriez ensuite voir ceci, qui examine les tendances spécifiques à la fibre optique.

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4 Corréler les commandes avec les préférences de contenu

**Intention**

Testez l&#39;hypothèse selon laquelle une préférence pour un genre spécifique (p. ex., science-fiction, sports, dramatique) prédit le comportement de mise à niveau de la large bande, en particulier pour les besoins en bande passante élevée.

Tout d’abord, vous devez déterminer quel champ est utilisé pour stocker la préférence de genre.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

Vous devriez alors voir ceci, qui indique que le champ utilisé pour le genre est **_experienceplatform.individualFeatures.preferences.preferences.preferencesGenre**.

![Agent Orchestrator](./images/chatgpt23.png)

Avec ces informations, vous pouvez commencer à analyser en profondeur les données d’achat.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

Vous devriez alors voir ceci. Cliquez sur **Recherche**.

![Agent Orchestrator](./images/chatgpt25.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/chatgpt26.png)

Faites défiler la page vers le bas pour afficher plus d’informations.

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5 Identifier Les Parcours Fibre Existants

**Intention**

Découvrez quels parcours actifs ou récemment conclus incluent « Fibre » dans le titre, par exemple, « Fibre Upgrade NYC - Sept », « Fibre Trial - Streaming Bundle ».

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

Vous devriez alors voir ceci. Cliquez sur **Recherche**.

![Agent Orchestrator](./images/chatgpt29.png)

Vous devriez alors voir une liste des parcours.

![Agent Orchestrator](./images/chatgpt30.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

Vous devriez alors voir ceci. Cliquez sur **Recherche**.

![Agent Orchestrator](./images/chatgpt32.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/chatgpt33.png)

Faites défiler la page vers le bas pour afficher plus de détails.

![Agent Orchestrator](./images/chatgpt34.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6 Validation des performances du parcours via l’analyse des abandons

**Intention**

Vous souhaitez comprendre l’abandon des performances du parcours pour déterminer s’il existe des nœuds ou des conditions dans le parcours qui enregistrent un pourcentage élevé de profils abandonnés. Cela permet de comprendre si des ajustements supplémentaires sont nécessaires dans le parcours.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

Vous devriez alors voir ceci.

![Agent Orchestrator](./images/chatgpt38.png)

Faites défiler l’écran vers le bas. Vous pouvez maintenant consulter le tableau en examinant chaque nœud et ses numéros d’entrée, numéros d’abandon et taux d’abandon respectifs.

![Agent Orchestrator](./images/chatgpt39.png)

Faites défiler la page vers le bas pour afficher les observations et les recommandations.

![Agent Orchestrator](./images/chatgpt40.png)

Vous avez maintenant terminé ce Lab.

Revenir à [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}