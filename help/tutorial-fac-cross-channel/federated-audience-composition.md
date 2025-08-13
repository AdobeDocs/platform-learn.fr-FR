---
title: Enrichissement des audiences Experience Platform avec des données fédérées
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Enrichissement des audiences Experience Platform avec des données fédérées
description: Dans cet exercice visuel, une audience Experience Platform est enrichie de données fédérées.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 3de9721332379f9fd3dd45768ba2ca2308e09357
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---

# Enrichissement des audiences Experience Platform avec des données fédérées

La composition de l’audience fédérée vous permet d’enrichir les audiences existantes dans Adobe Experience Platform (AEP) en utilisant les données de l’audience composée qui ont été fédérées à partir de l’entrepôt de données d’entreprise. Ces données ne seront pas conservées dans les profils client Adobe Experience Platform.

## Lecture d’une audience AEP dans une composition fédérée

Dans cet exercice visuel, nous utilisons l’audience **visiteur de la page de demande de prêt financier** stockée dans le service de profil AEP pour démarrer notre composition fédérée. Il utilise les données fédérées dans Snowflake pour déterminer la préapprobation en fonction de la cote de crédit et de l’activité de prêt.

![federated-composition-example](assets/snowflake-preapproval.png)

### Étapes

1. **Mappez une audience AEP** à la destination de la composition d’audiences fédérées.
2. **Créez votre composition** avec l’audience mappée en tant qu’audience Lecture.
3. **Réconcilier les identités** dans votre audience lue à joindre aux données fédérées.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

Nous allons examiner un autre exemple d’utilisation des données fédérées pour [prendre en charge la personnalisation « sur le moment »](drive-in-the-moment-personalization.md) !
