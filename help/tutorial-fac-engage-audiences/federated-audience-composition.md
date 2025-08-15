---
title: Enrichissement des audiences avec des données d’entrepôt de données
seo-title: Enrich Audiences with warehouse data | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Enrichissement des audiences avec des données d’entrepôt de données
description: Dans cet exercice, une audience Experience Platform est enrichie de données d’entrepôt de données.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
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

Nous allons examiner un autre exemple d’utilisation de données fédérées pour [offrir une personnalisation « à l’instant »](deliver-in-the-moment-personalization.md) !
