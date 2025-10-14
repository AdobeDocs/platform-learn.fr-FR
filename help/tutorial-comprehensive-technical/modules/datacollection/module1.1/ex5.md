---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Analytics et de Adobe Audience Manager
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Analytics et de Adobe Audience Manager
kt: 5342
doc-type: tutorial
exl-id: a9022269-6db2-46c6-a82b-ec8d5b881a55
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 1.1.5 Mise en œuvre d’Adobe Analytics et de Adobe Audience Manager

## Contexte

Vous savez désormais que les données XDM circulent dans Platform. Vous découvrirez XDM dans [Module 1.2](./../module1.2/data-ingestion.md) et comment créer votre propre schéma pour effectuer le suivi des variables personnalisées. Pour l’instant, vous allez examiner ce qui se passe lorsque vous définissez votre Flux de données pour transférer des données vers Analytics et Audience Manager.

## Mappage de variables dans Analytics

Le [!DNL Web SDK] Adobe Experience Platform mappe automatiquement certaines valeurs, ce qui permet une nouvelle implémentation d’Analytics via le SDK web aussi rapide que possible. Les variables mappées automatiquement sont répertoriées [ici](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=fr#data-collection).

Pour les données XDM qui ne sont pas automatiquement mappées à Adobe Analytics, vous pouvez utiliser des [données contextuelles](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=fr) pour correspondre à votre [schéma](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr). Il peut ensuite être mappé à Analytics à l’aide de [règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=fr) pour renseigner les variables Analytics. Les données contextuelles et les règles de traitement seront des concepts familiers pour ceux qui ont travaillé avec Analytics par le passé, mais ne vous inquiétez pas pour les détails s’il s’agit de nouveaux concepts.

Vous pouvez également utiliser un ensemble d’actions et de listes de produits par défaut pour envoyer ou récupérer des données avec le SDK Web AEP. Pour ce faire, voir [Produits](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=fr#data-collection).

### Données contextuelles

Pour être utilisées par Analytics, les données XDM sont aplaties à l’aide de la notation par points et mises à disposition sous forme de `contextData`. La liste suivante de paires valeur présente un exemple de `context data` :

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### Règles de traitement

Toutes les données collectées par Edge Network sont accessibles via [&#x200B; règles de traitement &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=fr). Dans Analytics, vous pouvez utiliser des règles de traitement pour incorporer des données contextuelles dans les variables Analytics.

## Audience Manager sur l&#39;Edge Network Experience Platform

Le transfert côté serveur n’est pas un concept nouveau pour l’Audience Manager et le même processus qu’auparavant s’applique. Vous pouvez également synchroniser les identités.

## Vérifier le flux de données pour envoyer des données à Adobe Analytics

Si vous souhaitez envoyer les données collectées par Web SDK à Adobe Analytics et Adobe Audience Manager, procédez comme suit.

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) puis à **Flux de données**.

Dans le coin supérieur droit de l’écran, sélectionnez le nom du sandbox, qui doit être `--aepSandboxName--`. Ouvrez votre flux de données spécifique, nommé `--aepUserLdap-- - Demo System Datastream`.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Tu verras ça. Pour activer Adobe Analytics, cliquez sur **Ajouter un service**.

![&#x200B; Débogueur AEP &#x200B;](./images/aa2.png)

Tu verras ça. Sélectionnez le service **Adobe Analytics**, après quoi vous devrez ajouter la suite de rapports dans Adobe Analytics pour envoyer des données. Dans ce tutoriel, cela est hors de portée. Cliquez sur **Annuler**.

![&#x200B; Débogueur AEP &#x200B;](./images/aa3.png)

## Vérifier le flux de données pour envoyer des données à Adobe Audience Manager

Tu verras ça. Pour activer Adobe Audience Manager, cliquez sur **Ajouter un service**.

![&#x200B; Débogueur AEP &#x200B;](./images/aa2.png)

Tu verras ça. Sélectionnez le service **Adobe Audience Manager** après lequel vous pouvez décider d’activer ou de désactiver les destinations de cookie Adobe Audience Manager et/ou les destinations d’URL. Dans ce tutoriel, cette configuration est hors de portée. Cliquez sur **Annuler**.

![&#x200B; Débogueur AEP &#x200B;](./images/aam1.png)

Étape suivante : [1.1.6 Mise en œuvre d’Adobe Target](./ex6.md)

[Retour au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
