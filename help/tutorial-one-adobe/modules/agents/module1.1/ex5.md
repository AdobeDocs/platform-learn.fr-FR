---
title: Adobe Marketing Agent pour Claude
description: Adobe Marketing Agent pour Claude
kt: 5342
doc-type: tutorial
exl-id: 2563ca77-699b-4cd3-af51-1105cea03c79
source-git-commit: 2339a3a9c122a3e757c59eec3a9be54acf8d9c1e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 9%

---

# 1.1.5 Adobe Marketing Agent pour Claude

[!BADGE Beta]

+++Détails Beta
En utilisant le Adobe Marketing Agent avec Claude Beta, vous reconnaissez que le Beta est fourni « en l&#39;état » sans garantie d&#39;aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce Beta et/ou des éléments qui l’accompagnent. Le Beta est considéré comme des informations confidentielles d’Adobe.  Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts que vous rencontrez lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ce commentaire.

+++

## Conditions préalables

Pour suivre les étapes de cet atelier, comme indiqué ci-dessous, vous devez disposer des droits d’accès suivants :

- Accès à Real-Time CDP, Journey Optimizer et Customer Journey Analytics
- Accès à l’assistant d’IA dans Adobe Experience Cloud
- Accès à AEP Agent Orchestrator
- Accès à Claude

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3482212?quality=12&learn=on)

Ce laboratoire est en cours de développement.

## 1.1.5.1 Créer une application personnalisée dans Claude.ai pour CJA

>[!NOTE]
>
>L’utilisation de Adobe Marketing Agent dans Claude.ai requiert les éléments suivants :
>- une version payante de Claude.ai

Accédez à [](https://claude.ai/){target="_blank"} et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci.

![Claude.ai](./images/claude1.png)

Cliquez pour ouvrir votre compte, puis sélectionnez **Paramètres**.

![Claude.ai](./images/claude2.png)

Accédez à **Connecteurs** puis cliquez sur **Accéder à la personnalisation**.

![Claude.ai](./images/claude2a.png)

Cliquez sur **+**, puis sélectionnez **Ajouter un connecteur personnalisé**.

![Claude.ai](./images/claude3.png)

Renseignez les champs comme suit :

- **Nom** : `Adobe Marketing Agent`
- **URL du serveur MCP** : demandez à votre représentant Adobe

Cliquez sur **Ajouter**.

![Claude.ai](./images/claude4.png)

Vous devriez alors voir ceci. Cliquez sur **+** pour démarrer une nouvelle conversation.

![Claude.ai](./images/claude5.png)

Cliquez sur l’icône **+**, accédez à **Connecteurs** et assurez-vous que **Adobe Marketing Agent** est activé.

![Claude.ai](./images/claude6.png)

## 1.1.5.2 Authentifier et définir le contexte

Avant d’interagir davantage avec Adobe Marketing Agent via Claude.ai, vous devez vous connecter et définir le contexte.

Saisissez l’invite suivante et cliquez sur **envoyer**.

```
login to Adobe Marketing Agent
```

![Claude.ai](./images/claude7.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai](./images/claude8.png)

Cliquez sur le lien pour vous connecter à l’agent marketing **.

![Claude.ai](./images/claude8a.png)

Cliquez sur **Ouvrir le lien**.

![Claude.ai](./images/claude8b.png)

Cliquez sur **Autoriser l’accès**.

![Claude.ai](./images/claude8c.png)

Une fois l’authentification terminée, vous devriez voir ceci. Revenez à Claude.

![Claude.ai](./images/claude8d.png)

Saisissez la commande suivante, puis cliquez sur **envoyer**.

```javascript
logged in
```

![Claude.ai](./images/claude8e.png)

Vous êtes maintenant connecté. L’étape suivante consiste à définir le contexte. Saisissez l’invite suivante et cliquez sur **envoyer**.


```javascript
change context
```

![Claude.ai &amp; CJA](./images/claude9.png)

Sélectionnez **Organisation**. Vous pouvez également répéter cette commande pour modifier ultérieurement le sandbox et la vue de données.

![Claude.ai &amp; CJA](./images/claude10.png)

Saisissez le nom de votre instance et cliquez sur **envoyer**.

![Claude.ai &amp; CJA](./images/claude11.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai &amp; CJA](./images/claude12.png)

Vous devriez alors voir quelque chose comme ça.

![Claude.ai &amp; CJA](./images/claude13.png)

Si le sandbox n’est pas encore défini correctement, vous pouvez utiliser la commande suivante pour passer au sandbox que vous devez utiliser. Cliquez sur **envoyer**. Vous pouvez également utiliser la `change context` de commande ci-dessus, puis sélectionner **sandbox**

```javascript
change sandbox to --aepSandboxName--
```

![Claude.ai &amp; CJA](./images/claude14.png)

Si la vue de données n’est pas encore définie correctement, vous pouvez utiliser la commande suivante pour passer au sandbox que vous devez utiliser (remplacez XXX dans la commande ci-dessous par le nom de votre vue de données). Cliquez sur **envoyer**. Vous pouvez également utiliser la `change context` de commande ci-dessus, puis sélectionner **vue de données**

```javascript
change dataview to XXX
```

![Claude.ai &amp; CJA](./images/claude15.png)

Une fois que les **Organisation**, **Sandbox** et **Vue de données** sont correctement définis, vous pouvez commencer à poser des questions à Adobe Marketing Agent.

## Étapes suivantes

Revenir à [](./agentorchestrator.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
