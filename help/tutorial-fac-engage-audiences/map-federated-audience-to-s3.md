---
title: Mapper une audience fédérée à S3
seo-title: Map a federated audience to S3 | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Mapper une audience fédérée à S3
description: Dans cet exercice, nous allons mapper une audience fédérée à une destination Real-Time CDP en aval afin de prendre en charge une expérience hors ligne personnalisée.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Mapper l’audience fédérée à S3 pour exploiter les attributs d’audience à des fins d’enrichissement

Vous pouvez exploiter les attributs d’audience dans votre entrepôt de données pour enrichir l’expérience de votre audience dans les workflows d’activation en aval à l’aide des destinations RTCDP. Pour SecurFinancial, ces attributs fédérés peuvent être utilisés pour améliorer l’expérience de personnalisation hors ligne de l’audience du client. Ci-dessous, l’audience fédérée est mappée à une destination Amazon S3 préconfigurée.

## Étapes

1. Accédez au portail **Destinations**.

2. Cliquez sur le bouton **menu en forme de point** en regard de la destination Amazon S3 préconfigurée, puis cliquez sur **Activer les audiences**.

   ![activate-audiences](assets/activate-audiences.png)

3. Sélectionnez la destination **S3**, puis cliquez sur **Suivant**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Sélectionnez l’audience appropriée. Dans notre exemple : **SecureFinancial Customers - No Loans, Good Credit** audience.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Dans la section **Planification**, utilisez les paramètres par défaut et cliquez sur **Suivant**.

6. À l’étape **Mappage**, choisissez la clé de déduplication. Dans notre exemple, `xdm: personalEmail.address` est inclus et sélectionné comme **Clé de déduplication**. Cliquez ensuite sur **Suivant** :

   ![clé-déduplication](assets/deduplication-key.png)

7. À l’étape de mappage , sélectionnez des attributs d’enrichissement en fonction des mappages des champs d’audience dans la composition de l’audience fédérée. Cliquez sur l’icône **crayon (modifier)** pour afficher les attributs présélectionnés.

   ![edit-attributes](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Vérifiez le mappage des audiences et appuyez sur **Terminer**.

>[**!SUMMARY**]
>
> Nous avons créé une audience et l’avons activée facilement vers une destination S3. L’interface conviviale permet aux équipes marketing de créer et d’activer rapidement des audiences sans déplacer les données sous-jacentes.

Maintenant, nous allons [construire un parcours ](build-journey-federated-audience.md).
