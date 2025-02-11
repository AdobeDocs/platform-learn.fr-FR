---
title: Configuration initiale - Migration d’Adobe Target vers Adobe Journey Optimizer - Extension mobile Decisioning
description: Découvrez et configurez les éléments fondamentaux importants requis pour l’implémentation de Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: a928fb5c8e48e71984b75faf4eb397814caac6aa
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 5%

---

# Configurer la collecte de données initiale

La migration de Target SDK vers Optimize SDK nécessite une configuration initiale pour permettre la capture de données, les fonctionnalités et les fonctions appropriées d’Optimize SDK. Les étapes suivantes doivent être effectuées avant toute modification de l’implémentation du site web :

- [Configurez les autorisations appropriées](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} dans Adobe Admin Console pour la collecte de données
- [Configurer un schéma XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} pour transmettre des données structurées à Edge Network
- [Configurer le schéma](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} pour recevoir les données Adobe Target
- [Configurer un espace de noms d’identité](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} pour la personnalisation inter-appareils et la fonctionnalité mbox3rdPartyId
- [Création d’un flux de données](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} pour activer le transfert des données d’Edge Network
- [Configurer le flux de données](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} pour activer le transfert des données vers Adobe Target
- [Configurer la propriété de balise](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} pour l’extension Decisioning

>[!BEGINTABS]

>[!TAB Extension Decisioning]

Extensions de balise installées lors de l’utilisation de l’extension Decisioning :

1. Adobe Journey Optimizer - Prise de décision
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Profile
1. Consentement
1. Identité
1. AEP Assurance (facultatif, nécessaire pour le débogage)

![ Extensions de balise installées lors de l’utilisation de l’extension Decisioning ](assets/tag-extensions-decisioning.png)

>[!TAB Extension cible]

Extensions de balise installées lors de l’utilisation de l’extension Target :

1. Adobe Target
1. Mobile Core
1. Profile
1. Adobe Analytics (facultatif, nécessaire si vous utilisez Adobe Analytics en tant que source de création de rapports pour les activités Adobe Target)

![ Extensions de balise installées lors de l’utilisation de l’extension Target ](assets/tag-extensions-target.png)

>[!ENDTABS]

Découvrez ensuite comment [remplacer le SDK Target](replace-library.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
