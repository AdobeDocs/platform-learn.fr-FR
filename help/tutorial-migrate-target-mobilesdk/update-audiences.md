---
title: Mise à jour des audiences et des scripts de profil - Migration de Target d’at.js 2.x vers le SDK Web
description: Découvrez comment mettre à jour les audiences Adobe Target et les scripts de profil pour des raisons de compatibilité avec le SDK Web Experience Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Mise à jour des audiences Target et des scripts de profil pour la compatibilité du SDK Web Platform


## Ajustement des audiences


Pour plus d’informations et de bonnes pratiques, consultez la documentation dédiée sur les [scripts de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Mise à jour des jetons de paramètre pour le contenu dynamique



Si vous choisissez d’effectuer des ajustements après la migration afin de prendre en compte les nouveaux noms de paramètres de mbox XDM, veillez à suspendre toute activité impactée pendant l’événement de migration afin d’empêcher l’affichage des erreurs d’activité aux visiteurs.

Ensuite, découvrez comment [valider l’implémentation de Target](validate.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension Optimize. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
