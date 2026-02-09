---
title: Configuration d’un espace de noms d’identité
description: Découvrez comment configurer des espaces de noms d’identité à utiliser avec Adobe Experience Platform Web SDK. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 12%

---

# Configuration d’un espace de noms d’identité

Découvrez comment configurer les espaces de noms d’identité à utiliser avec le SDK web d’Adobe Experience Platform.

Le [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/fr/docs/id-service/using/home) définit un identifiant visiteur commun (ECID) entre les applications Adobe basées sur SDK afin d’alimenter les fonctionnalités d’Experience Cloud telles que le partage d’audience entre les applications. Vous pouvez également envoyer vos propres ID de client au Service pour activer le ciblage inter-appareils et les intégrations à d’autres systèmes, tels que votre système de gestion de la relation client (CRM).

Le service d’identités [Adobe Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/home) (oui, il y en a deux !) utilise les ECID et les ID client pour générer des graphiques d’identités, ce qui vous permet de fusionner des attributs et des comportements dans des profils client en temps réel.

>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

>[!NOTE]
>
>Un espace de noms d’identité personnalisé est _non requis_ pour implémenter Adobe Analytics, Adobe Target ou Adobe Audience Manager avec Web SDK (les identités authentifiées peuvent être transmises dans l’objet `data` au lieu de l’objet `xdm`, comme vous le verrez plus loin). Les espaces de noms d’identité sont requis pour les applications natives de Platform telles que Journey Optimizer, Real-Time Customer Data Platform et Customer Journey Analytics. Bien que vous puissiez décider de ne pas utiliser d’espace de noms d’identité dans votre propre mise en œuvre, vous devez le faire dans le cadre de ce tutoriel.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon vous permettent de capturer les détails d’identité d’un client fictif connecté au [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) à l’aide des informations d’identification, **utilisateur : `test@test.com`/mot de passe : test**.

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Compréhension des espaces de noms d’identité
* Création d’un espace de noms d’identité personnalisé pour capturer un identifiant CRM interne


## Conditions préalables

Vous devez avoir déjà terminé les leçons précédentes :

* [Configuration des schémas](configure-schemas.md)

>[!IMPORTANT]
>
>L’extension [Experience Cloud ID](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) n’est pas nécessaire lors de l’implémentation de Adobe Experience Platform Web SDK, car la bibliothèque Web SDK JavaScript contient la fonctionnalité du service d’identification des visiteurs.
>
> Si votre site web utilise déjà le service Experience Cloud ID sur votre site web, par le biais de l’API visiteur ou de l’extension de balise du service Experience Cloud ID, et que vous souhaitez continuer à l’utiliser lors de la migration vers Adobe Experience Platform Web SDK, vous devez utiliser la dernière version de l’API visiteur ou l’extension de balise du service Experience Cloud ID. Pour plus d’informations, consultez [&#x200B; Migration des ID &#x200B;](https://experienceleague.adobe.com/fr/docs/experience-platform/edge/identity/overview) .

## Création d’un espace de noms d’identité

Dans cet exercice, vous allez créer un espace de noms d’identité pour le champ d’identité personnalisé de Luma, `lumaCrmId`. Les espaces de noms d’identité jouent un rôle essentiel dans la création de profils clients en temps réel, car deux valeurs correspondantes dans le même espace de noms permettent à deux sources de données de former un graphique d’identité.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur l’identité dans Adobe Experience Platform :

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on&enablevpops)

Créez maintenant un espace de noms pour l’identifiant CRM de Luma :

1. Ouvrez l’interface [Collecte de données](https://experience.adobe.com/data-collection/){target="_blank"}
1. Sélectionnez le sandbox que vous utilisez pour le tutoriel

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un sandbox de développement pour ce tutoriel. Si ce n’est pas le cas, utilisez le sandbox **[!UICONTROL Prod]**.

1. Sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche
1. Sélectionnez **[!UICONTROL Parcourir]**

   Une liste d’espaces de noms d’identité s’affiche dans l’interface principale de la page. Elle indique leurs noms, symboles d’identité, date de la dernière mise à jour et s’il s’agit d’espaces de noms standard ou personnalisés. Le rail de droite contient des informations sur [!UICONTROL &#x200B; l’intensité du graphique d’identités &#x200B;].

1. Sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**

   ![Affichage des identités](assets/configure-identities-screen.png)

1. Fournissez les détails comme suit et sélectionnez **[!UICONTROL Créer]**.

   | Champ | Valeur |
   |---------------|-----------|
   | Nom d’affichage | Identifiant CRM de Luma |
   | Symbole d’identité | lumaCrmId |
   | Type | Identifiant individuel sur l&#39;ensemble des appareils |


   ![Création d’espaces de noms.](assets/identities-create-namespace.png)


   L’espace de noms d’identité est renseigné dans l’écran **[!UICONTROL Identités]**.

   ![Création d’espaces de noms.](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> Dans la leçon [Création d’identités](create-identities.md), vous apprendrez à utiliser cet espace de noms lors de l’envoi d’identités à Platform Edge Network.

Maintenant que les identités sont en place, le flux de données peut être configuré.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
