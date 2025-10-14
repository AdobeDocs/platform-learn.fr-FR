---
title: Validation des mises en oeuvre de Target avec le SDK Web - Migration de Target d’at.js 2.x vers le SDK Web
description: Découvrez comment valider des activités et déboguer une mise en oeuvre Adobe Target à l’aide du SDK Web de Adobe Experience Platform.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Validation de la mise en oeuvre du SDK Web Platform

Après avoir migré votre implémentation Target d’at.js vers le SDK Web Platform, il est important de valider que tout fonctionne correctement avant de publier toute modification sur votre site de production. Adobe recommande ce qui suit, qui est décrit en détail sur cette page :

* Effectuez une validation technique pour vous assurer que la mise en oeuvre de base et les requêtes et réponses du SDK Web Platform sont correctes.
* Assurez-vous que les activités Target sont diffusées et rendues correctement.
* Vérifier que le reporting fonctionne correctement
* Révisez les audiences et les scripts de profil pour vous assurer qu’ils sont compatibles avec le SDK Web Platform.
* Assurez-vous que les intégrations avec des applications d’Adobe ou tierces fonctionnent correctement

Chaque mise en oeuvre de Target est différente selon l’architecture du site et les fonctionnalités utilisées. Vous pouvez utiliser les tableaux ci-dessous comme point de départ et ajouter tout élément unique à votre mise en oeuvre. La [page de débogage](debugging.md) de ce tutoriel présente les outils que vous pouvez utiliser pour faciliter cette validation.

## Validation technique

| Élément de validation | Notes |
|---|---|
| Le fragment de code at.js prémasquant n’est plus présent sur la page. | Le SDK Web Platform ne supprime pas automatiquement le style avec l’ID `at-body-style`. Si vous laissez cet ancien fragment sur la page, le contenu est masqué jusqu’à ce que le délai d’expiration du fragment soit atteint. |
| La bibliothèque at.js n’est plus présente sur la page. | Vérifiez qu’il n’existe aucun objet &quot;adobe.target&quot; dans la console des outils de développement de votre navigateur. L’inclusion du SDK Web Platform et d’at.js entraîne un comportement de rendu inattendu. |
| Les paramètres attendus se trouvent dans le XDM et les objets de données de la requête `sendEvent` | |
| Le catalogue Recommendations est mis à jour comme prévu si vous utilisez des requêtes de page pour renseigner le catalogue. | |
| Les paramètres de profil sont transmis à Target avec succès. | Affichage des traces Edge dans Debugger |
| Les paramètres mappés à XDM dans le mappeur de flux de données sont transmis correctement à Target. | Validation à l’aide de la fonction Edge Trace du débogueur et/ou de l’assurance |
| Le contenu cible est renvoyé dans les réponses `sendEvent` applicables | Attendu lorsque l’option `renderDecisions` est définie sur `true` ou que les portées sont demandées et que l’utilisateur est admissible pour une activité Target particulière. |
| Un événement `decisioning.propositionDisplay` se déclenche après le rendu des activités basées sur VEC | Les activités rendues automatiquement et à la demande doivent comporter des appels d’événement distincts. |
| Un événement `decisioning.propositionDisplay` se déclenche après le rendu des activités basées sur des formulaires | Applicable uniquement pour certaines mises en oeuvre. Nécessite du code personnalisé pour exécuter cet appel. |
| Un événement `decisioning.propositionDisplay` se déclenche lorsqu’une offre est appliquée à un changement de vue SPA | Applicable uniquement pour les mises en oeuvre SPA |
| Un événement `decisioning.propositionDisplay` ne se déclenche PAS lorsqu’un composant SPA est rendu pour une vue donnée. | Applicable uniquement pour les mises en oeuvre SPA |
| Un événement `decisioning.propsitionInteract` se déclenche après une conversion d’activité | Les conversions &quot;A cliqué sur un élément&quot; et personnalisées migrées depuis at.js `trackEvent` ou `sendNotifications` doivent comporter des appels d’événement distincts. |
| Les jetons de réponse sont renvoyés dans la réponse `sendEvent` et ont des valeurs attendues. | Les jetons de réponse doivent fonctionner normalement avec le SDK Web |
| Les ECID sont cohérents entre les pages avec le SDK Web et at.js. | S’applique aux migrations page par page. Les offres de redirection ne doivent pas fonctionner dans ces types de migrations |


## Diffusion et rendu des activités

