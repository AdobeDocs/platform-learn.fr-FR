---
title: Mapper une audience fédérée à S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Mapper une audience fédérée à S3
description: Dans cette leçon, nous allons mapper une audience fédérée à une destination Real-Time CDP en aval afin de prendre en charge une expérience hors ligne personnalisée.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Mapper l’audience fédérée à S3 pour exploiter les attributs d’audience à des fins d’enrichissement

Dans cet exercice, vous apprendrez à exploiter les attributs d’audience dans votre entrepôt de données afin d’enrichir l’expérience de votre audience dans les workflows d’activation en aval à l’aide des destinations RTCDP. Pour SecurFinancial, ces attributs fédérés peuvent être utilisés pour améliorer l’expérience de personnalisation hors ligne de l’audience du client. Dans cet exemple, nous allons mapper l’audience fédérée à une destination Amazon S3 préconfigurée.

## Étapes

1. Accédez au portail **Destinations**.

2. Cliquez sur le bouton **menu en forme de point** en regard de la destination Amazon S3 préconfigurée, puis cliquez sur **Activer les audiences**.

   ![activate-audiences](assets/activate-audiences.png)

3. Sélectionnez la destination **S3**, puis cliquez sur **Suivant**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Sélectionnez l’audience **SecureFinancial Customers - No Loans, Good Credit**.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Dans la section **Planification**, conservez tous les paramètres par défaut, puis cliquez sur **Suivant**.

6. À l’étape **Mappage**, assurez-vous que `xdm: personalEmail.address` est inclus et sélectionné comme **Clé de déduplication**. Cliquez ensuite sur **Suivant** :

   ![clé-déduplication](assets/deduplication-key.png)

7. Dans l’étape de mappage suivante, vous pouvez sélectionner des attributs d’enrichissement en fonction des mappages des champs d’audience dans la composition de l’audience fédérée. Cliquez sur l’icône **crayon (modifier)** pour afficher les attributs présélectionnés.

   ![edit-attributes](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Vérifiez le mappage des audiences et appuyez sur **Terminer**.

Nous sommes prêts à passer à [construire un parcours ](build-journey-federated-audience.md).
