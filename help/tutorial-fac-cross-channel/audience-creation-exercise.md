---
title: Création d’une audience
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Création d’une audience
description: Dans cette leçon, nous configurons une connexion entre Adobe Experience Platform et votre Data Warehouse d’entreprise pour activer la composition d’audiences fédérées.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---


# Exercice De Création D’Audience

Cet exercice vous guide tout au long de la création d’une audience à partir de votre Data Warehouse à l’aide de la composition d’audiences fédérées. Nous créons une audience pour qualifier les clients SecurFinancial qui ont une cote de crédit de 650 ou plus et qui n&#39;ont pas actuellement de prêt dans leur portefeuille SecurFinancial.

## Étapes

1. Sur le portail **Client > Audiences**, cliquez sur l’onglet **Compositions fédérées** .
2. Cliquez sur **Créer une composition**.

   ![create-composition](assets/create-composition.png)

3. Étiquetez votre composition comme `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Cliquez sur **Créer**.

4. Cliquez sur le bouton **+** dans la zone de travail et sélectionnez **Créer une audience**. Le rail de droite doit apparaître.

5. Cliquez sur **Sélectionner un schéma** puis sélectionnez le schéma **FSI_CRM** et cliquez sur **Confirmer**.

6. Cliquez sur **Continuer**. Dans la fenêtre du générateur de requêtes, cliquez sur le bouton **+**, puis sur **Condition personnalisée**. Créez les conditions suivantes :
   - `CURRENTPRODUCTS does not contain loan`
   - `AND`
   - `CREDITSCORE greater than or equal to 650`
   - Nous utilisons les données de préférence marketing pour segmenter les clients qui ont choisi l’e-mail comme canal de communication préféré :
   - `AND`
   - `CONSENTSMARKETINGPREFERRED equal to email`

   **Remarque :** le champ de valeur respecte la casse.

   Votre requête doit maintenant se présenter comme suit :

   ![query-builder](assets/query-builder.png)

7. Cliquez sur le bouton **+** suivant, puis sur **Enregistrer l’audience**.

   Étiqueter cette étape comme `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Utilisez la même valeur que le libellé de l’audience.

8. Ajoutez les mappages d’audience suivants :
   - **Champ Audience Source :** E-MAIL
   - **Champ d’audience Source :** CURRENTPRODUCTS
   - **Champ Audience Source :** PRÉNOM

9. Sélectionnez l’identité principale et l’espace de noms à utiliser pour les profils :
   - Champ d&#39;identité de Principal **&#x200B;**&#x200B;: e-mail
   - **Espace de noms d’identité :** e-mail

10. Cliquez sur **Enregistrer** puis sur **Démarrer** pour exécuter la requête de la composition que vous venez de créer.

**Remarque :** nous avons utilisé des informations sur les produits et le crédit pour créer notre audience qui n’a pas déplacé de données sensibles, telles que la cote de crédit, vers des plateformes en aval pour activation.

Pour plus d’informations sur la composition de l’audience, consultez [Experience League](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Maintenant que notre audience fédérée a été créée, nous allons procéder au [mappage à un compte S3](map-federated-audience-to-s3.md).
