---
title: Adobe Analytics et Claude.ai avec serveur MCP
description: Adobe Analytics et Claude.ai avec serveur MCP
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics et Claude.ai avec serveur MCP

[!BADGE Alpha]

+++Détails Alpha
En utilisant le fichier CJA &amp; Claude.ai avec le serveur MCP Alpha, vous reconnaissez que l’Alpha est fourni « en l’état », sans garantie d’aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Alpha. Il est conseillé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ces Alpha et/ou des éléments qui les accompagnent. Alpha est considéré comme des informations confidentielles d’Adobe. Tout « commentaire » (informations relatives à Alpha, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de l’utilisation d’Alpha, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

+++

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1 Créer une application personnalisée dans Claude.ai pour Adobe Analytics

>[!NOTE]
>
>L’utilisation d’Adobe Analytics dans Claude.ai requiert les éléments suivants :
>- une version payante de Claude.ai
>- utiliser le client web Claude.ai

Accédez à [https://claude.ai/](https://claude.ai/){target="_blank"} et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci. Cliquez sur l’icône **+** .

![Claude.ai](./images/claudeaa1.png)

Sélectionnez **Ajouter des connecteurs**.

![Claude.ai](./images/claudeaa2.png)

Cliquez sur **ajouter un élément personnalisé**.

![Claude.ai](./images/claudeaa3.png)

Renseignez les champs comme suit :

- **Nom** : `CJA`
- **URL du serveur MCP** : vérifiez auprès de votre représentant Adobe

Cliquez sur **Ajouter**.

![Claude.ai](./images/claudeaa4.png)

Vous devriez alors voir ceci. Cliquez sur **Connecter**.

![Claude.ai](./images/claudeaa5.png)

Une fois l’authentification terminée, vous devriez voir ceci. Cliquez sur l’icône **+** pour démarrer une nouvelle conversation.

![Claude.ai](./images/claudeaa6.png)

Accédez à **+**, à **Connecteurs** et vous devriez voir que le connecteur **Adobe Analytics** est maintenant activé.

![Claude.ai](./images/claudeaa7.png)

Vous êtes maintenant prêt à commencer votre analyse des données.

![Claude.ai](./images/claudeaa8.png)

## 1.5.3.2 Définir le contexte dans Adobe Analytics

Avant d’interagir davantage avec CJA via Claude.ai, le contexte doit être défini.

Pour cet exercice, le contexte doit être défini pour utiliser :

- **Suite de rapports** : **CID - Données de démonstration**

Le paramètre Suite de rapports permet d’identifier les données que Claude.ai doit examiner lorsqu’il pose des questions.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
list report suites
```

![Claude.ai](./images/claudeaa9.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai](./images/claudeaa10.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai](./images/claudeaa11.png)

Vous devriez alors voir quelque chose comme ça.

![Claude.ai](./images/claudeaa12.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
use report suite CID Demo Data
```

![Claude.ai](./images/claudeaa13.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai](./images/claudeaa14.png)

Votre suite de rapports a maintenant été sélectionnée.

![Claude.ai](./images/claudeaa15.png)

## 1.5.2.3 Explorer la suite de rapports

Saisissez l’élément suivant **Invite** et cliquez sur le bouton **envoyer** pour découvrir les mesures et dimensions disponibles.

```javascript
list the available metrics and dimensions
```

![Claude.ai &amp; CJA](./images/claudeaa101.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai &amp; CJA](./images/claudeaa102.png)

Sélectionnez **Toujours autoriser** à nouveau.

![Claude.ai &amp; CJA](./images/claudeaa103.png)

Vous devriez ensuite voir cette réponse, qui inclut les mesures et dimensions configurées dans cette suite de rapports.

![Claude.ai &amp; CJA](./images/claudeaa104.png)

## 1.5.2.4 Reports

Vous pouvez maintenant commencer à explorer les données. Commencez par saisir l’invite ci-dessous et cliquez sur **envoyer** pour envoyer votre demande de rapport.

```javascript
show me pageviews for Feb 2?
```

![Claude.ai &amp; CJA](./images/claudeaa105.png)

Vous devriez alors voir quelque chose comme ça.

![Claude.ai &amp; CJA](./images/claudeaa106.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
break down pageviews by page name
```

![Claude.ai &amp; CJA](./images/claudeaa107.png)

Vous devriez alors voir ceci.

![Claude.ai &amp; CJA](./images/claudeaa108.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai &amp; CJA](./images/claudeaa109.png)

Vous devriez alors voir quelque chose comme ça.

![Claude.ai &amp; CJA](./images/claudeaa110.png)

Faites défiler l’écran vers le bas pour afficher l’analyse.

![Claude.ai &amp; CJA](./images/claudeaa111.png)

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai &amp; CJA](./images/claudeaa112.png)

Vous devriez alors voir quelque chose comme ça.

![Claude.ai &amp; CJA](./images/claudeaa113.png)

Vous avez maintenant terminé cet exercice.

Revenir à [&#x200B; Analytics et agents &#x200B;](./analyticsagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}