---
title: 'Configuration initiale : migration de Target d’at.js 2.x vers le SDK Web'
description: Découvrez et configurez les éléments fondamentaux importants requis pour l’implémentation de votre SDK Web Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Exécution de la configuration initiale de la collecte de données

La migration d’at.js vers le SDK Web Platform nécessite une configuration initiale pour permettre la capture de données, les fonctionnalités et les fonctions appropriées du SDK Web Platform. Les étapes suivantes du [tutoriel de mise en oeuvre du SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) doivent être effectuées avant toute modification de mise en oeuvre de site Web :

- [Configurez les autorisations appropriées](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} dans Adobe Admin Console pour la collecte de données
- [Configuration d’un schéma XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} pour transmettre des données structurées à l’Edge Network
- [Configuration d’un espace de noms d’identité](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} pour la personnalisation sur plusieurs appareils et la fonctionnalité mbox3rdPartyId
- [Créez un flux de données](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} pour activer le transfert de données à partir d’un Edge Network.
- [Configurez la banque de données](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} pour activer le transfert de données vers Adobe Target

>[!CAUTION]
>
>N’oubliez pas que ces aspects de conception doivent être coordonnés entre Target, Analytics et les migrations d’Audience Manager.

Une fois la configuration initiale terminée, la fonctionnalité Target doit être activée à l’aide de l’Edge Network Adobe Experience Platform.

Ensuite, découvrez comment [remplacer la bibliothèque at.js et configurer une implémentation de base du SDK Web Platform](replace-library.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension Optimize. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
