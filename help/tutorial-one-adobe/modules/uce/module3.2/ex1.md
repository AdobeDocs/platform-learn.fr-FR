---
title: Prise en main des services de traduction AJO
description: Prise en main des services de traduction AJO
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---

# 3.2.1 Fournisseur De Traductions

## 3.2.1.1 Configurer Microsoft Azure Translator

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home).

![ Traductions ](./images/transl1.png)

Dans la barre de recherche, saisissez `translators`. Cliquez ensuite sur **+ Créer**.

![ Traductions ](./images/transl2.png)

Sélectionnez **Créer un traducteur**.

![ Traductions ](./images/transl3.png)

Choisissez votre **ID d’abonnement** et **Groupe de ressources**.
Définissez **Region** sur **Global**.
Définissez **Pricing Tier** sur **Free F0**.

Sélectionnez **Réviser + créer**.

![ Traductions ](./images/transl4.png)

Sélectionnez **Créer**.

![ Traductions ](./images/transl5.png)

Sélectionnez **Accéder à la ressource**.

![ Traductions ](./images/transl6.png)

Dans le menu de gauche, accédez à **Gestion des ressources** > **Clés et point d’entrée**. Cliquez pour copier votre clé.

![ Traductions ](./images/transl7.png)

## Dictionnaire de paramètres régionaux 3.2.1.2

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Journey Optimizer**.

![ Traductions ](./images/ajolp1.png)

Dans le menu de gauche, accédez à **Traductions** puis à **Dictionnaire des paramètres régionaux**. Si ce message s’affiche, cliquez sur **Ajouter des paramètres régionaux par défaut**.

![ Traductions ](./images/locale1.png)

Vous devriez alors voir ceci.

![ Traductions ](./images/locale2.png)

## 3.2.1.3 Configurer le fournisseur de traductions dans AJO

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Journey Optimizer**.

![ Traductions ](./images/ajolp1.png)

Dans le menu de gauche, accédez à **Traductions** puis à **Fournisseurs**. Cliquez sur **Ajouter un fournisseur**.

![ Traductions ](./images/transl8.png)

Sous **Fournisseurs**, sélectionnez **Traducteur Microsoft**. Cochez la case pour activer l’utilisation du fournisseur de traduction. Collez la clé que vous avez copiée à partir de Microsoft Azure Translators. Cliquez ensuite sur **Valider les informations d’identification**.

![ Traductions ](./images/transl9.png)

Vos informations d’identification doivent ensuite être validées avec succès. Si elles le sont, faites défiler la page vers le bas pour sélectionner les langues à traduire.

![ Traductions ](./images/transl10.png)

Veillez à sélectionner `[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`.

![ Traductions ](./images/transl11.png)

Faites défiler vers le haut et cliquez sur **Enregistrer**.

![ Traductions ](./images/transl12.png)

Votre **fournisseur de traduction** est maintenant prêt à être utilisé.

![ Traductions ](./images/transl13.png)

## 3.2.1.4 Configurer Le Projet De Traduction

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Journey Optimizer**.

![ Traductions ](./images/ajolp1.png)

Dans le menu de gauche, accédez à **Traductions** puis à **Dictionnaire des paramètres régionaux**. Si ce message s’affiche, cliquez sur **Créer un projet**.

![ Traductions ](./images/ajoprovider1.png)

Saisissez le nom `--aepUserLdap-- - Translations`, définissez les **paramètres régionaux Source** sur `[en-US] English - United States` et cochez la case pour activer **Publier automatiquement les traductions approuvées**. Cliquez ensuite sur **+ Ajouter un paramètre régional**.

![ Traductions ](./images/ajoprovider1a.png)

Recherchez `fr`, activez la case à cocher pour `[fr] French`, puis activez la case à cocher pour **Microsoft Translator**. Cliquez sur **+ Ajouter un paramètre régional**.

![ Traductions ](./images/ajoprovider2.png)

Recherchez `es`, activez la case à cocher pour `[es] Spanish`, puis activez la case à cocher pour **Microsoft Translator**. Cliquez sur **+ Ajouter un paramètre régional**.

![ Traductions ](./images/ajoprovider3.png)

Recherchez `nl`, activez la case à cocher pour `[nl] Spanish`, puis activez la case à cocher pour **Microsoft Translator**. Cliquez sur **+ Ajouter un paramètre régional**.

![ Traductions ](./images/ajoprovider6.png)

Cliquez sur **Enregistrer**.

![ Traductions ](./images/ajoprovider8.png)

Votre projet **Traductions** est maintenant prêt à être utilisé.

![ Traductions ](./images/ajoprovider9.png)

Vous avez terminé cet exercice.

## Étapes suivantes

Accédez à [3.2.2 Création de votre campagne](./ex2.md)

Revenir au [module 3.2](./ajotranslationsvcs.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}