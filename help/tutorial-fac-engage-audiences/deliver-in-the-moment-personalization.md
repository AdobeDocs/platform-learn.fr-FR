---
title: Personnalisation instantanée à l’aide d’Edge Network
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Personnalisation instantanée à l’aide d’Edge Network
description: Dans cet exercice, l’audience fédérée est évaluée sur Edge en vue d’un reciblage instantané.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Personnalisation instantanée à l’aide d’Edge Network

La composition de l’audience fédérée vous permet d’enrichir les audiences existantes dans Adobe Experience Platform (AEP) en utilisant les données de l’audience composée qui ont été fédérées à partir de l’entrepôt de données d’entreprise. Ces données ne seront pas conservées dans Adobe Experience Platform, mais vous pouvez utiliser les fonctionnalités de [transfert d’événement](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview){target="_blank"} pour envoyer ces données directement à votre entrepôt de données.

Dans cet exercice, nous utilisons une audience fédérée interrogée avec la cote de crédit et l’activité de prêt pour enrichir l’audience comportementale des visiteurs de la page web de la demande de prêt.

En évaluant cette audience sur Edge, nous reciblons instantanément les visiteurs de la page de demande de prêt préapprouvés avec des offres personnalisées sur le site.

![enrichissement-de-l’audience-Edge](assets/edge-audience-enrich.png)

## Étapes

1. **Enregistrer et démarrer** votre composition d’audience fédérée. Une fois la composition exécutée, l’audience fédérée apparaît dans le portail d’audience.
2. **Créer une règle d’audience** à l’aide des attributs de profil et des événements d’expérience du service de profil, en incorporant votre audience fédérée.

Résumons cela par un [résumé des enseignements et des points à retenir finaux](conclusion.md) !
