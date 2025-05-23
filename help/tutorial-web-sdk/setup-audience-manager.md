---
title: Configuration de l’Audience Manager avec le SDK Web Platform
description: Découvrez comment configurer Adobe Audience Manager à l’aide du SDK Web Platform et valider l’implémentation à l’aide d’une destination de cookie. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
solution: Data Collection, Audience Manager
jira: KT-15409
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 4%

---

# Configuration de l’Audience Manager avec le SDK Web Platform

Découvrez comment configurer Adobe Audience Manager à l’aide du SDK web Adobe Experience Platform et valider l’implémentation à l’aide d’une destination de cookie.

[Adobe Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager) est la solution Adobe Experience Cloud qui fournit tout ce qui est nécessaire pour collecter des informations commercialement pertinentes sur les visiteurs du site, créer des segments commercialisables et diffuser de la publicité et du contenu ciblés à la bonne audience.

![ Diagramme SDK Web et Adobe Audience Manager ](assets/dc-websdk-aam.png)

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Configuration d’un flux de données pour activer l’Audience Manager
* Activation d’une destination de cookie dans Audience Manager
* Validation de la mise en oeuvre de l’Audience Manager en confirmant la qualification de l’audience avec Adobe Experience Platform Debugger

## Conditions préalables

Pour terminer cette leçon, vous devez d’abord :

* Suivez les leçons des sections Configuration initiale et Configuration des balises de ce tutoriel.
* Avoir accès à Adobe Audience Manager et aux autorisations appropriées pour créer, lire et écrire des caractéristiques, des segments et des destinations. Pour plus d’informations, consultez le [contrôle d’accès en fonction du rôle de l’Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).

## Configuration du flux de données

L’implémentation de l’Audience Manager à l’aide du SDK Web de Platform diffère de l’implémentation à l’aide du [transfert côté serveur (SSF)](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/server-side-forwarding/ssf). Le transfert côté serveur transmet les données de demande Adobe Analytics à l’Audience Manager. Une implémentation du SDK Web Platform transmet les données XDM envoyées à l’Edge Network Platform à Audience Manager. L’Audience Manager est activée dans le flux de données :

1. Accédez à l’interface [Collecte de données](https://experience.adobe.com/#/data-collection){target="blank"}
1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Datastreams]**
1. Sélectionnez le flux de données `Luma Web SDK: Development Environment` créé précédemment.

   ![Sélectionnez la banque de données du SDK Web Luma](assets/datastream-luma-web-sdk-development.png)

1. Sélectionnez **[!UICONTROL Ajouter un service]**
   ![Ajouter un service à la banque de données](assets/aam-datastream-addService.png)
1. Sélectionnez **[!UICONTROL Adobe Audience Manager]** comme **[!UICONTROL Service]**
1. Confirmez que les **[!UICONTROL destinations de cookie activées]** et **[!UICONTROL destinations d’URL activées]** sont sélectionnées
1. Sélectionnez **[!UICONTROL Save]**
   ![Confirmez les paramètres du flux de données d’Audience Manager et enregistrez](assets/aam-datastream-save.png)

## Création d’une source de données

Créez ensuite un [Source de données](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings), un outil fondamental pour organiser les données dans l’Audience Manager :

1. Accédez à l&#39;interface [Audience Manager](https://experience.adobe.com/#/audience-manager/)
1. Sélectionnez **[!UICONTROL Données d’audience]** dans la barre de navigation supérieure.
1. Sélectionnez les **[!UICONTROL sources de données]** dans le menu déroulant.
1. Sélectionnez le bouton **[!UICONTROL Ajouter nouveau]** dans la partie supérieure de la page Sources de données.

   ![Sources de données d’Audience Manager Adobe Experience Platform](assets/data-sources-list.jpg)

1. Attribuez un nom et une description conviviaux à Data Source. Pour la configuration initiale, vous pouvez nommer cet `Platform Web SDK tutorial`.
1. Définissez **[!UICONTROL Type d’ID]** sur **[!UICONTROL Cookie]**
1. Dans la section **[!UICONTROL Contrôles des exportations de données]**, sélectionnez **[!UICONTROL Aucune restriction]**

   ![Configuration de Source de données d’Audience Manager Adobe Experience Platform](assets/data-source-details.png)

1. **[!UICONTROL Enregistrer]** le Source de données


## Création d’une caractéristique

