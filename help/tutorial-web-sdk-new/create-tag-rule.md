---
title: Création d’une règle de balise
description: Découvrez comment envoyer un événement à Platform Edge Network avec votre objet XDM à l’aide d’une règle de balise. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Tags
source-git-commit: 695c12ab66df33af00baacabc3b69eaac7ada231
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 3%

---

# Création d’une règle de balise

Découvrez comment envoyer un événement à Platform Edge Network avec votre objet XDM à l’aide d’une règle de balise. Une règle de balise est une combinaison d’événements, de conditions et d’actions qui indique à la propriété de balise de faire quelque chose.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon s’appuient sur l’exemple utilisé pendant la [Création d’éléments de données](create-data-elements.md) étape ; envoi d’une action d’événement XDM pour capturer le contenu et les identités des utilisateurs sur la [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Utilisation d’une convention d’affectation de nom pour la gestion des règles dans les balises
* Créer une règle de balise pour envoyer un événement XDM
* Publier une règle de balise dans une bibliothèque de développement


## Conditions préalables

Vous connaissez bien les balises de collecte de données et la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html), et vous devez avoir suivi les leçons précédentes suivantes dans le tutoriel :

* [Configuration des autorisations](configure-permissions.md)
* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Créer des éléments de données](create-data-elements.md)

## Conventions de nommage

Pour mieux gérer les règles dans les balises, il est recommandé de respecter une convention d’affectation des noms standard. Ce tutoriel utilise une convention de dénomination en trois parties :

* [location] - [event] - [outil]

où ;

1. location correspond à la ou aux pages du site sur lesquelles la règle se déclenche.
1. est le déclencheur qui déclenche la balise
1. est l’application ou les applications spécifiques utilisées dans l’étape d’action pour cette règle.


## Créer une règle de balise

Dans les balises, les règles sont utilisées pour exécuter des actions (appels de déclenchement) sous diverses conditions. Vous utiliserez cette première règle pour envoyer l’objet XDM au réseau Edge à l’aide du SDK Web. [!UICONTROL Envoyer un événement] action. Plus loin dans ce tutoriel, vous enverrez différentes versions de l’objet XDM en fonction du type de page sur laquelle se trouve le visiteur. C’est pourquoi vous utiliserez des conditions de règle pour exclure ces autres types de pages.

Pour créer une règle de balise :

1. Ouvrez la propriété de balise que vous utilisez pour ce tutoriel.
1. Accédez à **[!UICONTROL Règles]** dans la navigation de gauche
1. Sélectionnez la variable **[!UICONTROL Créer une règle]** button
   ![Création d’une règle](assets/rules-create.png)
1. Donnez à la règle le nom `all pages - library load - AA & AT`.

   >[!NOTE]
   >
   > Cette règle sera utilisée de manière spécifique par Adobe Analytics et Target dans une leçon ultérieure, c’est pourquoi `AA & AT` est utilisée à la fin du nom.

1. Dans le **[!UICONTROL Événements]** , sélectionnez **[!UICONTROL Ajouter]**
   ![Attribuez un nom à la règle et ajoutez un événement](assets/rule-name.png)
1. Utilisez la variable **[!UICONTROL Extension Core]** et sélectionnez `Library Loaded (Page Top)` comme la propriété **[!UICONTROL Type d’événement]**.

   Ce paramètre signifie que la règle se déclenche chaque fois que la bibliothèque de balises se charge sur une page.
1. Sélectionner **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de la règle principale
   ![Ajout de l’événement Library Loaded (Bibliothèque chargée)](assets/rule-event-pagetop.png)
1. Dans le **[!UICONTROL Conditions]** , sélectionnez **[!UICONTROL Ajouter]** button
   ![Ajouter des conditions](assets/rules-add-conditions.png)
1. Sélectionner **[!UICONTROL Type de logique]** `Exception`, **[!UICONTROL Extension]** `Core`, et **[!UICONTROL Type de condition]** `Path Without Query String`
1. Saisissez le chemin de l’URL. `/content/luma/us/en/user/cart.html` dans le **[!UICONTROL path est égal à]** et **[!UICONTROL name]** it `Core - cart page`
1. Sélectionner **[!UICONTROL Conserver les modifications]**
   ![Ajouter des conditions](assets/rule-condition-exception.png)
1. Ajouter trois autres exceptions pour les chemins d’URL suivants

   * **`Core - checkout page`** for `/content/luma/us/en/user/checkout.html`
   * **`Core - thank you page`** for `/content/luma/us/en/user/checkout/order/thank-you.html`
   * **`Core - product page`** pour `/products/` l’interrupteur Regex étant activé

   ![Ajouter des conditions](assets/rule-condition-exception-all.png)

1. Dans le **[!UICONTROL Actions]** , sélectionnez **[!UICONTROL Ajouter]**
1. Sélectionner **[!UICONTROL SDK Web Adobe Experience Platform]** comme la propriété **[!UICONTROL Extension]**
1. Sélectionner **[!UICONTROL Envoyer un événement]** comme la propriété **[!UICONTROL Type d’action]**
1. Sélectionner **[!UICONTROL web.webpagedetails.pageViews]** comme la propriété **[!UICONTROL Type]**.

   >[!WARNING]
   >
   > Cette liste déroulante renseigne la variable **`xdm.eventType`** dans l’objet XDM. Bien que vous puissiez également saisir des libellés de forme libre dans ce champ, il est vivement recommandé de **ne pas** car cela aura des effets négatifs avec Platform.

1. Comme la variable **[!UICONTROL Données XDM]**, sélectionnez la variable `xdm.content` élément de données créé dans la leçon précédente
1. Sélectionner **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de la règle principale

   ![Ajout de l’action Envoyer l’événement](assets/rule-set-action-xdm.png)
1. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer la règle

   ![Enregistrer la règle](assets/rule-save.png)

## Publier la règle dans une bibliothèque

Ensuite, publiez la règle dans votre environnement de développement afin que nous puissions vérifier qu’elle fonctionne.

Pour créer une bibliothèque :

1. Accédez à **[!UICONTROL Flux de publication]** dans la navigation de gauche
1. Sélectionner **[!UICONTROL Ajouter une bibliothèque]**

   ![Sélectionner Ajouter une bibliothèque](assets/rule-publish-library.png)
1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Web SDK Tutorial`
1. Pour le **[!UICONTROL Environnement]**, sélectionnez `Development`
1. Sélectionner  **[!UICONTROL Ajouter toutes les ressources modifiées]**

   >[!NOTE]
   >
   >    Outre l’extension du SDK Web de Adobe Experience Platform et la variable `all pages - library load - AA & AT` , vous verrez les composants de balise créés dans les leçons précédentes. L’extension Core contient le code JavaScript de base requis par toutes les propriétés de balise Web.

1. Sélectionner **[!UICONTROL Enregistrement et création pour le développement]**

   ![Création et création de la bibliothèque](assets/rule-publish-add-all-changes.png)

La création de la bibliothèque peut prendre quelques minutes. Une fois l’opération terminée, un point vert s’affiche à gauche du nom de la bibliothèque :

![Build complete](assets/rule-publish-success.png)

Comme vous pouvez le voir sur la [!UICONTROL Flux de publication] le processus de publication, qui dépasse le cadre de ce tutoriel, contient beaucoup d’autres éléments. Ce tutoriel utilise une seule bibliothèque dans votre environnement de développement.

Vous êtes maintenant prêt à valider les données de la requête à l’aide de l’Adobe Experience Platform Debugger .

[Suivant ](validate-with-debugger.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
