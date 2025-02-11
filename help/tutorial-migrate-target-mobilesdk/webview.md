---
title: Activer la prise en charge inter-domaines - Migration d’Adobe Target vers Adobe Journey Optimizer - Extension mobile Decisioning
description: Découvrez comment configurer Adobe Target pour des scénarios inter-domaines et mobiles vers des navigateurs web à l’aide d’Experience Platform Web SDK.
exl-id: 1dc78771-b85c-4127-8d1b-6558509f9db8
source-git-commit: 18f0190881d2a997491d4d6ce367add74cc30288
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# Activer les profils de visiteurs interdomaines

Platform Web SDK prend en charge les fonctionnalités de partage des identifiants visiteur qui permettent aux clients de fournir des expériences personnalisées plus précisément sur l’ensemble de vos domaines. Cette fonctionnalité vous permet de fournir une personnalisation cohérente sur l’ensemble des domaines et améliore la précision de vos rapports d’activité des visiteurs, sans recourir à des cookies tiers.

## Conditions préalables

Pour utiliser le partage d’identifiants entre domaines, vous devez utiliser la version 2.11.0 ou ultérieure de Platform Web SDK. Cette fonctionnalité est également compatible avec VisitorAPI.js version 1.7.0 ou ultérieure.

Le partage d’identifiants entre domaines fonctionne en ajoutant un paramètre de chaîne de requête `adobe_mc` spécial à l’URL du domaine de destination. Ce paramètre est utilisé pour spécifier l’identifiant visiteur au lieu de générer un nouvel identifiant ou d’utiliser un identifiant existant.

Le domaine de destination doit utiliser l’une de ces bibliothèques pour le partage d’identifiants entre domaines afin de traiter le paramètre `adobe_mc` et de partager correctement l’identifiant visiteur.

## Comparaison des approches

Avant l’implémentation, déterminez d’abord si votre implémentation existante utilise la fonction `visitor.appendVisitorIDsTo()` . Tout code personnalisé utilisant cette fonction doit être mis à jour pour utiliser la nouvelle commande `appendIdentityToUrl` Web SDK.

| VisitorAPI.js | SDK Web de Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Utilisation de la commande `appendIdentityToURL`

Pour le partage d’identifiants entre domaines, la version 2.11.0 de Web SDK prend en charge la commande `appendIdentityToUrl`. Lorsqu’elle est utilisée, cette commande génère le paramètre de chaîne de requête `adobe_mc`.

La commande accepte un objet avec une propriété, `url`, et renvoie un objet avec l’URL de propriété.

Cette commande n’attend aucune mise à jour du consentement. Si le consentement n’a pas été fourni, l’URL est renvoyée inchangée.

Si aucun ECID n’est fourni, le point d’entrée `/acquire` est appelé pour générer un ECID.

Vous trouverez ci-dessous un exemple d’implémentation du partage d’identifiants entre domaines.

Ce code ajoute un écouteur d’événement pour tous les clics sur la page. Si le clic portait sur un lien vers un domaine correspondant, dans ce cas adobe.com ou behance.com, il ajoute l’identité à l’URL et redirige l’utilisateur vers celle-ci.

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
>Lors de l’utilisation de la fonctionnalité Balises (anciennement Launch) pour implémenter Web SDK, le partage d’ID entre domaines peut être effectué sans code personnalisé. Pour plus d’informations, consultez la [documentation dédiée](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension).

>[!NOTE]
>
>Platform Web SDK prend également en charge le partage d’identifiants de mobile à web pour les cas d’utilisation natifs d’applications mobiles. Pour plus d’informations, reportez-vous à la documentation dédiée au [partage d’identifiants entre appareils mobiles et domaines](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Découvrez ensuite comment [mettre à jour les audiences et les scripts de profil](update-audiences.md) pour garantir la compatibilité avec Platform Web SDK.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
