---
title: Bootcamp - Customer Journey Analytics - Des insights à l'action
description: Bootcamp - Customer Journey Analytics - Des insights à l'action
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6 Des insights aux actions

## Objectifs

- Comprendre comment créer une audience à partir d’une vue collectée dans Customer Journey Analytics
- Utilisation de cette audience dans Real-Time CDP et Adobe Journey Optimizer

## 4.6.1 Création d’une audience et publication de celle-ci

Dans votre projet, vous avez créé un filtre appelé **Sentiments d’appel** et vous avez pu afficher le nombre d’utilisateurs pour lesquels leurs appels au centre d’appel sont classés comme **positifs**. Vous pouvez désormais créer un segment avec ces utilisateurs et les activer dans des parcours ou des canaux de communication.

La première étape est : dans le panneau créé lors du dernier exercice, sélectionnez la ligne **1. Appelez l’impression : positive**, cliquez avec le bouton droit et sélectionnez l’option **Créer une audience d’après la sélection** :

![demo](./images/aud1.png)

Attribuez ensuite un nom à votre audience en suivant le modèle **votreNom - appel d’audience CJA se sentant positif** :

![demo](./images/aud2.png)

Notez qu’il est possible de disposer d’un aperçu de l’audience en cours de création :

![demo](./images/aud3.png)

Enfin, cliquez sur **Publish**.

![demo](./images/aud4.png)

## 4.6.2 Utilisation de l’audience dans le cadre d’un segment

Revenez à Adobe Experience Platform, accédez à **Segments > Parcourir** et vous pourrez voir que votre segment créé dans CJA est prêt et disponible pour être utilisé dans vos activations et parcours !

![demo](./images/aud5.png)

Utilisons maintenant ce segment dans une activation Facebook et dans un parcours client !

## 4.6.3 Utilisation de votre segment dans Real-Time CDP en temps réel

Dans Adobe Experience Platform, accédez à **Segments > Parcourir** et recherchez l’audience que vous avez créée dans CJA :

![demo](./images/aud6.png)

Cliquez sur votre segment, puis sur **Activer à la destination** :

![demo](./images/aud7.png)

Sélectionnez la destination nommée **bootcamp-facebook**, puis cliquez sur **Suivant**.

![demo](./images/aud8.png)

Cliquez à nouveau sur **Suivant**.

![demo](./images/aud9.png)

Sélectionnez l&#39;option **Origine de votre audience** et définissez-la sur **Directly from clients**, puis cliquez sur **Suivant**.

![demo](./images/aud10.png)

Cliquez sur **Terminer**.

![demo](./images/aud11.png)

Votre segment est maintenant connecté à Facebook et ses audiences personnalisées. Utilisons maintenant ce même segment dans Adobe Journey Optimizer.

## 4.6.4 Utilisation de votre segment dans Adobe Journey Optimizer

Dans Adobe Experience Platform, cliquez sur **Journey Optimizer**, puis, dans le menu de gauche, cliquez sur **Parcours** et commencez à créer un parcours en cliquant sur **Créer un Parcours**.

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Ensuite, dans le menu de gauche, sous **Événements**, sélectionnez **Qualification de segment** et faites-le glisser vers le parcours :

![demo](./images/aud23.png)

Sous Segment, cliquez sur **Modifier** pour sélectionner un segment :

![demo](./images/aud24.png)

Sélectionnez l’audience que vous avez créée précédemment dans CJA et cliquez sur **Enregistrer**.

![demo](./images/aud25.png)

Prêt ! À partir de là, vous pouvez créer un parcours pour les clients qui remplissent les critères de ce segment.

[Retour au flux utilisateur 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
