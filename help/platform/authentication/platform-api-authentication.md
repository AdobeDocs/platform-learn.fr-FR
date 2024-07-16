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
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# Authentification et accès aux API [!DNL Experience Platform]

Découvrez comment commencer à utiliser les API Adobe Experience Platform. Ce tutoriel vous guide tout au long du processus de création des informations d’identification d’authentification et de démarrage de la création de requêtes API Experience Platform.

## Créer un projet dans Adobe Developer Console et exporter un environnement Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) est une application tierce qui permet aux développeurs d’interagir rapidement et facilement avec les API Adobe Experience Platform.

La fonctionnalité [ ](https://developer.adobe.com/console/home) **Exporter les détails pour Postman** permet d’exporter facilement les détails du compte requis pour accéder et interagir avec des API Experience Platform dans un seul fichier d’environnement Postman, en supprimant la nécessité de copier-coller des valeurs de Adobe Developer Console dans Postman.

>[!IMPORTANT]
>
>Pour accéder au [Adobe Developer Console](https://developer.adobe.com/console/home), vous devez être un [administrateur système](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) ou un [développeur](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) dans le [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Après avoir créé vos informations d’identification d’API, un administrateur système doit associer ces informations à un rôle dans l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

## Génération d’un jeton d’accès avec Postman{#generate-an-access-token-with-postman}

Utilisez les [ API Adobe Service ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) pour obtenir un jeton d’accès afin d’accéder aux API Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)


## Interaction avec les API Experience Platform à l’aide de Postman

Explorez l’interaction avec les API Adobe Experience Platform à l’aide des [ collections Postman d’API Experience Platform fournies par l’Adobe ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), en vous basant sur les [variables d’environnement Adobe Developer Console](#export-integration-details-to-postman) et le [jeton d’accès généré](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)


## Ressources référencées dans ces vidéos

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [ Exemples Postman Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples)
   * [Collection Postman Identity Management System pour la génération de jetons d’accès](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Collections Postman de l’API Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Télécharger Postman](https://www.postman.com/)
