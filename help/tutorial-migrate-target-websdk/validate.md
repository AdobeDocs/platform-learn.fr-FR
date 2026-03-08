---
title: Validation des implémentations de Target avec Web SDK - Migration de Target d’at.js 2.x vers Web SDK
description: Découvrez comment valider les activités et déboguer une implémentation d’Adobe Target à l’aide de Adobe Experience Platform Web SDK.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Validation de l’implémentation de Platform Web SDK

Après la migration de votre implémentation Target d’at.js vers Platform Web SDK, il est important de vérifier que tout fonctionne correctement avant de publier les modifications apportées à votre site de production. Adobe recommande ce qui suit, qui est abordé en détail sur cette page :

* Effectuez une validation technique pour vous assurer que l’implémentation de base et les requêtes et réponses de Platform Web SDK sont correctes
* Assurez-vous que les activités Target sont diffusées et rendues correctement
* Vérifier le bon fonctionnement des rapports
* Consultez les audiences et les scripts de profil pour vous assurer qu’ils sont compatibles avec Platform Web SDK
* Assurez-vous que les intégrations à Adobe ou à des applications tierces fonctionnent correctement

Chaque implémentation de Target diffère selon l’architecture du site et les fonctionnalités utilisées. Vous pouvez utiliser les tableaux ci-dessous comme point de départ et ajouter des éléments uniques à votre implémentation. La [page de débogage](debugging.md) de ce tutoriel présente les outils que vous pouvez utiliser pour faciliter cette validation.

## Validation technique

| Élément de validation | Remarques |
|---|---|
| Le fragment de code de masquage préalable at.js ne figure plus sur la page | Platform Web SDK ne supprime pas automatiquement le style portant l’ID `at-body-style`. Si vous laissez cet ancien fragment de code sur la page, le contenu reste masqué jusqu’à ce que le délai d’expiration du fragment de code soit atteint. |
| La bibliothèque at.js n’est plus présente sur la page | Vérifiez qu’il n’existe aucun objet « adobe.target » dans la console des outils de développement de votre navigateur. L’inclusion de Platform Web SDK et d’at.js entraîne un comportement de rendu inattendu |
| Les paramètres attendus se trouvent dans les objets XDM et de données de la requête `sendEvent` | |
| Le catalogue de recommandations est mis à jour comme prévu si des requêtes de page sont utilisées pour le remplir | |
| Les paramètres de profil ont été transmis à Target. | Affichage des traces Edge dans le débogueur |
| Les paramètres mappés à XDM dans le mappeur de flux de données sont correctement transmis à Target | Validation à l’aide de la fonction Edge Trace du débogueur et/ou d’Assurance |
| Le contenu cible est renvoyé dans les réponses `sendEvent` applicables. | Attendu lorsque `renderDecisions` option est définie sur `true` ou que les portées sont demandées et que l’utilisateur est qualifié pour une activité Target particulière |
| Un événement `decisioning.propositionDisplay` se déclenche après le rendu des activités basées sur le VEC | Les activités rendues automatiquement et à la demande doivent avoir des appels d’événement distincts |
| Un événement `decisioning.propositionDisplay` se déclenche après le rendu des activités basées sur des formulaires | Applicable uniquement pour certaines implémentations. Nécessite du code personnalisé pour exécuter cet appel. |
| Un événement `decisioning.propositionDisplay` se déclenche lorsqu’une offre est appliquée à une modification d’affichage SPA | Applicable uniquement aux implémentations de SPA |
| Un événement `decisioning.propositionDisplay` ne se déclenche PAS lorsqu’un composant SPA effectue un nouveau rendu pour une vue donnée | Applicable uniquement aux implémentations de SPA |
| Un événement `decisioning.propsitionInteract` se déclenche après une conversion d’activité | Les conversions « A cliqué sur un élément » et personnalisées migrées depuis at.js `trackEvent` ou `sendNotifications` doivent avoir des appels d’événement distincts |
| Les jetons de réponse sont renvoyés dans la réponse `sendEvent` et possèdent les valeurs attendues | Les jetons de réponse doivent fonctionner normalement avec Web SDK. |
| Les ECID sont cohérents sur toutes les pages avec Web SDK et at.js | S’applique aux migrations page par page. Les offres de redirection ne devraient pas fonctionner dans ces types de migration |


## Diffusion et rendu des activités

