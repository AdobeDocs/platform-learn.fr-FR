---
title: Enrichissement des audiences avec des données d’entrepôt de données
seo-title: Enrich Audiences with Warehouse Data | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Enrichissement des audiences avec des données d’entrepôt de données
description: Dans cet exercice, une audience Experience Platform est enrichie de données d’entrepôt de données.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# Enrichissement des audiences avec des données d’entrepôt de données

La composition de l’audience fédérée vous permet d’enrichir les audiences existantes dans Adobe Experience Platform (AEP) en utilisant les données de l’audience composée qui ont été fédérées à partir de l’entrepôt de données d’entreprise. Ces données ne seront pas conservées dans les profils client Adobe Experience Platform.

## Lecture d’une audience dans une composition fédérée

Dans cet exercice, nous utilisons l’audience **visiteur de la page de demande de prêt financier** stockée dans le service de profil Experience Platform pour démarrer notre composition fédérée. Il utilise les données fédérées dans Snowflake pour déterminer la préapprobation en fonction de la cote de crédit et de l’activité de prêt.

![federated-composition-example](assets/snowflake-preapproval.png)

### Étapes

1. **Mappez une audience AEP** à la destination de la composition d’audiences fédérées.
2. **Créez votre composition** avec l’audience mappée en tant qu’audience Lecture.
3. **Réconcilier les identités** dans votre audience lue à joindre aux données fédérées.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

Nous allons examiner un autre exemple d’utilisation des données fédérées pour [prendre en charge la personnalisation « sur le moment »](deliver-in-the-moment-personalization.md) !
