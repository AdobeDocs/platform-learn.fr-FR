---
title: Création d’une règle de balise
description: Découvrez comment envoyer un événement à Platform Edge Network avec votre objet XDM à l’aide d’une règle de balise. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# Création d’une règle de balise

Découvrez comment envoyer un événement à Platform Edge Network avec votre objet XDM à l’aide d’une règle de balise. Une règle de balise est une combinaison d’événements, de conditions et d’actions qui indique à la propriété de balise de faire quelque chose.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon s’appuient sur l’exemple utilisé pendant la [Création d’identités](create-identities.md) étape ; envoi d’une action d’événement XDM pour capturer le contenu et les identités des utilisateurs sur la [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pouvez :

* Utilisation d’une convention d’affectation de nom pour la gestion des règles dans les balises
* Envoi d’un événement XDM à l’aide des types d’action Mettre à jour une variable et Envoyer un événement dans une règle de balise
* Publier une règle de balise dans une bibliothèque de développement


## Conditions préalables

Vous connaissez bien les balises de collecte de données et la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html), et vous devez avoir suivi les leçons précédentes suivantes dans le tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Créer des éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)

## Conventions de nommage

Pour mieux gérer les règles dans les balises, il est recommandé de respecter une convention d’affectation des noms standard. Ce tutoriel utilise une convention de dénomination en trois parties :

* [**location**] - [**event**] - [**outil**] (**séquence**)

où ;

1. **location** est la ou les pages du site sur lesquelles la règle se déclenche.
1. **event** est le déclencheur de la règle.
1. **outil** correspond à l’application ou aux applications spécifiques utilisées à l’étape d’action pour cette règle.
1. **séquence** est l’ordre dans lequel la règle doit se déclencher par rapport aux autres règles.
<!-- minor update -->

## Créer une règle de balise

Dans les balises, les règles sont utilisées pour exécuter des actions (appels de déclenchement) sous diverses conditions. L’extension de balises SDK Web Platform comprend deux actions qui seront utilisées dans cette leçon :

* **[!UICONTROL Mettre à jour la variable]** mappe des éléments de données aux champs XDM ;
* **[!UICONTROL Envoyer un événement]** envoie l’objet XDM à Experience Platform Edge Network

### Mettre à jour la variable

Créez cette première règle en tant que &quot;configuration globale&quot; pour définir toutes les variables de contenu essentielles dans l’objet XDM à l’aide des SDK Web Platform. **[!UICONTROL Mettre à jour la variable]** action. Ensuite, créez une deuxième règle, séquencée pour la déclencher après la première, pour envoyer l’objet XDM à Platform Edge Network à l’aide de l’événement **[!UICONTROL Envoyer un événement]** action. Plus loin dans ce tutoriel, vous envoyez différents champs XDM en fonction du type de page sur laquelle se trouve le visiteur (par exemple, des SKU de produit sur les pages de produit). Pour ce faire, séquencez les règles contenant les **[!UICONTROL Mettre à jour la variable]** actions avant la règle qui utilise la variable **[!UICONTROL Envoyer un événement]** action.

Pour créer une règle de balise :

1. Ouvrez la propriété de balise que vous utilisez pour ce tutoriel.

1. Accédez à **[!UICONTROL Règles]** dans la navigation de gauche

1. Sélectionnez la variable **[!UICONTROL Créer une règle]** button

   ![Création d’une règle](assets/rules-create.png)

1. Donnez à la règle le nom `all pages global content variables - page bottom - AA (order 1)`.

1. Dans le **[!UICONTROL Événements]** , sélectionnez **[!UICONTROL Ajouter]**

   ![Attribuez un nom à la règle et ajoutez un événement](assets/rule-name-new.png)

1. Utilisez la variable **[!UICONTROL Extension Core]** et sélectionnez `Page Bottom` comme la propriété **[!UICONTROL Type d’événement]**

1. Sous , **[!UICONTROL Nom]** champ, nommez-le `Core - Page Bottom - order 1`. Vous pouvez ainsi décrire le déclencheur avec un nom significatif.

1. Sélectionner **[!UICONTROL Avancé]** menu déroulant et entrée `1` in **[!UICONTROL Commande]**

   >[!NOTE]
   >
   > Plus le nombre que vous saisissez est élevé, plus tard dans l’ordre global des opérations qu’il déclenche.

1. Sélectionner **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de la règle principale
   ![Sélectionner le déclenchement inférieur de la page](assets/create-tag-rule-trigger-bottom.png)

1. Dans le **[!UICONTROL Actions]** , sélectionnez **[!UICONTROL Ajouter]**

1. Comme la variable **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL SDK Web Adobe Experience Platform]**

1. Comme la variable **[!UICONTROL Type d’action]**, sélectionnez **[!UICONTROL Mettre à jour la variable]**

1. Comme la variable **[!UICONTROL Élément de données]**, sélectionnez la variable `xdm.variable.content` que vous avez créé dans la variable [Création d’éléments de données](create-data-elements.md) leçon

   ![Mettre à jour le schéma de variable](assets/create-rule-update-variable.png)

Mappez maintenant vos [!UICONTROL éléments de données] à la fonction [!UICONTROL schema] utilisé par votre objet XDM.

>[!NOTE]
> 
> Vous pouvez mapper des propriétés individuelles ou des objets entiers. Dans cet exemple, vous mappez des propriétés individuelles.


