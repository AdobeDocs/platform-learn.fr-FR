---
title: Création de règles pour le suivi des événements de page vue et de commerce
description: Création de règles pour le suivi des événements de page vue et de commerce
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Création de règles pour le suivi des événements de page vue et de commerce

Pour vérifier que l’utilisateur a consulté la page du produit, créez une règle dans les balises Adobe Experience Platform. Pour ce faire, cliquez sur [!UICONTROL Règles] dans le menu de gauche, puis cliquez sur [!UICONTROL Ajouter une règle].

Pour le nom de la règle, saisissez _Page vue_.

## Ajout d’un événement

Cliquez sur le bouton [!UICONTROL Ajouter] sous [!UICONTROL Événements]. Vous affichez maintenant la vue d’événement. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL Adobe de la couche de données client]. Pour le [!UICONTROL Type d’événement] champ, sélectionnez [!UICONTROL Données transférées].

Parce que vous souhaitez que cette règle soit déclenchée uniquement lorsque la variable `pageViewed` est transmis à la couche de données, select [!UICONTROL Evénement spécifique] under [!UICONTROL Écoute] et type _pageViewed_ dans la [!UICONTROL Événement/Clé à enregistrer pour] Champ de texte.

![Événement de consultation de page](../../../assets/implementation-strategy/page-viewed-event.png)

Cliquez sur [!UICONTROL Conserver les modifications].

## Ajouter une action

Maintenant que vous êtes de retour à l’affichage des règles, cliquez sur le bouton [!UICONTROL Ajouter] sous [!UICONTROL Actions]. Vous devriez maintenant être dans la vue d’action. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL SDK Web Adobe Experience Platform]. Pour le [!UICONTROL Type d’action] champ, sélectionnez [!UICONTROL Envoyer un événement]. Cette action vous permet d’envoyer un événement d’expérience à Adobe Experience Platform Edge Network.

Dans la partie droite de l’écran, recherchez le [!UICONTROL Type] champ et sélectionnez `web.webpagedetails.pageViews`. Il s’agit de l’un des types d’événements d’expérience canoniques fournis par défaut par Adobe Experience Platform. Il représente une page vue.

Pour le [!UICONTROL Données XDM] champ, entrer `%event.fullState%`. Cela indique que l’état calculé (également appelé état complet) de la couche de données, capturé au moment du déclenchement de la règle, doit être envoyé dans le cadre de l’événement d’expérience.

![Action Page vue](../../../assets/implementation-strategy/page-viewed-action.png)

Si les données que vous avez transmises à la couche de données à partir de votre site web ne sont pas conformes à votre schéma XDM ou si vous souhaitez uniquement envoyer une partie de l’état calculé de la couche de données, utilisez la variable [!UICONTROL Objet XDM] type d’élément de données (fourni par l’extension SDK Web de Adobe Experience Platform) pour créer un objet approprié qui correspond à votre schéma.

Cliquez sur le bouton [!UICONTROL Conserver les modifications] bouton .

## Enregistrez la règle

Votre règle doit maintenant être terminée.

![Règle de consultation de page](../../../assets/implementation-strategy/page-viewed-rule.png)

Enregistrez la règle en cliquant sur [!UICONTROL Enregistrer].

## Répétez le processus.

Répétez le processus décrit ci-dessus pour créer des règles pour lorsqu’un produit est affiché, qu’un panier est ouvert et qu’un produit est ajouté au panier. Les seules différences entre les règles seront le nom de la règle, la valeur saisie dans la variable [!UICONTROL Événement/Clé à enregistrer pour] dans le champ [!UICONTROL Données transférées] et la variable [!UICONTROL Type] dans le champ [!UICONTROL Envoyer un événement] action. Voici les valeurs de chaque règle :

Règle de consultation du produit :

* **Nom de la règle**: _Produit consulté_
* **Événement/Clé à enregistrer pour** dans [!UICONTROL Données transférées] event: `productViewed`
* **Type** dans [!UICONTROL Envoyer un événement] action : `commerce.productViews`

Règle d’ouverture de panier :

* **Nom de la règle**: _Panier ouvert_
* **Événement/Clé à enregistrer pour** dans [!UICONTROL Données transférées] event: `cartOpened`
* **Type** dans [!UICONTROL Envoyer un événement] action : `commerce.productListOpens`

Produit ajouté à la règle de panier :

* **Nom de la règle**: _Produit Ajouté Au Panier_
* **Événement/Clé à enregistrer pour** dans [!UICONTROL Données transférées] event: `productAddedToCart`
* **Type** dans [!UICONTROL Envoyer un événement] action : `commerce.productListAdds`

Ensuite, nous allons gérer les clics de suivi sur le [!UICONTROL Téléchargement de l’application] lien.
