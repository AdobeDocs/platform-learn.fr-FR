---
title: Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer
description: Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 8%

---

# 1.4.2 Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer

## 1.4.2.1 Créer votre campagne dans Adobe Journey Optimizer

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP &#x200B;](./images/acoptriglp.png)

Vous allez maintenant créer une campagne. Contrairement au parcours basé sur un événement de l’exercice précédent, qui repose sur les événements d’expérience entrants, les entrées ou les sorties d’audience pour déclencher un parcours pour un client spécifique, les campagnes ciblent une audience entière une fois avec du contenu unique tel que des newsletters, des promotions ponctuelles ou des informations génériques, ou périodiquement avec du contenu similaire envoyé régulièrement, par exemple des campagnes d’anniversaire et des rappels.

Dans le menu, accédez à **Campagnes** et cliquez sur **Créer une campagne**.

![Journey Optimizer](./images/gsemail21.png)

Sélectionnez **Planifié - Marketing** et cliquez sur **Créer**.

![Journey Optimizer](./images/gsemail22.png)

Dans l’écran de création de la campagne, configurez les éléments suivants :

- **Nom** : `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Cliquez sur **Actions**.

![Journey Optimizer](./images/gsemail23.png)

Cliquez sur **+ Ajouter une action** puis sélectionnez **E-mail**.

![Journey Optimizer](./images/gsemail24.png)

Sélectionnez ensuite une **configuration d’e-mail** existante, puis cliquez sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail25.png)

Tu verras ça. Pour la **ligne d’objet**, utilisez la commande suivante :

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Cliquez ensuite sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail26.png)

Sélectionnez **Créer en partant de zéro**.

![Journey Optimizer](./images/gsemail27.png)

Vous devriez alors voir ceci.

![Journey Optimizer](./images/gsemail28.png)

Ajoutez 2x **1:1 colonne** à la zone de travail.

![Journey Optimizer](./images/gsemail29.png)

Accédez à **Fragments**, faites glisser le fragment **en-tête** vers la première colonne 1:1, puis faites glisser le fragment **pied de page** vers la deuxième colonne 1:1.

![Journey Optimizer](./images/gsemail30.png)

Ajoutez une nouvelle colonne 1:1 entre les 2 fragments, puis ajoutez une **Image** dans cette colonne 1:1. Cliquez ensuite sur **Parcourir**.

![Journey Optimizer](./images/gsemail31.png)

Accédez au dossier dans lequel vous avez stocké votre modèle Dynamic Media. Sélectionnez votre modèle Dynamic Media, puis cliquez sur **Sélectionner**.

![Journey Optimizer](./images/gsemail32.png)

Vous devriez alors voir ceci.

![Journey Optimizer](./images/gsemail33.png)

## Étapes suivantes

Revenir à [Adobe Experience Manager Assets et Dynamic Media](./aemassetsdm.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
