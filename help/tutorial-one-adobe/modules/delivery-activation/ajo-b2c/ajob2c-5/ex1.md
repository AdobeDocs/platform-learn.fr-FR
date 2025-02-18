---
title: Prise en main des services de traduction AJO
description: Prise en main des services de traduction AJO
kt: 5342
doc-type: tutorial
exl-id: ec032c58-c5c2-48d2-bdd3-ff860bc4a35a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 5%

---

# 3.5.1 Fournisseur De Traductions

## 3.5.1.1 Configurer Microsoft Azure Translator

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

## Dictionnaire de paramètres régionaux 3.5.1.2

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Journey Optimizer**.

![ Traductions ](./images/ajolp1.png)

Dans le menu de gauche, accédez à **Traductions** puis à **Dictionnaire des paramètres régionaux**. Si ce message s’affiche, cliquez sur **Ajouter des paramètres régionaux par défaut**.

![ Traductions ](./images/locale1.png)

Vous devriez alors voir ceci.

![ Traductions ](./images/locale2.png)

## 3.5.1.3 Configurer le fournisseur de traductions dans AJO

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

## 3.5.1.4 Configurer Le Projet De Traduction

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Journey Optimizer**.

![ Traductions ](./images/ajolp1.png)

Dans le menu de gauche, accédez à **Traductions** puis à **Dictionnaire des paramètres régionaux**. Si ce message s’affiche, cliquez sur **Créer un projet**.

![ Traductions ](./images/ajoprovider1.png)

Saisissez le nom `--aepUserLdap-- - Translations`, définissez les **paramètres régionaux Source** sur `[en-US] English - United States` et cochez les cases pour activer **Publier automatiquement les traductions approuvées** et **Activer le workflow de révision**. Cliquez ensuite sur **+ Ajouter un paramètre régional**.

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

## 3.5.1.5 Configurer Les Paramètres De Langue

Accédez à **Canaux** > **Paramètres généraux** > **Paramètres de langue**. Cliquez sur **Créer des paramètres de langue**.

![Journey Optimizer](./images/camploc6.png)

Utilisez le nom `--aepUserLdap--_translations`. Sélectionnez **Projet de traduction**. Cliquez ensuite sur l’icône **modifier**.

![Journey Optimizer](./images/camploc7.png)

Sélectionnez le projet de traduction que vous avez créé à l’étape précédente. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/camploc8.png)

Vous devriez alors voir ceci. Définissez la **préférence de secours** sur **Anglais - États-Unis**. Cliquez pour sélectionner **Sélectionner l’attribut de langue de profil préféré**, qui décidera du champ du profil client à utiliser pour charger les traductions. Cliquez ensuite sur l’icône **modifier** pour sélectionner le champ à utiliser.

![Journey Optimizer](./images/camploc9.png)

Saisissez **langue préférée** dans la barre de recherche, puis sélectionnez le champ **Langue préférée**.

![Journey Optimizer](./images/camploc10.png)

Cliquez sur l’icône **edit** pour **Anglais - États-Unis** et **Néerlandais** pour en vérifier la configuration.

![Journey Optimizer](./images/camploc11.png)

Voici la configuration pour **Anglais - États-Unis**. Cliquez sur **Annuler**.

![Journey Optimizer](./images/camploc12.png)

Cliquez pour voir la configuration pour **Néerlandais**. Cliquez sur **Annuler**.

![Journey Optimizer](./images/camploc13.png)

Faites défiler vers le haut et cliquez sur **Envoyer**.

![Journey Optimizer](./images/camploc14.png)

Vos paramètres de langue sont maintenant configurés.

![Journey Optimizer](./images/camploc15.png)

Vous avez terminé cet exercice.

## Étapes suivantes

Accédez à [3.5.2 Création de votre campagne](./ex2.md)

Revenez à [Adobe Journey Optimizer : Services de traduction](./ajotranslationsvcs.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
