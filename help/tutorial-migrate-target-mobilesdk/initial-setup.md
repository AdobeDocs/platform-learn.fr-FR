---
title: 'Configuration initiale : migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Offer Decisioning et Target.'
description: Découvrez et configurez les éléments fondamentaux importants requis pour l’implémentation de Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 6%

---

# Configurer la collecte de données initiale

La migration de Target SDK vers Optimize SDK nécessite une configuration initiale pour permettre la capture de données, les fonctionnalités et les fonctions appropriées d’Optimize SDK. Les étapes suivantes doivent être effectuées avant toute modification de l’implémentation des applications mobiles :

- [Configurez les autorisations appropriées](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} dans Adobe Admin Console pour la collecte de données
- [Configurer un schéma XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} pour transmettre des données structurées à Edge Network
- [Configurer le schéma](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} pour recevoir les données Adobe Target
- [Configurer un espace de noms d’identité](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} pour la personnalisation inter-appareils et la fonctionnalité mbox3rdPartyId
- [Création d’un flux de données](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} pour activer le transfert des données d’Edge Network
- [Configurer le flux de données](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} pour activer le transfert des données vers Adobe Target
- [Configurer la propriété de balise](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} pour Offer Decisioning et l’extension Target

## Configuration d’extension

>[!BEGINTABS]

>[!TAB Extension Offer Decisioning and Target]

Extensions de balise installées lors de l’utilisation de l’extension Offer Decisioning et Target :

1. Offer Decisioning et Target
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Profile
1. Consentement
1. Identité
1. AEP Assurance (facultatif, nécessaire pour le débogage)

![ Extensions de balise installées lors de l’utilisation de l’extension Offer Decisioning et Target ](assets/tag-extensions-decisioning.png)

>[!TAB Extension cible]

Extensions de balise installées lors de l’utilisation de l’extension Target :

1. Adobe Target
1. Mobile Core
1. Profile
1. Adobe Analytics (facultatif, nécessaire si vous utilisez Adobe Analytics en tant que source de création de rapports pour les activités Adobe Target)

![ Extensions de balise installées lors de l’utilisation de l’extension Target ](assets/tag-extensions-target.png)

>[!ENDTABS]

## Configuration du flux de données

L’extension cible comporte des [ paramètres configurables ](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) qui, avec l’extension de décision, sont [ configurés dans le flux de données](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup).

| Extension Target | Extension Offer Decisioning and Target | Notes |
| --- | --- | --- | 
| Code client | S.O. | Défini automatiquement par Edge à l’aide des détails de l’organisation IMS |
| Identifiant de l’environnement | Identifiant de l’environnement Target | Configuré dans le flux de données |
| Propriété Workspace de Target | Jeton de propriété | Configuré dans le flux de données |
| Temporisation | Temporisation | Configurable dans l’extension Offer Decisioning and Target et dans le SDK d’optimisation. Le délai d’expiration par défaut est de 10 secondes. |
| Server Domain (Domaine du serveur) | domaine Edge Network | Défini dans l’extension Adobe Experience Platform Edge Network |

Découvrez ensuite comment [remplacer le SDK Target](replace-sdk.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target vers l’extension Offer Decisioning et Target. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
