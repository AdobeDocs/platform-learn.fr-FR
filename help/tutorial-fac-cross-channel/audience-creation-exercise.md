---
title: Création d’une audience
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Création d’une audience
description: Dans cet exercice visuel, nous configurons une connexion entre Adobe Experience Platform et votre Data Warehouse d’entreprise pour activer la composition d’audiences fédérées.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 4%

---

# Exercice De Création D’Audience

Ensuite, nous vous guiderons tout au long de la création d’une audience à partir de notre Data Warehouse à l’aide de la composition d’audiences fédérées. L’audience est composée de clients de SecurFinancial qui ont une cote de crédit de 650 ou plus et qui n’ont actuellement pas de prêt dans leur portefeuille de SecurFinancial.

## Étapes

1. Sur le portail **Client > Audiences**, cliquez sur l’onglet **Compositions fédérées** .
2. Cliquez sur **Créer une composition**.

   ![create-composition](assets/create-composition.png)

3. Étiquetez votre composition. Dans notre exemple : `SecurFinancial Customers - No Loans, Good Credit`. Cliquez sur **Créer**.

4. Cliquez sur le bouton **+** dans la zone de travail et sélectionnez **Créer une audience**. Le rail de droite s’affiche.

5. Cliquez sur **Sélectionner un schéma**, sélectionnez le schéma approprié, puis cliquez sur **Confirmer**.

6. Cliquez sur **Continuer**. Dans la fenêtre du générateur de requêtes, cliquez sur le bouton **+**, puis sur **Condition personnalisée**. Écrivez les conditions. Notre exemple utilise :

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *La dernière condition garantit que les données de préférences marketing sont utilisées pour segmenter les clients qui ont choisi l’e-mail comme canal de communication préféré*.

   **Remarque :** le champ de valeur respecte la casse.

   ![query-builder](assets/query-builder.png)

7. Cliquez sur le bouton **+** suivant, puis sur **Enregistrer l’audience**. Étiqueter cette étape. Dans notre exemple, nous l’étiquetons comme `SecurFinancial Customers - No Loans, Good Credit`.

8. Ajoutez les mappages d’audience pertinents. Dans cet exemple :

   - **Champ Audience Source :** E-MAIL
   - **Champ d’audience Source :** CURRENTPRODUCTS
   - **Champ Audience Source :** PRÉNOM

9. Sélectionnez l’identité principale et l’espace de noms à utiliser pour les profils. Il s’agit des identités et des champs utilisés pour nos données :

   - Champ d&#39;identité de Principal **&#x200B;**&#x200B;: e-mail
   - **Espace de noms d’identité :** e-mail

10. Cliquez sur **Enregistrer** puis sur **Démarrer** pour exécuter la requête de la composition.

>[**RÉSUMÉ**]
>
> Dans cet exemple, les informations sur les produits et le crédit ont été utilisées pour créer notre audience par le biais d’un accès direct aux données d’entreprise de Snowflake, sans en faire une copie dans Adobe Experience Platform. Une fois que le système externe traite la requête, seules les valeurs d’e-mail, de produits actuels et de prénom appropriées sont transférées vers la définition d’audience pour l’activation en aval. Cela s’applique à toutes les destinations prises en charge par RTCDP.

Pour plus d’informations sur la composition de l’audience, consultez [Experience League](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Maintenant que notre audience fédérée a été créée, nous allons la [mapper à un compte S3](map-federated-audience-to-s3.md).