| Élément de validation | Notes |
|---|---|
| Les activités basées sur VEC s’affichent correctement au chargement de la page. | Il est préférable de valider les modifications de code personnalisé et les modifications de base, telles que la réorganisation des éléments ou le remplacement de texte. |
| Les activités basées sur le compositeur d’expérience visuelle s’affichent correctement lors des modifications SPA vue | Applicable uniquement pour les mises en oeuvre SPA |
| Les activités basées sur des formulaires s’affichent correctement | Applicable uniquement pour certaines mises en oeuvre. Le rendu des activités basées sur des formulaires nécessite un code personnalisé similaire à at.js. |
| Les activités qui utilisent des redirections fonctionnent correctement | Les redirections sont prises en charge si la page source et la page de destination utilisent le SDK Web de Platform. Une redirection Target d’une page at.js vers une page SDK Web Platform ou de l’autre côté n’est pas prise en charge. |
| Les activités qui utilisent des offres distantes fonctionnent correctement | Non courant, vérifiez votre inventaire d’offres Target pour les offres distantes. |
| Le scintillement est atténué de manière appropriée | La gestion du scintillement est facultative, mais assurez-vous que toutes les tactiques de limitation que vous avez mises en place fonctionnent comme prévu pour des performances de page optimales et une expérience utilisateur optimale. |
| Les liens QA fonctionnent comme prévu | Si cela ne fonctionne pas, vérifiez que le fichier web.webPageDetails.URL correspond exactement à l’URL du navigateur. |
| Tous les types d’offres couramment utilisés sont rendus comme prévu. |  |

## Création de rapports

| Élément de validation | Notes |
|---|---|
| Les visiteurs sont attribués aux activités basées sur VEC | Il est préférable de valider le fonctionnement des rapports comme prévu pour les modifications de chargement de page et les modifications d’affichage SPA |
| Les visiteurs sont attribués aux activités d’après les formulaires | Selon l’approche de rendu utilisée, votre mise en oeuvre peut nécessiter du code personnalisé pour exécuter un événement `decisioning.propositionDisplay`. |
| Les objectifs de conversion standard sont correctement capturés. | S’applique à Target ou à Analytics comme source de création de rapports. |
| Les conversions de commande et les détails sont correctement capturés. | Vérification du rapport d’audit |
| Les conversions de suivi des clics sont correctement capturées. |  |
| Les objectifs de conversion personnalisés sont correctement capturés. | Par exemple, les objectifs de conversion migrés depuis at.js `trackEvent` ou `sendNotifications` qui sont généralement utilisés avec l’objectif &quot;visualisé une mbox&quot; |

## Audiences et scripts de profil

| Élément de validation | Notes |
|---|---|
| Les audiences utilisées dans les activités en direct sont compatibles avec le SDK Web de Platform. | Les audiences qui utilisent le composant &quot;Personnalisé&quot; (paramètre de mbox) doivent être mises à jour pour inclure des attributs XDM. |
| Tous les scripts de profil sont compatibles avec le SDK Web de Platform. | Tous les scripts de profil qui utilisent des paramètres de mbox doivent être mis à jour pour inclure des attributs XDM. |
| Retour des activités pour les audiences Target | Il est préférable d’effectuer une validation de bout en bout sur les audiences que vous modifiez pour les rendre compatibles avec le SDK Web Platform. |
| Les scripts de profil évaluent comme prévu | Affichage des traces Edge dans Debugger |

## Intégrations aux applications Adobe

| Élément de validation | Notes |
|---|---|
| Retour des activités pour les audiences Experience Cloud | Par exemple, un segment publié depuis Adobe Analytics |
| Retour des activités pour les audiences Experience Platform | S’applique uniquement si vous disposez d’une licence pour une application basée sur un Experience Platform telle que RTCDP |
| Retour des activités pour les audiences d’Audience Manager | Par exemple, un segment basé sur la consultation d’une page spécifique |
| Les données d’activité de Target s’affichent dans Analysis Workspace | S’applique aux activités qui utilisent Adobe Analytics comme source des rapports. |

## Intégrations à des applications tierces

| Élément de validation | Notes |
|---|---|
| Les données du jeton de réponse sont correctement transmises aux applications tierces. | Les approches d’intégration peuvent varier, mais une méthode courante consiste à utiliser des jetons de réponse Target pour transmettre des informations d’activité et d’expérience à d’autres outils d’analyse tels que les Google Analytics. |
| Les informations provenant de tiers sont transmises en tant que données XDM ou de profil. | Toutes les informations pertinentes provenant de tiers doivent être transmises dans des appels `sendEvent` à Target |

Après avoir effectué les étapes de validation ci-dessus, vous pouvez vous assurer que l’implémentation du SDK Web de Platform est prête à passer en production.

Ensuite, découvrez comment [&#x200B; résoudre les problèmes liés à une mise en oeuvre de Target à l’aide du SDK Web Platform &#x200B;](debugging.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
