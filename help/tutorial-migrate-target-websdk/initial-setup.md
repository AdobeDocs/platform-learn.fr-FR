---
title: Configuration initiale | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez et configurez les éléments fondamentaux importants requis pour l’implémentation de votre SDK Web Platform.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# Exécution de la configuration initiale de la collecte de données

La migration d’at.js vers le SDK Web Platform nécessite une configuration initiale pour permettre la capture de données, les fonctionnalités et les fonctions appropriées du SDK Web Platform. Les étapes suivantes de la [Tutoriel de mise en oeuvre du SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) doit être renseigné avant que toute modification de mise en oeuvre du site web ne soit effectuée :

- [Configurer les autorisations appropriées](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"} dans Adobe Admin Console pour la collecte de données
- [Configuration d’un schéma XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} pour transmettre des données structurées au réseau Edge
- [Configuration d’un espace de noms d’identité](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} pour la personnalisation sur plusieurs appareils et la fonctionnalité mbox3rdPartyId
- [Création d’un flux de données](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} pour activer le transfert de données à partir d’Edge Network
- [Configuration du flux de données](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} pour activer le transfert de données vers Adobe Target

>[!CAUTION]
>
>N’oubliez pas que ces aspects de conception doivent être coordonnés entre Target, Analytics et les migrations d’Audience Manager.

Une fois la configuration initiale terminée, la fonctionnalité Target doit être activée à l’aide du réseau Adobe Experience Platform Edge.

Ensuite, apprenez à [remplacez la bibliothèque at.js et configurez une mise en oeuvre de base du SDK Web Platform](replace-library.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
