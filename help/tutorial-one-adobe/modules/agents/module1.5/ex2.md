---
title: CJA et Claude.ai avec serveur MCP
description: CJA et Claude.ai avec serveur MCP
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# 1.5.2 CJA et Claude.ai avec serveur MCP

[!BADGE Alpha]

+++Détails Alpha
En utilisant le fichier CJA &amp; Claude.ai avec le serveur MCP Alpha, vous reconnaissez que l’Alpha est fourni « en l’état », sans garantie d’aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Alpha. Il est conseillé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ces Alpha et/ou des éléments qui les accompagnent. Alpha est considéré comme des informations confidentielles d’Adobe. Tout « commentaire » (informations relatives à Alpha, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de l’utilisation d’Alpha, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

+++


>[!NOTE]
>
>Cet exercice de configuration et d’utilisation d’un serveur MCP avec Claude.ai pour la connexion à CJA est lié à cet exercice [1.1 Customer Journey Analytics : créer un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La vue de données et la connexion CJA utilisées dans l’exercice ci-dessous sont la vue de données et la connexion configurées dans cet exercice. Si vous souhaitez répliquer les résultats ci-dessous, vous devez d’abord suivre ces instructions.

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3479561?quality=12&learn=on)

## 1.5.2.1 Créer une application personnalisée dans Claude.ai pour CJA

>[!NOTE]
>
>L’utilisation de CJA dans Claude.ai requiert les éléments suivants :
>- une version payante de Claude.ai
>- utiliser le client web Claude.ai

Accédez à [https://claude.ai/](https://claude.ai/){target="_blank"} et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci. Cliquez sur l’icône **+** .

![Claude.ai](./images/claude1.png)

Sélectionnez **Ajouter des connecteurs**.

![Claude.ai](./images/claude2.png)

Cliquez sur **ajouter un élément personnalisé**.

![Claude.ai](./images/claude3.png)

Renseignez les champs comme suit :

- **Nom** : `CJA`
- **URL du serveur MCP** : vérifiez auprès de votre représentant Adobe

Cliquez sur **Ajouter**.

![Claude.ai](./images/claude4.png)

Vous devriez alors voir ceci. Cliquez sur **Connecter**.

![Claude.ai](./images/claude5.png)

Une fois l’authentification terminée, vous devriez voir ceci. Cliquez sur l’icône **+** pour démarrer une nouvelle conversation.

![Claude.ai](./images/claude6.png)

Accédez à **+**, à **Connecteurs** et vous devriez voir que le connecteur **CJA** est maintenant activé.

![Claude.ai](./images/claude8.png)

Vous êtes maintenant prêt à commencer votre analyse des données.

![Claude.ai](./images/claude7.png)

## 1.5.2.2 Définir le contexte dans CJA

Avant d’interagir davantage avec CJA via Claude.ai, le contexte doit être défini.

Pour cet exercice, le contexte doit être défini pour utiliser :

- **Vue de données** : **—aepUserLdap— - Vue de données omnicanal**

Le paramètre Vue de données permet d’identifier la vue de données que Claude.ai doit examiner lorsqu’il pose des questions.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
list dataviews
```

![Claude.ai &amp; CJA](./images/claude9.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai &amp; CJA](./images/claude10.png)

Vous devriez alors voir une liste similaire des vues de données disponibles.

![Claude.ai &amp; CJA](./images/claude11.png)

Pour modifier cela en vue de données à utiliser, saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai &amp; CJA](./images/claude11a.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai &amp; CJA](./images/claude12.png)

Vous devriez alors voir ceci.

![Claude.ai &amp; CJA](./images/claude16.png)

Votre contexte est maintenant correctement défini, vous pouvez donc commencer à envoyer des invites spécifiques.

## 1.5.2.3 Explorer la vue de données

>[!NOTE]
>
>La vue de données utilisée ici a été configurée dans le cadre de l’exercice [Créer une vue de données](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Saisissez l’élément suivant **Invite** et cliquez sur le bouton **envoyer** pour découvrir les mesures et dimensions disponibles.

```javascript
list the available metrics and dimensions
```

![Claude.ai &amp; CJA](./images/claude101.png)

Sélectionnez **Toujours autoriser** deux fois, une fois pour récupérer **mesures** et une seconde fois pour récupérer **dimensions**.

![Claude.ai &amp; CJA](./images/claude101a.png)

Vous devriez ensuite voir cette réponse, qui inclut les mesures et dimensions configurées dans le cadre de l’exercice [Créer une vue de données](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![Claude.ai &amp; CJA](./images/claude102.png)

## Tableau à structure libre 1.5.2.4 - Consultations de produit

Vous pouvez maintenant commencer à explorer les données. Commencez par saisir l’invite ci-dessous et cliquez sur **envoyer** pour envoyer votre demande de rapport.

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai &amp; CJA](./images/claude103.png)

Sélectionnez **Toujours autoriser**.

![Claude.ai &amp; CJA](./images/claude104.png)

Vous devriez alors voir une réponse comme celle-ci.

![Claude.ai &amp; CJA](./images/claude105.png)

Vous pouvez maintenant ventiler la réponse en ajoutant une dimension. Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
break down product views by product name
```

![Claude.ai &amp; CJA](./images/claude106.png)

Vous devriez alors voir une réponse comme celle-ci.

![Claude.ai &amp; CJA](./images/claude107.png)

Vous pouvez désormais également créer une visualisation. Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai &amp; CJA](./images/claude108.png)

Vous devriez alors voir ceci.

![Claude.ai &amp; CJA](./images/claude109.png)

Vous pouvez désormais également télécharger ce graphique linéaire . Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
export this chart to PNG
```

![Claude.ai &amp; CJA](./images/claude113.png)

Vous devriez alors voir ceci. Cliquez sur **Télécharger**.

![Claude.ai &amp; CJA](./images/claude114.png)

Vous pouvez ensuite ouvrir le fichier PNG téléchargé et l’utiliser dans d’autres documents.

![Claude.ai &amp; CJA](./images/claude114a.png)

Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
can you breakdown product views by user agent?
```

![Claude.ai &amp; CJA](./images/claude115.png)

Vous devriez alors voir ceci.

![Claude.ai &amp; CJA](./images/claude117.png)

## Visualisation des abandons 1.5.2.5

Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai &amp; CJA](./images/claude118.png)

Vous devriez ensuite voir un élément semblable à ceci, qui comprend une visualisation générée par Claude.ai à partir des données fournies par Customer Journey Analytics.

![Claude.ai &amp; CJA](./images/claude119.png)

Étape suivante : [Adobe Analytics et Claude.ai avec serveur MCP](./ex3.md){target="_blank"}

Revenir à [&#x200B; Analytics et agents &#x200B;](./analyticsagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}