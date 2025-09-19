---
title: Prise en main d’Adobe Commerce as a Cloud Service
description: Prise en main d’Adobe Commerce as a Cloud Service
kt: 5342
doc-type: tutorial
source-git-commit: 28553f8042be7bfc0b553272a6c72e6677fe1cb3
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 16%

---

# 1.5.1 Prise en main d’Adobe Commerce as a Cloud Service

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Assurez-vous que vous vous trouvez dans l’environnement correct, qui doit être nommé `--aepImsOrgName--`. Cliquez sur **Commerce**.

![AEM Assets](./images/accs1.png)

## 1.5.1.1 Créer votre instance ACCS

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter une instance**.

![AEM Assets](./images/accs2.png)

Renseignez les champs comme suit :

- **Nom de l’instance** : `--aepUserLdap-- - ACCS`
- **Environnement** : `Sandbox`
- **Region** : `North America`

Cliquez sur **Ajouter une instance**.

![AEM Assets](./images/accs3.png)

Votre instance est en cours de création. Cela peut prendre 5 à 10 minutes.

![AEM Assets](./images/accs4.png)

Une fois l’instance prête, cliquez sur votre instance pour l’ouvrir.

![AEM Assets](./images/accs5.png)

## 1.5.1.2 Configurer votre boutique CitiSignal

Vous devriez alors voir ceci. Cliquez sur **Se connecter avec Adobe ID** puis connectez-vous.

![AEM Assets](./images/accs6.png)

Une fois la connexion effectuée, vous devriez voir cette page d’accueil. La première étape consiste à configurer votre boutique CitiSignal dans Commerce. Cliquez sur **Magasins**.

![AEM Assets](./images/accs7.png)

Cliquez sur **Toutes les boutiques**.

![AEM Assets](./images/accs8.png)

Cliquez sur **Créer un site web**.

![AEM Assets](./images/accs9.png)

Renseignez les champs comme suit :

- **Nom** : `CitiSignal`
- **Code** : `citisignal`

Cliquez sur **Enregistrer le site web**.

![AEM Assets](./images/accs10.png)

Tu devrais alors être de retour ici. Cliquez sur **Créer une boutique**.

![AEM Assets](./images/accs11.png)

Renseignez les champs comme suit :

- **Site Web** : `CitiSignal`
- **Nom** : `CitiSignal`
- **Code** : `citisignal`
- **Catégorie racine** : `Default Category`

Cliquez sur **Enregistrer la boutique**.

![AEM Assets](./images/accs12.png)

Tu devrais alors être de retour ici. Cliquez sur **Créer une vue de magasin**.

![AEM Assets](./images/accs13.png)

Renseignez les champs comme suit :

- **Store** : `CitiSignal`
- **Nom** : `CitiSignal`
- **Code** : `citisignal`
- **Statut** : `Enabled`

Cliquez sur **Enregistrer la vue de la boutique**.

![AEM Assets](./images/accs14.png)

Vous devriez alors voir ce message. Cliquez sur **OK**.

![AEM Assets](./images/accs15.png)

Tu devrais alors être de retour ici.

![AEM Assets](./images/accs16.png)

## 1.5.1.3 Configurer les catégories et les produits

Accédez à **Catalogue** puis sélectionnez **Catégories**.

![AEM Assets](./images/accs17.png)

Sélectionnez **Catégorie par défaut** puis cliquez sur **Ajouter une sous-catégorie**.

![AEM Assets](./images/accs18.png)

Saisissez le nom `Phones`, puis cliquez sur **Enregistrer**.

![AEM Assets](./images/accs19.png)

Sélectionnez **Catégorie par défaut** puis cliquez de nouveau sur **Ajouter une sous-catégorie**.

![AEM Assets](./images/accs20.png)

Saisissez le nom `Watches`, puis cliquez sur **Enregistrer**.

![AEM Assets](./images/accs21.png)

Vous devriez alors avoir 2 catégories créées.

![AEM Assets](./images/accs22.png)

