---
title: Valider et résoudre les problèmes liés à l’implémentation de l’extension Decisioning
description: Découvrez comment valider et résoudre les problèmes liés à une implémentation mobile d’Adobe Target à l’aide de l’extension Decisioning.
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: a4fe85580776e5d84f6deaf3c0224f0513ba8415
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Valider et résoudre les problèmes liés à l’implémentation de l’extension Decisioning

Après avoir migré votre implémentation Target de l’extension Target vers l’extension Decisioning, il est important de vérifier que tout fonctionne correctement avant de publier les modifications apportées à votre application de production. Adobe recommande ce qui suit, qui est abordé en détail sur cette page :

* Effectuez une validation technique pour vous assurer que l’implémentation de base et les requêtes et réponses de Platform Mobile SDK sont correctes
* Assurez-vous que les activités Target sont diffusées et rendues correctement
* Vérifier le bon fonctionnement des rapports
* Consultez à nouveau les audiences et les scripts de profil pour vous assurer qu’ils sont compatibles avec Platform Mobile SDK et l’extension Optimisation
* Assurez-vous que les intégrations à Adobe ou à des applications tierces fonctionnent correctement

Chaque implémentation de Target diffère selon l’architecture du site et les fonctionnalités utilisées. Vous pouvez utiliser les tableaux ci-dessous comme point de départ et ajouter des éléments uniques à votre implémentation.

## Validation technique et dépannage

La validation et le dépannage techniques avec Platform Mobile SDK et l’extension Decisioning sont considérablement améliorés avec Assurance. Consultez les pages de documentation suivantes pour en savoir plus sur cet outil essentiel :

* [Configuration des plug-ins Decisioning dans Assurance](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [Validation de la configuration d’Optimize SDK](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [Examen des requêtes et simulation de différentes expériences](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

Après avoir effectué les étapes de validation ci-dessus, vous pouvez être sûr que l’implémentation de Platform Mobile SDK avec l’extension Decisioning est prête à passer en production.

Félicitations, vous avez atteint la fin du tutoriel. Bonne chance pour la migration de votre implémentation Adobe Target vers l’extension Decisioning !

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
