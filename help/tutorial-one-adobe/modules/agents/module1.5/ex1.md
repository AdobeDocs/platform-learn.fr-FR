---
title: CJA et ChatGPT avec le serveur MCP
description: CJA et ChatGPT avec le serveur MCP
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# 1.5.1 CJA et ChatGPT avec le serveur MCP

[!BADGE Alpha]

+++Détails Alpha
En utilisant le fichier CJA &amp; Claude.ai avec le serveur MCP Alpha, vous reconnaissez que l’Alpha est fourni « en l’état », sans garantie d’aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Alpha. Il est conseillé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ces Alpha et/ou des éléments qui les accompagnent. Alpha est considéré comme des informations confidentielles d’Adobe. Tout « commentaire » (informations relatives à Alpha, y compris, mais sans s’y limiter, les problèmes ou défauts rencontrés lors de l’utilisation d’Alpha, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ces commentaires.

+++

>[!NOTE]
>
>Cet exercice de configuration et d’utilisation d’un serveur MCP avec ChatGPT pour la connexion à CJA est lié à cet exercice [1.1 Customer Journey Analytics : créer un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La vue de données et la connexion CJA utilisées dans l’exercice ci-dessous sont la vue de données et la connexion configurées dans cet exercice. Si vous souhaitez répliquer les résultats ci-dessous, vous devez d’abord suivre ces instructions.

## Vidéo

Dans cette vidéo, vous obtiendrez une explication et une démonstration de toutes les étapes impliquées dans cet exercice.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Créer une application personnalisée dans ChatGPT pour CJA

>[!NOTE]
>
>L’utilisation de CJA dans ChatGPT nécessite ce qui suit :
>- une version payante du ChatGPT d’OpenAI
>- utilisant le client web ChatGPT ;

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

- **Nom** : `CJA`
- **URL du serveur MCP** : vérifiez auprès de votre représentant Adobe
- **Authentification** : `OAuth`

Cochez la case **Je comprends et je souhaite continuer**.

Cliquez sur **Créer**.

![ChatGPT](./images/chatgpt6.png)

Une fois la connexion établie, vous devriez constater que votre application CJA est maintenant connectée.

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2 Définir le contexte dans CJA

Fermez cette fenêtre.

![ChatGPT et CJA](./images/chatgpt9.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **+**, accédez à **Plus** puis sélectionnez **CJA**.

![ChatGPT et CJA](./images/chatgpt10.png)

Avant d’interagir davantage avec CJA par le biais du ChatGPT, le contexte doit être défini.

Pour cet exercice, le contexte doit être défini pour utiliser :

- **Vue de données** : **—aepUserLdap— - Vue de données omnicanal**

Le paramètre Vue de données permet d’identifier la vue de données que le GPT de conversation doit examiner lors de la pose de questions.

Saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
list dataviews
```

![ChatGPT et CJA](./images/chatgpt11.png)

Vous devriez alors voir une liste similaire des vues de données disponibles.

![ChatGPT et CJA](./images/chatgpt11a.png)

Pour modifier cela en vue de données à utiliser, saisissez l’invite **Prompt** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT et CJA](./images/chatgpt12.png)

Vous devriez alors voir ceci.

![ChatGPT et CJA](./images/chatgpt16.png)

Votre contexte est maintenant correctement défini, vous pouvez donc commencer à envoyer des invites spécifiques.

## 1.5.1.3 Explorer la vue de données

>[!NOTE]
>
>La vue de données utilisée ici a été configurée dans le cadre de l’exercice [Créer une vue de données](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Saisissez l’élément suivant **Invite** et cliquez sur le bouton **envoyer** pour découvrir les mesures et dimensions disponibles.

```javascript
list the available metrics and dimensions
```

![ChatGPT et CJA](./images/chatgpt101.png)

Vous devriez ensuite voir cette réponse, qui inclut les mesures et dimensions configurées dans le cadre de l’exercice [Créer une vue de données](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![ChatGPT et CJA](./images/chatgpt102.png)

## Tableau à structure libre 1.5.1.4 - Consultations de produit

Vous pouvez maintenant commencer à explorer les données. Commencez par saisir l’invite ci-dessous et cliquez sur **envoyer** pour envoyer votre demande de rapport.

```javascript
how many product views happened on January 21?
```

![ChatGPT et CJA](./images/chatgpt103.png)

Sélectionnez **ExécuterRapport**.

![ChatGPT et CJA](./images/chatgpt104.png)

Vous devriez alors voir une réponse comme celle-ci.

![ChatGPT et CJA](./images/chatgpt105.png)

Vous pouvez maintenant ventiler la réponse en ajoutant une dimension. Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
break down product views by product name
```

![ChatGPT et CJA](./images/chatgpt106.png)

Vous devriez alors voir une réponse comme celle-ci.

![ChatGPT et CJA](./images/chatgpt107.png)

Vous pouvez désormais également créer une visualisation. Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT et CJA](./images/chatgpt108.png)

Sélectionnez **UpsertProject**.

![ChatGPT et CJA](./images/chatgpt109.png)

Sélectionnez **ExécuterRapport**.

![ChatGPT et CJA](./images/chatgpt110.png)

Vous devriez alors voir ceci.

![ChatGPT et CJA](./images/chatgpt111.png)

Faites défiler vers le bas.

![ChatGPT et CJA](./images/chatgpt112.png)

Vous pouvez désormais également télécharger ce graphique linéaire . Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
export this chart to PNG
```

![ChatGPT et CJA](./images/chatgpt113.png)

Vous devriez alors voir ceci. Cliquez sur **Télécharger le fichier PNG**.

![ChatGPT et CJA](./images/chatgpt114.png)

Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT et CJA](./images/chatgpt115.png)

Sélectionnez **ExécuterRapport**.

![ChatGPT et CJA](./images/chatgpt116.png)

Vous devriez alors voir ceci.

![ChatGPT et CJA](./images/chatgpt117.png)

## Visualisation des abandons 1.5.1.5

Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT et CJA](./images/chatgpt118.png)

Sélectionnez **UpsertProject**.

![ChatGPT et CJA](./images/chatgpt119.png)

Sélectionnez **ExécuterRapport**.

![ChatGPT et CJA](./images/chatgpt120.png)

Vous devriez alors voir quelque chose comme ça. Saisissez l’**invite** suivante, puis cliquez sur le bouton **envoyer**.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT et CJA](./images/chatgpt120a.png)

Cliquez sur **Télécharger le fichier PNG**.

![ChatGPT et CJA](./images/chatgpt121.png)

La visualisation de l’analyse des abandons s’affiche maintenant.

![ChatGPT et CJA](./images/chatgpt122.png)

Étape suivante : [CJA et Claude.ai avec le serveur MCP](./ex2.md){target="_blank"}

Revenir à [&#x200B; Analytics et agents &#x200B;](./analyticsagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}