Ensuite, accédez à **Catalogue** puis sélectionnez **Produits**.

![AEM Assets](./images/accs23.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter un produit**.

![AEM Assets](./images/accs24.png)

Configurez votre produit comme suit :

- **Nom du produit** : `iPhone Air`
- **SKU** : `iPhone-Air`
- **Prix** : `999`
- **Quantité** : `10000`
- **Catégories** : sélectionnez `Phones`

Cliquez sur **Enregistrer**.

![AEM Assets](./images/accs25.png)

Faites défiler jusqu’à **Configurations** et cliquez sur **Créer des configurations**.

![AEM Assets](./images/accs26.png)

Vous devriez alors voir ceci. Cliquez sur **Créer un attribut**.

![AEM Assets](./images/accs27.png)

Définissez le **Libellé par défaut** sur `Storage`, puis cliquez sur **Ajouter une option** sous **Gérer les options**.

![AEM Assets](./images/accs28.png)

Configurez la première option en utilisant le nom `256GB` dans les 3 colonnes, puis cliquez de nouveau sur **Ajouter une option**.

![AEM Assets](./images/accs29.png)

Configurez la deuxième option en utilisant le nom `512GB` dans les 3 colonnes, puis cliquez de nouveau sur **Ajouter une option**.

![AEM Assets](./images/accs30.png)

Configurez la troisième option en utilisant le nom `1TB` dans les 3 colonnes, puis cliquez de nouveau sur **Ajouter une option**.

![AEM Assets](./images/accs31.png)

Faites défiler jusqu’à **Propriétés du storefront**. Définissez les options suivantes sur **Oui** :

- **Utiliser dans la recherche**
- **Autoriser les balises HTML sur Storefront**
- **Visible sur les pages de catalogue sur Storefront**
- **Utiliser dans la liste de produits**

![AEM Assets](./images/accs32.png)

Faites défiler vers le haut et cliquez sur **Enregistrer l’attribut**.

![AEM Assets](./images/accs33.png)

Vous devriez alors voir ceci. Sélectionnez les deux attributs **couleur** et **stockage**, puis cliquez sur **Suivant**.

![AEM Assets](./images/accs34.png)

Vous devriez alors voir ceci. Vous devez maintenant ajouter les options de couleur disponibles. Pour ce faire, cliquez sur **Créer une valeur**.

![AEM Assets](./images/accs35.png)

Saisissez la valeur `Sky-Blue` et cliquez sur **Créer une valeur**.

![AEM Assets](./images/accs36.png)

Saisissez la valeur `Light-Gold` et cliquez sur **Créer une valeur**.

![AEM Assets](./images/accs37.png)

Saisissez la valeur `Cloud-White` et cliquez sur **Créer une valeur**.

![AEM Assets](./images/accs38.png)

Saisissez la valeur `Space-Black`. Cliquez sur **Tout sélectionner**

![AEM Assets](./images/accs39.png)

Sélectionnez les 3 options sous **Stockage** et cliquez sur **Suivant**.

![AEM Assets](./images/accs40.png)

Laissez les paramètres par défaut et cliquez sur **Suivant**.

![AEM Assets](./images/accs41.png)

Vous devriez alors voir ceci. Cliquez sur **Générer des produits**.

![AEM Assets](./images/accs42.png)

Cliquez sur **Enregistrer**.

![AEM Assets](./images/accs43.png)

Faites défiler jusqu’à **Produit dans Sites web** et cochez la case **CitiSignal**.

Cliquez sur **Enregistrer**.

![AEM Assets](./images/accs44.png)

Cliquez sur **Confirmer**.

![AEM Assets](./images/accs45.png)

Vous devriez alors voir ceci. Cliquez sur **Précédent**.

![AEM Assets](./images/accs46.png)

Le produit **iPhone Air** et ses variantes s’affichent désormais dans le catalogue de produits.

![AEM Assets](./images/accs47.png)


Étape suivante : [Connexion d’ACCS au storefront AEM Sites CS/EDS](./ex2.md){target="_blank"}

Revenir à [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
