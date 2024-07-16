---
title: Configuration d’un espace de noms d’identité
description: Découvrez comment configurer les espaces de noms d’identité à utiliser avec le SDK Web de Adobe Experience Platform. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 1a4f2e3813a6db4bef77753525c8a7d40692a4b2
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 12%

---

# Configuration d’un espace de noms d’identité

Découvrez comment configurer les espaces de noms d’identité à utiliser avec le SDK web d’Adobe Experience Platform.

Le [service Adobe Experience Cloud Identity](https://experienceleague.adobe.com/fr/docs/id-service/using/home) définit un identifiant visiteur commun (l’ECID) sur l’ensemble des applications d’Adobe basées sur le SDK afin d’alimenter les fonctionnalités Experience Cloud telles que le partage d’audiences entre applications. Vous pouvez également envoyer vos propres ID de client au service pour permettre le ciblage entre appareils et les intégrations avec d’autres systèmes, tels que votre système de gestion de la relation client (CRM).

Le [service Adobe Experience Platform Identity](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) (oui, il y en a deux !) utilise les ECID et les ID de client pour générer des graphiques d’identité, ce qui vous permet de fusionner des attributs et des comportements dans des profils client en temps réel.

>[!NOTE]
>
>Un espace de noms d’identité personnalisé est _non requis_ pour implémenter Adobe Analytics, Adobe Target ou Adobe Audience Manager avec SDK Web (les identités authentifiées peuvent être transmises dans l’objet `data` au lieu de l’objet `xdm` comme vous le verrez plus loin). Les espaces de noms d’identité sont requis pour les applications natives à Platform telles que Journey Optimizer, Real-Time Customer Data Platform, Customer Journey Analytics. Bien que vous puissiez décider de ne pas utiliser un espace de noms d’identité dans votre propre mise en oeuvre, vous devez le faire dans le cadre de ce tutoriel.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon vous permettent de capturer les détails d’identité d’un client fictif connecté au [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) à l’aide des informations d’identification, **utilisateur : `test@adobe.com` / mot de passe : test**.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Présentation des espaces de noms d’identité
* Création d’un espace de noms d’identité personnalisé pour capturer un identifiant CRM interne


## Conditions préalables

Vous devez avoir terminé les leçons précédentes :

* [Configuration des schémas](configure-schemas.md)

>[!IMPORTANT]
>
>L’ [’ extension d’ID Experience Cloud](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) n’est pas nécessaire lors de l’implémentation du SDK Web Adobe Experience Platform, car la bibliothèque JavaScript du SDK Web contient la fonctionnalité du service d’identification des visiteurs.
>
> Si votre site web utilise déjà le service d’ID Experience Cloud sur votre site web (via l’API visiteur ou l’extension de balise du service d’ID Experience Cloud) et que vous souhaitez continuer à l’utiliser lors de la migration vers le SDK Web Adobe Experience Platform, vous devez utiliser la dernière version de l’API visiteur ou de l’extension de balise du service d’ID Experience Cloud. Voir [Migration des identifiants](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview) pour plus d’informations.

## Création d’un espace de noms d’identité

Dans cet exercice, vous créez un espace de noms d’identité pour le champ d’identité personnalisé de Luma, `lumaCrmId`. Les espaces de noms d’identité jouent un rôle essentiel dans la création de profils clients en temps réel, car deux valeurs correspondantes dans le même espace de noms permettent à deux sources de données de former un graphique d’identité.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur l’identité dans Adobe Experience Platform :

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Maintenant, créez un espace de noms pour l’ID de gestion de la relation client Luma :

1. Ouvrez l’ [ interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Sélectionnez l’environnement de test que vous utilisez pour le tutoriel

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un environnement de test de développement pour ce tutoriel. Si ce n&#39;est pas le cas, utilisez l&#39;environnement de test **[!UICONTROL Prod]**.

1. Sélectionnez **[!UICONTROL Identités]** dans la navigation de gauche.
1. Sélectionnez **[!UICONTROL Parcourir]**

   Une liste d’espaces de noms d’identité s’affiche dans l’interface principale de la page, indiquant leurs noms, symboles d’identité, la date de la dernière mise à jour et s’ils sont des espaces de noms standard ou personnalisés. Le rail de droite contient des informations sur la [!UICONTROL force du graphique d’identités].

1. Sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**

   ![Afficher les identités](assets/configure-identities-screen.png)

1. Indiquez les détails comme suit et sélectionnez **[!UICONTROL Créer]**.

   | Champ | Valeur |
   |---------------|-----------|
   | Nom d’affichage | Identifiant Luma CRM |
   | Symbole d’identité | lumaCrmId |
   | Type | Identifiant individuel sur l&#39;ensemble des appareils |


   ![Création d’espaces de noms.](assets/identities-create-namespace.png)


   L’espace de noms Identity est renseigné dans l’écran **[!UICONTROL Identités]** .

   ![Création d’espaces de noms.](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> Dans la leçon [Créer des identités](create-identities.md), vous apprendrez à utiliser cet espace de noms lors de l’envoi d’identités à l’Edge Network Platform.

Maintenant que les identités sont en place, le flux de données peut être configuré.

[Suivant : ](configure-datastream.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
