---
title: S’authentifier et accéder aux API Experience Platform
description: Découvrez comment accéder aux API Adobe Experience Platform.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 42427df298e2c5ae734ce050e935378db51e66a1
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 18%

---

# Authentification et accès aux [!DNL Experience Platform]API

Découvrez comment commencer à utiliser les API Adobe Experience Platform. Ce tutoriel vous guide tout au long du processus de création des informations d’identification d’authentification et de démarrage de la création de requêtes API Experience Platform.

## Création d’un projet dans la console Adobe Developer et exportation d’un environnement Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) est une application tierce qui aide les développeurs à interagir rapidement et facilement avec les API Adobe Experience Platform.

[Console Adobe Developer](https://developer.adobe.com/console/home) **Détails de l’exportation pour Postman** Cette fonctionnalité permet d’exporter facilement les détails du compte requis pour accéder et interagir avec une API Experience Platform dans un seul fichier d’environnement Postman, en supprimant la nécessité de copier-coller des valeurs de la console Adobe Developer dans Postman.

>[!IMPORTANT]
>
>Pour accéder au [Console Adobe Developer](https://developer.adobe.com/console/home), vous devez être [Administrateur système](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) ou [Développeur](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) dans le [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Après avoir créé vos informations d’identification d’API, un administrateur système doit associer ces informations à un rôle dans l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)




## Génération d’un jeton d’accès avec Postman{#generate-an-access-token-with-postman}

Utilisez la variable [Adobe des API du service Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) pour obtenir un jeton d’accès afin d’accéder aux API Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interaction avec les API Experience Platform à l’aide de Postman

Explorez l’interaction avec les API Adobe Experience Platform à l’aide de la variable [Collections Postman d’API Experience Platform fournies par Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), en s’appuyant sur la variable [Variables d’environnement de la console Adobe Developer](#export-integration-details-to-postman) et [jeton d’accès généré](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Ressources référencées dans ces vidéos

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Exemples de Postman Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples)
   * [Collection Postman Identity Management System pour la génération de jetons d’accès](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Collections Postman de l’API Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Télécharger Postman](https://www.postman.com/)