Une fois le Source de données enregistré, configurez une [caractéristique](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/features/traits/traits-overview). Les caractéristiques sont une combinaison d’un ou de plusieurs signaux en Audience Manager. Créez une caractéristique pour les visiteurs de la page d’accueil.

>[!NOTE]
>
>Toutes les données XDM sont envoyées à l’Audience Manager si elles sont activées dans le flux de données. Toutefois, les données peuvent prendre 24 heures jusqu’à ce qu’elles soient disponibles dans le rapport Signaux non utilisés. Créez des caractéristiques explicites pour les données XDM que vous souhaitez utiliser immédiatement en Audience Manager, comme décrit dans cet exercice.

1. Sélectionnez **[!UICONTROL Données d’audience]** > **[!UICONTROL Caractéristiques]**
1. Sélectionnez la caractéristique **[!UICONTROL Add New]** > **[!UICONTROL Rule-Based]**

   ![Caractéristique basée sur des règles d’Audience Manager Adobe Experience Platform](assets/rule-based-trait.jpg)

1. Donnez un nom et une description conviviaux à votre caractéristique, `Luma homepage view`
1. Sélectionnez le **[!UICONTROL Source de données]** que vous avez créé dans la section précédente.
1. **[!UICONTROL Sélectionnez un dossier]** dans lequel enregistrer votre caractéristique dans le volet de droite. Vous pouvez créer un dossier en **sélectionnant l’icône +** en regard d’un dossier parent existant. Vous pouvez nommer ce nouveau dossier `Platform Web SDK tutorial`.
1. Développez le signe d’insertion **[!UICONTROL Expression de caractéristique]** et sélectionnez **[!UICONTROL Générateur d’expression]**. Vous devez fournir une paire de valeurs de clé qui correspond à une visite de page d’accueil.
1. Ouvrez la [page d’accueil Luma](https://luma.enablementadobe.com/content/luma/us/en.html) (mappée à la propriété de balise) et l’ **Adobe Experience Platform Debugger** et actualisez la page.
1. Consultez les requêtes réseau et les détails de l’événement pour le SDK Web Platform afin de trouver la clé et la valeur de nom de la page d’accueil.
   ![Adobe Experience Platform Audience Manager XDM Data](assets/xdm-keyvalue.jpg)
1. Revenez au Générateur d’expression dans l’interface utilisateur d’Audience Manager et saisissez la clé **`web.webPageDetails.name`** et la valeur **`content:luma:us:en`**. Cette étape vous permet de déclencher une caractéristique chaque fois que vous chargez la page d’accueil.
1. **[!UICONTROL Enregistrez]** la caractéristique.


## Création d’un segment

Les étapes suivantes consistent à créer un **segment** et à affecter votre caractéristique nouvellement définie à ce segment.

1. Sélectionnez **[!UICONTROL Données d’audience]** dans le volet de navigation supérieur et sélectionnez **[!UICONTROL Segments]**
1. Sélectionnez **[!UICONTROL Ajouter nouveau]** dans le coin supérieur gauche de la page pour ouvrir le créateur de segments.
1. Attribuez à votre segment un nom et une description conviviaux, tels que `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Sélectionnez un dossier]** où votre segment est enregistré dans le volet de droite. Vous pouvez créer un dossier en **sélectionnant l’icône +** en regard d’un dossier parent existant. Vous pouvez nommer ce nouveau dossier `Platform Web SDK tutorial`.
1. Ajoutez un code d’intégration, qui dans ce cas est un jeu aléatoire de nombres.
1. Dans la section **[!UICONTROL Source de données]**, sélectionnez **[!UICONTROL Audience Manager]** et la source de données que vous avez créée précédemment
1. Développez la section **[!UICONTROL Caractéristiques]** et recherchez la caractéristique que vous avez créée.
1. Sélectionnez **[!UICONTROL Ajouter une caractéristique]**.
1. Sélectionnez **[!UICONTROL Enregistrer]** au bas de la page.

   ![Adobe Experience Platform Audience Manager Add Trait](assets/add-trait-segment.jpg)

   ![Adobe Experience Platform Audience Manager Add Trait](assets/saved-segment.jpg)

## Créer une destination

Créez ensuite une **destination basée sur un cookie** à l’aide du **créateur de destinations**. Le créateur de destinations vous permet de créer et de gérer des destinations de cookie, d’URL et de serveur à serveur.

1. Ouvrez le créateur de destinations en sélectionnant **[!UICONTROL Destinations]** dans le menu **Données d’audience** dans la barre de navigation supérieure.
1. Sélectionnez **[!UICONTROL Créer une destination]**
1. Saisissez un nom et une description, `Platform Web SDK tutorial`
1. En tant que **[!UICONTROL Catégorie]**, sélectionnez **[!UICONTROL Personnalisé]**
1. Comme **[!UICONTROL Type]**, sélectionnez **[!UICONTROL Cookie]**

   ![Adobe Experience Platform Audience Manager Add Trait](assets/destination-settings.jpg)

1. Ouvrez la section **[!UICONTROL Configuration]** pour saisir les détails sur votre destination de cookie.
1. Attribuez un nom convivial à votre cookie, `platform_web_sdk_tutorial`
1. En tant que **[!UICONTROL domaine du cookie]**, ajoutez le domaine du site sur lequel vous envisagez d’intégrer, pour le tutoriel, saisissez le domaine Luma `luma.enablementadobe.com`.
1. En tant qu&#39;option **[!UICONTROL Publish data to]** , sélectionnez **[!UICONTROL Uniquement les domaines sélectionnés]**
1. Sélectionnez votre domaine s’il n’a pas déjà été ajouté
1. En tant que **[!UICONTROL format de données]**, sélectionnez **[!UICONTROL clé unique]** et attribuez une clé à votre cookie. Pour ce tutoriel, utilisez `segment` comme valeur de clé.
1. Enfin, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer les détails de configuration de destination.

   ![Section de configuration de la destination de l’Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. Dans la section **[!UICONTROL Mappages de segments]**, utilisez la fonction **[!UICONTROL Rechercher et ajouter des segments]** pour rechercher les `Platform Web SDK - Homepage visitors` que vous avez créés précédemment et sélectionnez **[!UICONTROL Ajouter]**.


1. Une fois que vous avez ajouté votre segment, une fenêtre contextuelle s’ouvre dans laquelle vous devez fournir une valeur attendue pour votre cookie. Pour cet exercice, saisissez la valeur &quot;hpvisitor&quot;.

1. Sélectionnez **[!UICONTROL Save]**

1. Sélectionnez **[!UICONTROL Done]**
   ![Adobe Experience Platform Audience Manager Add Trait](assets/luma-cookie-segment-dw.png)

La période de mappage des segments nécessite quelques heures pour être activée. Une fois l’opération terminée, vous pouvez actualiser l’interface d’Audience Manager et voir la liste **Segments mappés** mise à jour.

## Validation du segment

Quelques heures après la création initiale du segment, vous pouvez vérifier qu’il fonctionne correctement.

Tout d’abord, vérifiez que vous pouvez être admissible pour le segment.

1. Ouvrez la [page d’accueil du site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) avec celle-ci mappée à la propriété de balise pour que le segment que vous venez de créer soit admissible.
1. Ouvrez l’onglet **Outils de développement** > **Réseau** de votre navigateur
1. Filtrer sur la requête SDK Web Platform en utilisant `interact` comme filtre de texte
1. Sélectionnez un appel et ouvrez l’onglet **Aperçu** pour afficher les détails de la réponse.
1. Développez la **payload** pour afficher les détails de cookie attendus, tels que précédemment configurés dans Audience Manager. Dans cet exemple, le nom de cookie attendu est `platform_web_sdk_tutorial`.

   ![Adobe Experience Platform Audience Manager Add Trait](assets/segment-validate-response.jpg)

1. Ouvrez l’onglet **Application** et ouvrez **Cookies** dans le menu **Stockage**.
1. Sélectionnez le domaine **`https://luma.enablementadobe.com`** et vérifiez que votre cookie est correctement écrit dans la liste.

   ![Adobe Experience Platform Audience Manager Add Trait](assets/validate-cookie.jpg)


Enfin, vous devez ouvrir le segment dans l’interface d’Audience Manager et vous assurer que les **populations de segments** ont été incrémentées :

![Adobe Experience Platform Audience Manager Add Trait](assets/segment-population.jpg)


Maintenant que vous avez terminé cette leçon, vous devriez être en mesure de voir comment le SDK Web Platform transmet les données à l’Audience Manager et peut définir un cookie propriétaire spécifique au segment avec une destination de cookie.

[Suivant : ](setup-target.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
