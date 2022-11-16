---
title: S’authentifier et accéder aux API Experience Platform
description: Découvrez comment accéder aux API Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 11%

---

# Authentification et accès [!DNL Experience Platform] API

Pour passer des appels aux API Adobe Experience Platform, vous devez d’abord accéder à un compte de développeur Experience Platform.

Pour obtenir des instructions détaillées sur la manière d’accéder à un compte de développeur, consultez la page [Tutoriel sur l’authentification des API Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

## Création et exportation de l’API Experience Platform vers Postman

[Postman](https://www.getpostman.com/) est un outil permettant aux développeurs d’interagir rapidement et facilement avec les API Adobe Experience Platform.

Console Adobe Developer **Détails de l’exportation pour Postman** Cette fonctionnalité permet d’exporter facilement tous les détails du compte requis pour accéder à une API Experience Platform et interagir avec elle dans un seul fichier d’environnement Postman, en supprimant la nécessité de copier et coller des valeurs de la console Adobe Developer dans Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Génération d’un jeton d’accès avec Postman

Utilisez la variable [Adobe des API du service Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) Obtention d’un jeton d’accès pour accéder aux API Adobe Experience Platform à des fins d’utilisation hors production

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Comme indiqué dans la collection Postman de génération de jeton d’accès Adobe I/O, les méthodes de génération signalées sont adaptées à un usage hors production. La signature locale charge une bibliothèque JavaScript à partir d’un hôte tiers et la signature à distance envoie la clé privée à un service Web géré et détenu par un Adobe. Bien qu’Adobe ne stocke pas cette clé privée, les clés de production ne doivent jamais être partagées avec personne.

## Interaction avec les API Adobe I/O à l’aide de Postman

Explorez l’interaction avec les API d’Adobe I/O à l’aide du [Collections Postman d’API Experience Platform fournies par Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), en s’appuyant sur la variable [Variables d’environnement d’Adobe I/O](#export-adobe-io-integration-details-to-postman) et [jeton d’accès généré](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Notez que les collections Postman fournies par l’Adobe peuvent ne pas exister pour chaque API d’Adobe I/O, mais le [Collections Postman de l’API Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) peut être utilisé comme guide pour définir vos propres collections Postman pour ces cas d’utilisation.

## Ressources supplémentaires

* [Adobe I/O Console](https://console.adobe.io)
* [Exemples de Postman Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples)
   * [Collection Postman de génération de jetons d’accès Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Collections Postman des API Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Télécharger Postman](https://www.getpostman.com/)
