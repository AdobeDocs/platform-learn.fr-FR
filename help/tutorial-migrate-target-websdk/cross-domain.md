---
title: Activation de la prise en charge inter-domaines - Migration de Target d’at.js 2.x vers le SDK Web
description: Découvrez comment configurer Adobe Target pour des scénarios de navigateur web inter-domaines et d’applications mobiles à l’aide du SDK web Experience Platform.
exl-id: 6ec24ddc-8f6d-4331-a3ae-bd0f3a7d6e78
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Activation des profils de visiteur interdomaines

Le SDK Web Platform prend en charge les fonctionnalités de partage des identifiants visiteur qui permettent aux clients de diffuser des expériences personnalisées plus précisément sur vos domaines. Cette fonctionnalité vous permet d’offrir une personnalisation cohérente sur plusieurs domaines et d’améliorer la précision des rapports d’activité des visiteurs, sans vous fier à des cookies tiers.

## Conditions préalables

Pour utiliser le partage d’identifiants entre domaines, vous devez utiliser la version 2.11.0 ou ultérieure du SDK Web Platform. Cette fonctionnalité est également compatible avec VisitorAPI.js version 1.7.0 ou ultérieure.

Le partage des identifiants inter-domaines fonctionne en ajoutant un paramètre de chaîne de requête `adobe_mc` spécial à l’URL du domaine de destination. Ce paramètre est utilisé pour spécifier l’identifiant visiteur au lieu de générer un nouvel identifiant ou d’utiliser un identifiant existant.

Le domaine de destination doit utiliser l’une de ces bibliothèques pour le partage des identifiants inter-domaines afin de traiter le paramètre `adobe_mc` et de partager correctement l’identifiant visiteur.

## Comparaison des approches

Avant de procéder à l’implémentation, déterminez d’abord si votre implémentation existante utilise la fonction `visitor.appendVisitorIDsTo()`. Tout code personnalisé utilisant cette fonction doit être mis à jour pour utiliser la nouvelle commande du SDK Web `appendIdentityToUrl`.

| VisitorAPI.js | SDK Web de Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Utilisation de la commande `appendIdentityToURL`

Pour le partage d’ID inter-domaines, le SDK Web version 2.11.0 ajoute la prise en charge de la commande `appendIdentityToUrl`. Lorsqu’elle est utilisée, cette commande génère le paramètre de chaîne de requête `adobe_mc`.

La commande accepte un objet avec une propriété, `url`, et renvoie un objet avec l’URL de propriété.

Cette commande n’attend aucune mise à jour du consentement. Si le consentement n’a pas été fourni, l’URL est renvoyée inchangée.

Si aucun ECID n’est fourni, le point de terminaison `/acquire` est appelé pour générer un ECID.

Vous trouverez ci-dessous un exemple de mise en oeuvre du partage d’ID entre domaines.

Ce code ajoute un écouteur d’événement pour tous les clics sur la page. Si le clic se trouvait sur un lien vers un domaine correspondant, ici adobe.com ou behance.com, il ajoute l’identité à l’URL et y redirige l’utilisateur.

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
>Lors de l’utilisation de la fonctionnalité de balises (anciennement Launch) pour mettre en oeuvre le SDK Web, le partage d’ID entre domaines peut être réalisé sans code personnalisé. Pour plus d’informations, consultez la [documentation dédiée](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) .

>[!NOTE]
>
>Le SDK Web Platform prend également en charge le partage d’ID entre appareils mobiles et web pour les cas d’utilisation d’applications mobiles natives. Pour plus d&#39;informations, consultez la documentation dédiée sur le [partage d&#39;ID entre appareils mobiles et sur le web et entre domaines](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Ensuite, découvrez comment [mettre à jour les audiences et les scripts de profil](update-audiences.md) pour garantir la compatibilité avec le SDK Web Platform.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