1. Faites défiler l’écran vers le bas jusqu’à ce que vous atteigniez le **`web`** objet

1. Sélectionner pour l’ouvrir

1. Mappez les éléments de données suivants aux `web` Variables XDM

   * **`web.webPageDetials.name`** vers `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** vers `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** vers `%page.pageInfo.hierarchie1%`

   ![Mettre à jour le contenu des variables](assets/create-rule-xdm-variable-content.png)

1. Recherchez ensuite le `identityMap` dans le schéma et sélectionnez-le.

1. Associer à la variable `identityMap.loginID` élément de données

   ![Mise à jour du mappage d’identité de variable](assets/create-rule-variable-identityMap.png)

1. Recherchez ensuite le champ eventType et sélectionnez-le.

1. Saisissez la valeur `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Cette liste déroulante renseigne la variable **`xdm.eventType`** dans l’objet XDM. Bien que vous puissiez également saisir des libellés de forme libre dans ce champ, il est vivement recommandé de **ne pas** car il a des effets négatifs avec Platform.

   >[!TIP]
   >
   > Pour comprendre les valeurs à renseigner dans la variable `eventType` , vous devez accéder à la page de schéma et sélectionner la variable `eventType` pour afficher les valeurs suggérées sur le rail de droite.

   ![Mise à jour du mappage d’identité de variable](assets/create-tag-rule-eventType.png)


1. Sélectionner **[!UICONTROL Conserver les modifications]** puis **[!UICONTROL Enregistrer]** la règle dans l’écran suivant pour terminer la création de la règle

### Envoyer un événement

Maintenant que vous avez défini les variables, vous pouvez créer la deuxième règle pour envoyer l’objet XDM à Platform Edge Network avec le **[!UICONTROL Envoyer un événement]** type d’action.

1. Sur la droite, sélectionnez pour **[!UICONTROL Ajouter une règle]** pour créer une autre règle

1. Donnez à la règle le nom `all pages send event - page bottom - AA (order 50)`.

1. Dans le **[!UICONTROL Événements]** , sélectionnez **[!UICONTROL Ajouter]**

1. Utilisez la variable **[!UICONTROL Extension Core]** et sélectionnez `Page Bottom` comme la propriété **[!UICONTROL Type d’événement]**

1. Sous , **[!UICONTROL Nom]** champ, nommez-le `Core - Page Bottom - order 50`. Vous pouvez ainsi décrire le déclencheur avec un nom significatif.

1. Sélectionner **[!UICONTROL Avancé]** menu déroulant et entrée `50` in **[!UICONTROL Commande]**. Cela garantit que la deuxième règle se déclenche après la première règle que vous définissez pour déclencher comme `1`.

1. Sélectionner **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de la règle principale
   ![Sélectionner le déclenchement inférieur de la page](assets/create-tag-rule-trigger-bottom-send.png)

1. Dans le **[!UICONTROL Actions]** , sélectionnez **[!UICONTROL Ajouter]**

1. Comme la variable **[!UICONTROL Extension]**, sélectionnez  **[!UICONTROL SDK Web Adobe Experience Platform]**

1. Comme la variable  **[!UICONTROL Type d’action]**, sélectionnez  **[!UICONTROL Envoyer un événement]**

1. Comme la variable **[!UICONTROL XDM]**, sélectionnez la variable `xdm.variable.content` élément de données créé dans la leçon précédente

1. Sélectionner **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de la règle principale

   ![Ajout de l’action Envoyer l’événement](assets/create-rule-send-event-action.png)
1. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer la règle

   ![Enregistrer la règle](assets/create-rule-save-rule.png)

## Publier la règle dans une bibliothèque

Ensuite, publiez la règle dans votre environnement de développement afin que vous puissiez vérifier qu’elle fonctionne.

Pour créer une bibliothèque :

1. Accédez à **[!UICONTROL Flux de publication]** dans la navigation de gauche

1. Sélectionner **[!UICONTROL Ajouter une bibliothèque]**

   ![Sélectionner Ajouter une bibliothèque](assets/rule-publish-library.png)
1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Web SDK Tutorial`
1. Pour le **[!UICONTROL Environnement]**, sélectionnez `Development`
1. Sélectionner  **[!UICONTROL Ajouter toutes les ressources modifiées]**

   >[!NOTE]
   >
   >    Outre l’extension du SDK Web de Adobe Experience Platform et la variable `all pages global content variables - page bottom - AA (order 50)` règle, vous voyez les composants de balise créés dans les leçons précédentes. L’extension Core contient le code JavaScript de base requis par toutes les propriétés de balise Web.

1. Sélectionner **[!UICONTROL Enregistrement et création pour le développement]**

   ![Création et création de la bibliothèque](assets/create-tag-rule-library-changes.png)

La création de la bibliothèque peut prendre quelques minutes. Une fois l’opération terminée, un point vert s’affiche à gauche du nom de la bibliothèque :

![Build complete](assets/create-rule-development-success.png)

Comme vous pouvez le voir sur la [!UICONTROL Flux de publication] le processus de publication, qui dépasse le cadre de ce tutoriel, contient beaucoup d’autres éléments. Ce tutoriel utilise une seule bibliothèque dans votre environnement de développement.

Vous êtes maintenant prêt à valider les données de la requête à l’aide de l’Adobe Experience Platform Debugger .

[Suivant ](validate-with-debugger.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
