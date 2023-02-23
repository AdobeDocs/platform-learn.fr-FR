---
title: Activation de la prise en charge inter-domaines | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment configurer Adobe Target pour des scénarios de navigateur web inter-domaines et d’applications mobiles à l’aide du SDK web Experience Platform.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Activation des profils de visiteur interdomaines

Le SDK Web Platform prend en charge les fonctionnalités de partage des identifiants visiteur qui permettent aux clients de diffuser des expériences personnalisées plus précisément sur vos domaines. Cette fonctionnalité vous permet d’offrir une personnalisation cohérente sur plusieurs domaines et d’améliorer la précision des rapports d’activité des visiteurs, sans vous fier à des cookies tiers.

## Conditions préalables

Pour utiliser le partage d’identifiants entre domaines, vous devez utiliser la version 2.11.0 ou ultérieure du SDK Web Platform. Cette fonctionnalité est également compatible avec VisitorAPI.js version 1.7.0 ou ultérieure.

Le partage des identifiants inter-domaines fonctionne en ajoutant un `adobe_mc` paramètre de chaîne de requête vers l’URL du domaine de destination. Ce paramètre est utilisé pour spécifier l’identifiant visiteur au lieu de générer un nouvel identifiant ou d’utiliser un identifiant existant.

Le domaine de destination doit utiliser l’une de ces bibliothèques pour le partage d’ID inter-domaines afin de traiter la variable `adobe_mc` et partager correctement l’identifiant visiteur.

## Comparaison des approches

Avant de procéder à l’implémentation, déterminez d’abord si votre implémentation existante utilise la variable `visitor.appendVisitorIDsTo()` fonction . Tout code personnalisé utilisant cette fonction doit être mis à jour pour utiliser la nouvelle fonction `appendIdentityToUrl` SDK Web, commande.

| VisitorAPI.js | SDK Web de Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## En utilisant la variable `appendIdentityToURL` command

Pour le partage d’identifiants entre domaines, le SDK Web version 2.11.0 prend en charge la variable `appendIdentityToUrl` . Lorsqu’elle est utilisée, cette commande génère le `adobe_mc` paramètre de chaîne de requête.

La commande accepte un objet avec une propriété, `url`, et renvoie un objet avec l’URL de propriété.

Cette commande n’attend aucune mise à jour du consentement. Si le consentement n’a pas été fourni, l’URL est renvoyée inchangée.

Si aucun ECID n’est fourni, la variable `/acquire` endpoint est appelé pour générer un ECID.

Vous trouverez ci-dessous un exemple de mise en oeuvre du partage d’ID entre domaines.

Ce code ajoute un écouteur d’événement pour tous les clics sur la page. Si le clic se trouvait sur un lien vers un domaine correspondant, adobe.com ou behance.com, dans ce cas, il ajoute l’identité à l’URL et y redirige l’utilisateur.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>Lors de l’utilisation de la fonctionnalité de balises (anciennement Launch) pour mettre en oeuvre le SDK Web, le partage d’ID entre domaines peut être réalisé sans code personnalisé. Reportez-vous à la section [documentation dédiée](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) pour plus d’informations.

>[!NOTE]
>
>Le SDK Web Platform prend également en charge le partage d’ID entre appareils mobiles et web pour les cas d’utilisation d’applications mobiles natives. Pour plus d’informations, reportez-vous à la documentation dédiée à la section [partage d’identifiants entre appareils mobiles et web et inter-domaines](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Ensuite, apprenez à [mise à jour des audiences et des scripts de profil](update-audiences.md) pour garantir la compatibilité avec le SDK Web Platform.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).