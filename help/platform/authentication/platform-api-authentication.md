---
title: S’authentifier et accéder aux API Experience Platform
description: Découvrez comment accéder aux API Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 16%

---

# Authentification et accès [!DNL Experience Platform] API

Pour envoyer des requêtes aux API Adobe Experience Platform, vous devez disposer d’un compte de développeur Experience Platform.

## Création d’un projet dans la console Adobe Developer et exportation d’un environnement Postman

[[!DNL Postman]](https://www.postman.com/) est un outil permettant aux développeurs d’interagir rapidement et facilement avec les API Adobe Experience Platform.

Console Adobe Developer **Détails de l’exportation pour Postman** Cette fonctionnalité permet d’exporter facilement tous les détails du compte requis pour accéder à une API Experience Platform et interagir avec elle dans un seul fichier d’environnement Postman, en supprimant la nécessité de copier et coller des valeurs de la console Adobe Developer dans Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>Après avoir créé vos informations d’identification d’API, un administrateur système de votre entreprise doit associer ces informations à un rôle d’Experience Platform.


## Génération d’un jeton d’accès avec Postman

Utilisez la variable [Adobe des API du service Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) pour obtenir un jeton d’accès afin d’accéder aux API Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interaction avec les API Experience Platform à l’aide de Postman

Explorez l’interaction avec les API Adobe Experience Platform à l’aide de la variable [Collections Postman d’API Experience Platform fournies par Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), en s’appuyant sur la variable [Variables d’environnement de la console Adobe Developer](#export-adobe-io-integration-details-to-postman) et [jeton d’accès généré](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Ressources supplémentaires

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Exemples de Postman Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples)
   * [Collection Postman Identity Management System pour la génération de jetons d’accès](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Collections Postman de l’API Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Télécharger Postman](https://www.postman.com/)
