---
title: Mise à jour des audiences et des scripts de profil - Migration de Target d’at.js 2.x vers le SDK Web
description: Découvrez comment mettre à jour les audiences Adobe Target et les scripts de profil pour des raisons de compatibilité avec le SDK Web Experience Platform.
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Mise à jour des audiences Target et des scripts de profil pour la compatibilité du SDK Web Platform

Après avoir effectué les mises à jour techniques pour migrer Target vers le SDK Web Platform, vous devrez peut-être mettre à jour certaines de vos audiences, scripts de profil et activités pour garantir une transition fluide.

Tous les paramètres de mbox Target doivent être transmis au format XDM avec une mise en oeuvre du SDK Web Platform. Avant de publier vos modifications en production, vous devez :

* Mise à jour des audiences qui utilisent des paramètres de mbox
* Mise à jour des scripts de profil utilisant des paramètres de mbox
* Mettez à jour toutes les offres et activités à l’aide du remplacement des jetons de paramètre de mbox (par exemple, `${mbox.parameter_name}`).

## Ajustement des audiences

Toutes les audiences qui utilisent des paramètres de mbox personnalisés doivent être mises à jour pour utiliser les nouveaux noms de paramètres XDM. Par exemple, un paramètre personnalisé pour `page_name` sera probablement mappé à `web.webpagedetails.pageName`.

Pour garantir la compatibilité avec at.js et le SDK Web Platform, une méthode consiste à mettre à jour les audiences appropriées afin que les conditions `OR` soient utilisées, comme illustré ci-dessous :

![Comment afficher la mise à jour d’une audience Target pour la compatibilité du SDK Web Platform](assets/target-audience-update.png){zoomable="yes"}

## Modifier les scripts de profil

Les scripts de profil doivent être mis à jour pour référencer de nouveaux noms de paramètres XDM, semblables aux audiences. Outre la modification des noms des paramètres de mbox, il n’existe aucune différence dans le fonctionnement des scripts de profil entre une implémentation d’at.js et d’un SDK Web Platform.

Une méthode permettant de garantir la compatibilité consiste à utiliser des conditions `OR` dans le code de script de votre profil.

Exemple de script de profil :

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Mise à jour du script de profil pour la compatibilité du SDK Web Platform :

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Pour plus d’informations et de bonnes pratiques, consultez la documentation dédiée sur les [scripts de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=fr).

## Mise à jour des jetons de paramètre pour le contenu dynamique

Si vous disposez d’offres, de conceptions de recommandations ou d’activités qui utilisent le [remplacement de contenu dynamique](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html?lang=fr), elles doivent peut-être être être mises à jour en conséquence pour tenir compte des nouveaux noms de paramètres XDM.

Selon la manière dont vous utilisez le remplacement de jetons pour les paramètres de mbox, vous pouvez améliorer votre configuration existante pour tenir compte des anciens et des nouveaux noms de paramètre. Cependant, dans les cas où le code JavaScript personnalisé n’est pas possible, par exemple dans les offres JSON, vous devez créer des copies et effectuer des mises à jour une fois la migration terminée et activée sur votre site de production.

Exemple d’offre JSON :

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Exemple d’offre JSON utilisant les noms des paramètres du SDK Web Platform :

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Si vous choisissez d’effectuer des ajustements après la migration afin de prendre en compte les nouveaux noms de paramètres de mbox XDM, veillez à suspendre toute activité impactée pendant l’événement de migration afin d’empêcher l’affichage des erreurs d’activité aux visiteurs.

Ensuite, découvrez comment [valider l’implémentation de Target](validate.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