| Élément de validation | Remarques |
|---|---|
| Les activités basées sur le VEC s’affichent correctement au chargement de la page | Il est préférable de valider les modifications du code personnalisé et les modifications de base, telles que la réorganisation des éléments ou le remplacement de texte |
| Les activités basées sur le compositeur d’expérience visuelle s’affichent correctement lors des modifications de la vue SPA | Applicable uniquement aux implémentations de SPA |
| Les activités basées sur des formulaires s’affichent correctement | Applicable uniquement pour certaines implémentations. Le rendu des activités basées sur des formulaires nécessite un code personnalisé similaire à at.js. |
| Les activités qui utilisent les redirections fonctionnent correctement | Les redirections sont prises en charge si la page source et la page de destination utilisent toutes deux Platform Web SDK. Une redirection Target d’une page at.js vers une page Web SDK Platform ou inversement n’est pas prise en charge. |
| Les activités qui utilisent des offres distantes fonctionnent correctement | Peu fréquent, vérifiez l’inventaire des offres Target pour les offres distantes |
| Le scintillement est correctement atténué | La gestion du scintillement est facultative, mais assurez-vous que toutes les tactiques de réduction que vous avez mises en place fonctionnent comme prévu pour offrir des performances de page et une expérience utilisateur optimales |
| Les liens d’assurance qualité fonctionnent comme prévu. | Si cela ne fonctionne pas, vérifiez que le fichier web.webPageDetails.URL correspond exactement à l’URL dans le navigateur |
| Tous les types d’offres couramment utilisés sont rendus comme prévu |  |

## Création de rapports

| Élément de validation | Remarques |
|---|---|
| Les visiteurs sont attribués aux activités basées sur le compositeur d’expérience visuelle | Il est préférable de valider les travaux de création de rapports comme prévu pour les modifications de chargement de page et les modifications d’affichage de SPA |
| Les visiteurs sont affectés à des activités basées sur des formulaires | Selon l’approche de rendu utilisée, votre implémentation peut nécessiter du code personnalisé pour exécuter un événement `decisioning.propositionDisplay` |
| Les objectifs de conversion standard sont correctement capturés | S’applique à Target ou à Analytics en tant que source de création de rapports |
| Les conversions de commandes et les détails sont correctement capturés | Vérifier le rapport d’audit |
| Les conversions de suivi des clics sont correctement capturées |  |
| Les objectifs de conversion personnalisés sont correctement capturés | Par exemple, les objectifs de conversion migrés depuis at.js `trackEvent` ou `sendNotifications` qui sont généralement utilisés avec l’objectif « afficher une mbox » |

## Audiences et scripts de profil

| Élément de validation | Remarques |
|---|---|
| Les audiences utilisées dans les activités dynamiques sont compatibles avec Platform Web SDK | Les audiences qui utilisent le composant « Personnalisé » (paramètre mbox) doivent être mises à jour pour inclure les attributs XDM |
| Tous les scripts de profil sont compatibles avec Platform Web SDK | Tous les scripts de profil qui utilisent des paramètres de mbox doivent être mis à jour pour inclure des attributs XDM |
| Retour des activités pour les audiences cibles | Il est préférable d’effectuer une validation de bout en bout sur les audiences que vous modifiez pour les rendre compatibles avec Platform Web SDK |
| Les scripts de profil sont évalués comme prévu. | Affichage des traces Edge dans le débogueur |

## Intégrations avec les applications Adobe

| Élément de validation | Remarques |
|---|---|
| Retour des activités pour les audiences Experience Cloud | Par exemple, un segment publié depuis Adobe Analytics |
| Retour des activités pour les audiences Experience Platform | S’applique uniquement si vous disposez d’une licence pour une application Experience Platform telle que RTCDP |
| Retour des activités pour les audiences Audience Manager | Par exemple, un segment basé sur la visite d’une page spécifique |
| Affichage des données d’activité de Target dans Analysis Workspace | S’applique aux activités qui utilisent Adobe Analytics comme source de création de rapports |

## Intégrations à des applications tierces

| Élément de validation | Remarques |
|---|---|
| Les données du jeton de réponse sont correctement transmises aux applications tierces. | Les approches d’intégration peuvent varier, mais une méthode courante consiste à utiliser des jetons de réponse Target pour transmettre des informations d’activité et d’expérience à d’autres outils d’analyse tels que Google Analytics |
| Les informations provenant de tiers sont transmises sous la forme de données XDM ou de profil | Toutes les informations pertinentes provenant de tiers doivent être transmises lors des appels `sendEvent` à Target |

Après avoir effectué les étapes de validation ci-dessus, vous pouvez être sûr que l’implémentation de Platform Web SDK est prête à passer en production.

Ensuite, découvrez comment [dépanner une implémentation de Target à l’aide de Platform Web SDK](debugging.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
