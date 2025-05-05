---
title: Suivi des événements de conversion - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Adobe Journey Optimizer - Decisioning
description: Découvrez comment effectuer le suivi des événements de conversion Adobe Target à l’aide de l’extension Adobe Journey Optimizer - Decisioning Mobile
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Suivi des événements de conversion Target à l’aide de l’extension mobile Decisioning

L’objectif de la plupart des activités Target est de générer des actions utilisateur importantes dans votre application, telles que des achats, des inscriptions, des clics, etc. Les implémentations de Target utilisent généralement des événements de conversion personnalisés pour effectuer le suivi de ces actions, souvent avec des détails supplémentaires sur la conversion. Les événements de conversion pour Target peuvent être suivis à l’aide d’un SDK optimisé similaire à Target SDK. Des API spécifiques doivent être appelées pour effectuer le suivi des événements de conversion, comme illustré dans le tableau ci-dessous :

| Objectif de l’activité | Extension Target | Extension Decisioning |
|---|---|---|
| Suivi d’un événement de conversion d’affichage pour un emplacement de mbox (portée) | Appeler l’API [displayLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} lors de la consultation de l’emplacement de la mbox | Appelez l’API [display](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} lors de la visualisation de l’offre relative à l’emplacement de la mbox. Un événement avec le type d’événement decisioning.propositionDisplay est alors envoyé au réseau Experience Edge. **Cela est essentiel pour incrémenter les visiteurs dans vos activités Target et doit être effectué lors de la diffusion des offres Target standard et par défaut.** |
| Suivi d’un événement de conversion de clics pour un emplacement de mbox (portée) | Appelez l’API [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} dans lorsque l’utilisateur clique sur l’emplacement de la mbox | Appelez l’API [tapped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} lorsque l’utilisateur clique sur l’offre pour l’emplacement de mbox. Un événement avec le type d’événement decisioning.propositionInteract est alors envoyé au réseau Experience Edge. |
| Effectuez le suivi d’un événement de conversion personnalisé qui peut également inclure des données supplémentaires, telles que les paramètres du profil Target et les détails de la commande | Transmettez les données supplémentaires dans le champ TargetParameters fourni par les API [displayLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} et [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} | Utilisez les méthodes publiques [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} et [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} API disponibles dans l’offre pour que l’emplacement de la mbox génère les données au format XDM pour l’affichage et le clic, respectivement. Appelez ensuite l’API Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} pour envoyer ces données XDM de suivi, ainsi que toutes les données XDM et à structure libre supplémentaires, au réseau Experience Edge. |


Ensuite, découvrez comment [mettre à jour les audiences et les scripts de profil](update-audiences.md) pour garantir la compatibilité avec l’extension Decisioning.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
