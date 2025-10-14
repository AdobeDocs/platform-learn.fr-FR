---
title: Foundation - Ingestion de données
description: Foundation - Ingestion de données
kt: 5342
doc-type: tutorial
exl-id: 976d801a-3dcb-4cd9-8b9f-b1c964fe7c25
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 1.2 Foundation - Ingestion de données

Dans ce module, l’objectif est de tout savoir sur l’ingestion de données. Vous en apprendrez plus sur l’ingestion de données dans Diffusion en continu et par lots. Vous implémenterez l’ingestion des données en flux continu à l’aide de Launch, de sorte que le comportement des clients sur le site Web pratique du Lab soit diffusé en flux continu vers Adobe Experience Platform en temps réel. Vous découvrirez l’ingestion de données par lots à l’aide d’un workflow Adobe Experience Platform permettant de prendre un fichier CSV, de le mapper à un schéma XDM, puis de l’ingérer dans Adobe Experience Platform.

## Objectifs d’apprentissage

- Découvrez comment créer un schéma XDM dans Adobe Experience Platform
- Découvrez comment créer des jeux de données dans Adobe Experience Platform
- Découvrez comment créer un point d’entrée de diffusion en continu et configurer l’extension Adobe Experience Platform dans Launch
- Découvrez comment créer des règles dans Launch pour diffuser des données vers Adobe Experience Platform
- Découvrez comment intégrer Adobe Experience Platform Launch à une page web
- Découvrez comment utiliser un workflow Adobe Experience Platform pour ingérer un fichier CSV dans Adobe Experience Platform

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à Adobe Experience Platform Launch : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès à Postman

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation de l’Experience League &#x200B;](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[1.2.1 Explorer le site Web](./ex1.md)

Au cours de cet exercice, vous allez explorer le site web que vous utiliserez dans le cadre de cette activation.

[1.2.2 Configuration des schémas et définition des identifiants](./ex2.md)

Dans cet exercice, vous allez configurer les schémas XDM requis pour capturer les informations de profil et le comportement du client. Dans chaque schéma XDM, vous devez également configurer un identifiant principal auquel lier toutes les informations.

[1.2.3 Configuration De Jeux De Données](./ex3.md)

Dans cet exercice, vous allez récupérer les jeux de données requis pour capturer et stocker les informations de profil et le comportement des clients.

[1.2.4 Ingestion de données à partir de sources hors ligne](./ex4.md)

Dans cet exercice, vous allez accéder au site web et à l’application mobile et vous comporter comme un client en diffusant des données en continu vers Platform.

[1.2.5 Zone D’Atterrissage Des Données](./ex5.md)

Configurez votre connecteur Source de zone d’atterrissage de données avec le stockage Azure Blob.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

![Insiders de la technologie &#x200B;](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
