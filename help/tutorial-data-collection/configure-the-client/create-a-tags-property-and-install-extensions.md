---
title: Création d’une propriété de balise Adobe Experience Platform et installation d’extensions
description: Création d’une propriété de balise Adobe Experience Platform et installation d’extensions
exl-id: d0fe82b5-a036-4e13-bae1-d1fee78d0084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Création d’un Adobe Experience Platform [!DNL Tags] propriétés et installation d’extensions

Maintenant que le code sur la page envoie des données et des événements dans la couche de données, il est temps pour le marketeur de lire les données de la couche de données et d’envoyer ces données à Adobe Experience Platform. Cela nécessite généralement deux bibliothèques JavaScript :

* Adobe de la couche de données client : Lors des étapes précédentes, vous avez créé un tableau de couche de données et y avez inséré des objets. Pour accéder à ces données, vous devez charger la bibliothèque JavaScript de la couche de données client Adobe. Cette bibliothèque fournit des notifications pour les événements et les modifications de couche de données, ainsi qu’un accès simple aux données.
* SDK Web Adobe Experience Platform : Cette bibliothèque JavaScript communique avec le [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Le SDK traite l’identité, le consentement, la collecte de données, la personnalisation, les audiences, etc.

Bien que vous puissiez charger ces bibliothèques individuelles sur votre site web et les utiliser directement, nous vous recommandons d’utiliser [Balises Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr). Avec les balises, vous pouvez incorporer un seul script dans votre HTML et utiliser l’interface utilisateur Balises pour déployer la couche de données client Adobe et le SDK Web Adobe Experience Platform. Les balises vous permettent également de créer des règles d’envoi de données, entre autres. Ce tutoriel utilise les balises à cet effet et suppose que vous connaissez de base le fonctionnement des balises.

## Création d’une propriété dans les balises

1. [Création d’une propriété dans les balises](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Installation de l’extension Adobe Client Data Layer

Installez l’extension Adobe Client Data Layer :

1. Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche de la propriété Tag que vous utilisez pour ce tutoriel.
1. Sélectionnez la **[!UICONTROL Catalogue]** Cliquez sur le lien supérieur, puis recherchez &quot;couche de données&quot;.
1. Une fois que la couche de données client Adobe s’affiche dans les résultats, cliquez sur le **[!UICONTROL Installer]** bouton . Un écran de configuration devrait s’afficher. Pour ce tutoriel, il n’est pas nécessaire de modifier les valeurs par défaut.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
   ![Installation de l’extension Adobe Client Data Layer](../assets/acdl-extension-installation.png)


## Installer l’extension Adobe Experience Platform Web SDK

Installez ensuite l’extension SDK Web Adobe Experience Platform :

1. Recherchez l’extension dans le catalogue d’extensions, puis cliquez sur les **[!UICONTROL Installer]** bouton . L’écran de configuration devrait s’afficher :
   ![Installation de l’extension SDK Web Adobe Experience Platform](../assets/web-sdk-extension-installation.png)
1. Dans le [!UICONTROL Datastream] , sélectionnez le flux de données que vous avez créé précédemment. Les mêmes environnements de flux de données que ceux que vous avez vus dans [Création d’un flux de données](../configure-the-server/create-a-datastream.md).
   ![Sélection des flux de données](../assets/web-sdk-datastream-selection.png)
1. Plus loin dans l’écran de configuration, recherchez et désélectionnez **[!UICONTROL Activer la collecte de données de clic]**. Par défaut, le SDK effectue automatiquement le suivi des liens pour vous. Toutefois, dans ce tutoriel, nous vous montrons comment effectuer le suivi de vos propres clics sur les liens à l’aide d’informations de lien personnalisées.
1. Cliquez sur le bouton **[!UICONTROL Enregistrer]** pour terminer l’installation de l’extension SDK Web Adobe Experience Platform.

>[!TIP]
>
>Les environnements de jeux de données ont une relation avec les environnements de balises. Supposons que vous ayez terminé l’installation de l’extension du SDK Web de Adobe Experience Platform, que vous créiez une bibliothèque de balises contenant l’extension, puis que vous publiiez la bibliothèque dans un environnement de développement de balises. Lorsque la bibliothèque de balises est chargée sur votre page web et que l’extension Adobe Experience Platform Web SDK envoie une requête à Edge Network, l’extension inclut la variable [!UICONTROL Environnement de développement] ID d’environnement de la banque de données. Edge Network, à son tour, utilise cet identifiant pour lire la configuration de la variable [!UICONTROL Environnement de développement] environnement de flux de données et transférez les données vers les produits d’Adobe appropriés.
>
>Actuellement, vous n’avez qu’un environnement de flux de données de développement, un environnement de flux de données intermédiaire et un environnement de flux de données de production. Il est possible de créer plusieurs environnements de développement de flux de données (un pour vous et un pour votre collègue, peut-être) à l’aide de l’interface utilisateur de flux de données. Si vous disposez de plusieurs environnements de flux de données de développement, vous pouvez sélectionner celui que vous souhaitez utiliser pour cette propriété de balise.


Les extensions appropriées ont été installées. Il est temps de créer des règles et des éléments de données.

[Suivant : ](create-rules-for-tracking-page-view-and-commerce-events.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
