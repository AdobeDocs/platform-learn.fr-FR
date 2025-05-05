---
title: Mise à jour des audiences Target et des scripts de profil - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Adobe Journey Optimizer - Decisioning
description: Découvrez comment mettre à jour les audiences Adobe Target et les scripts de profil pour des raisons de compatibilité avec l’extension Decisioning.
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Mise à jour des audiences Target et des scripts de profil pour la compatibilité des extensions mobiles Decisioning


Une fois les mises à jour techniques effectuées pour migrer Target vers l’extension Decisioning, vous devrez peut-être mettre à jour certaines de vos audiences, scripts de profil et activités pour assurer une transition fluide.

>[!INFO]
>
>Si vous migrez tous les paramètres de mbox vers l’objet `data.__adobe.target`, vous n’avez pas besoin de mettre à jour vos audiences, scripts de profil et activités comme illustré ci-dessous.


Si vous migrez les paramètres de mbox vers l’objet `xdm`, avant de publier vos modifications en exploitation, vous devez :

* Mettre à jour les audiences qui utilisent les paramètres de mbox
* Mettre à jour les scripts de profil utilisant des paramètres de mbox
* Mettez à jour les offres et les activités en remplaçant le jeton du paramètre mbox (par exemple, `${mbox.parameter_name}`).

## Ajuster les audiences

Si vous migrez les paramètres de mbox vers l’objet `xdm`, les audiences qui utilisent des paramètres de mbox personnalisés doivent être mises à jour pour utiliser les nouveaux noms de paramètres XDM. Par exemple, un paramètre personnalisé pour `page_name` serait probablement mappé à `web.webpagedetails.pageName`.

Pour garantir la compatibilité avec les extensions Target et Decisioning, mettez à jour les audiences pertinentes afin que des conditions `OR` soient utilisées, comme illustré ci-dessous :

![Comment afficher et mettre à jour une audience cible pour la compatibilité de l’extension Decisioning ](assets/target-audience-update.png){zoomable="yes"}

## Modifier les scripts de profil

Si vous migrez les paramètres de mbox vers l’objet `xdm`, les scripts de profil doivent être mis à jour pour référencer les nouveaux noms de paramètre XDM, similaires aux audiences. Outre la modification des noms de paramètre mbox, il n’existe aucune différence dans le fonctionnement des scripts de profil entre une implémentation de Target et de Decisioning.

Pour garantir la compatibilité, une méthode consiste à utiliser des conditions `OR` dans le code de script de votre profil.

Exemple de script de profil :

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Mise à jour du script de profil pour la compatibilité de Platform Web SDK :

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Pour plus d’informations et de bonnes pratiques, reportez-vous à la documentation dédiée sur [les scripts de profil](https://experienceleague.adobe.com/fr/docs/target/using/audiences/visitor-profiles/profile-parameters).

## Mise à jour des jetons de paramètre pour le contenu dynamique

Si vous migrez les paramètres de mbox vers l’objet `xdm` et que vous disposez d’offres, de conceptions de recommandations ou d’activités qui utilisent le [remplacement de contenu dynamique](https://experienceleague.adobe.com/fr/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer), ils doivent peut-être être mis à jour en conséquence pour tenir compte des nouveaux noms de paramètre XDM.

Selon la manière dont vous utilisez le remplacement de jeton pour les paramètres de mbox, vous pouvez améliorer votre configuration existante pour tenir compte des anciens et des nouveaux noms de paramètre. Cependant, dans les cas où le code JavaScript personnalisé n’est pas possible, comme dans les offres JSON, vous devez créer des copies et effectuer des mises à jour une fois la migration terminée et active sur votre site de production.

Exemple d’offre JSON :

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Exemple d’offre JSON utilisant des noms de paramètres d’objet XDM :

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Si vous choisissez d’effectuer des ajustements après la migration pour tenir compte des nouveaux noms de paramètres de mbox XDM, veillez à suspendre les activités affectées pendant l’événement de migration afin d’éviter que les visiteurs ne rencontrent des erreurs d’affichage des activités.


Découvrez ensuite comment [valider l’implémentation de Target](validate.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
