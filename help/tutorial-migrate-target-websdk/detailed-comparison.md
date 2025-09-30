---
title: Comparaison d’at.js 2.x à Web SDK - Migration de Target d’at.js 2.x à Web SDK
description: Découvrez les différences entre at.js 2.x et Platform Web SDK, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 7d3c1728925e322f9313cf71f081500e0c0bac0b
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 4%

---

# Comparaison d’at.js avec Platform Web SDK

La bibliothèque Adobe Target at.js autonome diffère considérablement de Platform Web SDK. Les tableaux suivants servent de référence pour vous aider à évaluer les aspects de votre implémentation sur lesquels vous devrez peut-être vous concentrer au cours du processus de migration.

Après avoir consulté les informations ci-dessous et évalué votre implémentation technique actuelle d’at.js, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par Platform Web SDK ?
- Quelles fonctions at.js possèdent des équivalents Platform Web SDK ?
- Application des paramètres de Target avec Platform Web SDK
- Différences entre le flux de données d’at.js et de Platform Web SDK

Si vous découvrez Platform Web SDK, ne vous inquiétez pas : les éléments ci-dessous sont abordés plus en détail tout au long de ce tutoriel.

## Comparaison des fonctionnalités

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Mettre à jour le profil Target | Pris en charge | Pris en charge |
| Déclencher la vue pour les SPA | Pris en charge | Pris en charge |
| Recommandations relatives à Target | Pris en charge | Pris en charge |
| Récupérer des offres basées sur des formulaires | Pris en charge | Pris en charge |
| Suivi des événements | Pris en charge | Pris en charge |
| A4T : application monopage (SPA) | Pris en charge | Pris en charge |
| A4T : suivi des clics | Pris en charge | Pris en charge |
| A4T : journalisation côté client | Pris en charge | Pris en charge |
| A4T : journalisation côté serveur | Pris en charge | Pris en charge |
| Application d’offres | Pris en charge | Pris en charge |
| Rendu de la vue dans la SPA sans notifications | Pris en charge | Pris en charge |
| Applications hybrides | Pris en charge | Pris en charge |
| URL de l’assurance qualité | Pris en charge | Pris en charge |
| ID de mbox tiers | Pris en charge | Pris en charge |
| Attributs du client | Pris en charge | Pris en charge |
| Offres distantes | Pris en charge | Partiellement pris en charge. Les offres distantes dynamiques ne sont pas prises en charge. |
| Offres de redirection | Pris en charge | Pris en charge. Cependant, la redirection d’une page avec Platform Web SDK vers une page avec at.js (et dans le sens opposé) n’est pas prise en charge. |
| Prise De Décision Sur L’Appareil | Pris en charge | Actuellement non pris en charge |
| Prérécupération des mbox | Pris en charge pour les portées personnalisées et le VEC SPA | La prérécupération est le mode par défaut de Web SDK |
| Événements personnalisés | Pris en charge | Non pris en charge. Consultez la [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}) pour connaître le statut actuel. |
| Jetons de réponse | Pris en charge | Pris en charge. Reportez-vous à la documentation [jetons de réponse dédiés](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr) pour obtenir des exemples de code et des différences entre at.js et Platform Web SDK |
| Fournisseurs de données | Pris en charge | Non pris en charge. Le code personnalisé peut être utilisé pour déclencher une commande de `sendEvent` de Platform Web SDK après la récupération des données d’un autre fournisseur. |


## Légendes dignes de mention

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Atténuation du scintillement | Le fragment de code de masquage préalable pour les implémentations asynchrones utilise un identifiant de style `at-body-style`. at.js recherche cet ID d’élément pour supprimer le style une fois qu’une réponse est reçue. | Le fragment de code de masquage préalable par défaut utilise un ID de style de `alloy-prehiding`. Web SDK n’est pas compatible avec le fragment de code de masquage préalable at.js. Il doit donc être modifié dans le cadre du processus de migration. |
| Rendu automatique du contenu au chargement de la page | Contrôlé avec un paramètre Target global. Activé lorsque la `pageLoadEnabled` est définie sur `true`. | Spécifiée dans la commande Platform Web SDK `sendEvent`. Activé en définissant l’option `renderDecisions` sur `true`. |
| Rendu manuel du contenu | Les fonctions `applyOffer()` et `applyOffers()` prennent uniquement en charge la définition d’HTML | La commande `applyPropositions` prend en charge la définition, le remplacement ou l’ajout d’HTML pour plus de flexibilité |
| Suivi des événements personnalisés | Pris en charge avec les fonctions `trackEvent()` et `sendNotifications()`. Ces fonctions sont spécifiques à Target et n’ont aucune incidence sur les mesures Adobe Analytics. | Toutes les données des appels de `sendEvent` de Platform Web SDK sont transférées vers Target. Les données supplémentaires nécessaires spécifiquement pour Target doivent être incluses avec la commande `sendEvent` avec un eventType de `decisioning.propositionDisplay` ou `decisioning.propositionInteract` pour s’assurer que les mesures Adobe Analytics ne sont pas affectées. |
| CNAME cible | Pris en charge. Ce nom est distinct du CNAME utilisé pour Analytics et le service Experience Cloud ID. | Plus pertinent. Un seul CNAME peut être utilisé pour tous les appels de Platform Web SDK. |
| Débogage | Les paramètres d’URL `mboxDisable`, `mboxDebug` et `mboxTrace` peuvent être utilisés à des fins de débogage à l’aide des outils de développement de votre navigateur.<br><br>Adobe Experience Platform Debugger est également un outil de débogage pris en charge. | Les paramètres `mboxDisable`, `mboxDebug` et URL `mboxTrace` ne sont pas pris en charge.<br><br>Vous pouvez activer le débogage Web SDK en ajoutant le `alloy_debug=true` à votre chaîne de requête ou en exécutant `alloy("setDebug", { "enabled": true });` dans votre Developer Console.<br><br>L’extension de navigateur Adobe Experience Platform Debugger peut être utilisée pour lancer une trace Edge à des fins de débogage.<br><br>Pour plus d’informations, consultez la documentation [débogage de Platform Web SDK](debugging.md). |
| Analytics for Target (A4T) | Utilise des valeurs SDID pour regrouper les appels Target et Analytics. | Pris en charge de manière native sans avoir à effectuer de groupement |

>[!NOTE]
>
>La migration de Target vers Platform Web SDK tout en conservant une implémentation AppMeasurement Adobe Analytics existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre implémentation at.js (et AppMeasurement.js) vers Platform Web SDK une page à la fois. Si vous optez pour cette approche, il est préférable de définir les options [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#targetMigrationEnabled) à `true` avec la commande `configure`.

## Fonctions at.js et équivalents de Platform Web SDK

De nombreuses fonctions at.js adoptent une approche équivalente à l’aide de Platform Web SDK, comme indiqué dans le tableau ci-dessous. Pour plus d’informations sur les fonctions [at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| Fonction at.js 2.x | Équivalent de Platform Web SDK |
| --- | --- | 
| `getOffer()` et `getOffers()` | Pour demander et [générer automatiquement](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#automatically-rendering-content) des expériences basées sur le compositeur d’expérience visuelle de Target, utilisez la commande `sendEvent` et définissez l’option `renderDecisions` sur true.<br><br>Pour demander des expériences basées sur des formulaires ou pour [effectuer manuellement le rendu](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#manually-rendering-content) du contenu, spécifiez un tableau d’`decisionScopes` (mbox) avec la commande `sendEvent`. |
| `applyOffer()` et `applyOffers()` | Utilisez la commande [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#applypropositions) pour appliquer le contenu. Vous pouvez choisir de définir, de remplacer ou d’ajouter HTML à un sélecteur spécifique. |
| `triggerView()` | Platform Web SDK déclenche automatiquement une [modification d’affichage](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=fr#how-to-trigger-a-view-change-in-a-single-page-application) aux fins du VEC SPA si la propriété `web.webPageDetails.viewName` est définie sous l’option `xdm` de la commande `sendEvent`. |
| `trackEvent()` et `sendNotifications()` | Utilisez la commande `sendEvent` avec un jeu de [`eventType` spécifique à ](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=fr#how-to-track-events) : <br><br>`decisioning.propositionDisplay` signale le rendu d’une activité<br><br>`decisioning.propositionInteract` signale l’interaction d’un utilisateur avec une activité, comme un clic de souris. |
| `targetGlobalSettings()` | Pas d&#39;équivalent direct. Pour plus d’informations, reportez-vous à la [comparaison des paramètres Target](detailed-comparison.md). |
| `targetPageParams()` et `targetPageParamsAll()` | Toutes les données transmises dans l’option `xdm` de la commande `sendEvent` sont mappées aux paramètres de mbox cible. Étant donné que les paramètres de mbox sont nommés à l’aide de la notation par points sérialisée, la migration vers Platform Web SDK peut nécessiter la mise à jour des audiences et activités existantes pour utiliser les nouveaux noms de paramètres de mbox. <br><br>Les données transmises dans le cadre de la `data.__adobe.target` de la commande `sendEvent` sont mappées aux [paramètres spécifiques au profil Target et à Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=fr#single-profile-update). |
| événements personnalisés at.js | Non pris en charge. Consultez la [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}) pour connaître le statut actuel. Les [jetons de réponse](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=fr) sont exposés dans le cadre du `propositions` dans la réponse de l’appel `sendEvent`. |

## Paramètres at.js et équivalents de Platform Web SDK

La bibliothèque at.js peut être configurée et téléchargée avec divers paramètres dans l’interface utilisateur de Target. Ces paramètres peuvent également être mis à jour avec la fonction [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/). Le tableau ci-dessous compare ces paramètres à ceux disponibles avec Platform Web SDK.

| Paramètre at.js | Équivalent de Platform Web SDK |
| --- | --- |
| `bodyHiddenStyle` | Définissez la [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#prehidingStyle) avec la commande `configure` |
| `bodyHidingEnabled` | Si une `prehidingStyle` est définie avec la commande `configure`, cette fonctionnalité est activée. Si aucun style n’est défini, Platform Web SDK ne tente pas de masquer le contenu. |
| `clientCode` | Configuré automatiquement |
| `cookieDomain` | Non applicable |
| `crossDomain` | Définissez l’option `thirdPartyCookiesEnabled` sur `true` avec la commande `configure` pour activer les cookies propriétaires et tiers pour les cas d’utilisation interdomaines |
| `cspScriptNonce` et `cspStyleNonce` | Reportez-vous à la documentation relative à la [configuration d’un fichier CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html?lang=fr) |
| `dataProviders` | Non pris en charge |
| `decisioningMethod` | Toutes les commandes `sendEvent` de Platform Web SDK utilisent la prise de décision côté serveur. La prise de décision hybride et sur l’appareil n’est pas prise en charge. |
| `defaultContentHiddenStyle` et `defaultContentVisibleStyle` | Applicable uniquement avec at.js 1.x. Tout comme pour at.js 2.x, le code personnalisé permet de réduire le scintillement des expériences basées sur des formulaires. |
| `deviceIdLifetime` | Non pris en charge. Si `targetMigrationEnabled` est défini sur `true` avec la commande `configure`, le cookie `mbox` est défini avec la durée de vie de l’appareil définie sur 2 ans. Cette valeur n’est pas configurable. |
| `enabled` | La fonctionnalité Target est activée ou désactivée avec la configuration du flux de données |
| `globalMboxAutoCreate` | Définissez l’option `renderDecisions` sur `true` avec la commande `sendEvent` pour récupérer et générer automatiquement des expériences basées sur VEC.<br><br>Demandez un `decisionScope` pour `__view__` si vous préférez effectuer manuellement le rendu des expériences basées sur le compositeur d’expérience visuelle. |
| `imsOrgId` | Définissez la `orgId` avec la commande `configure` |
| `optinEnabled` et `optoutEnabled` | Reportez-vous à la section SDK web Platform [options de confidentialité](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=fr). L’option `defaultConsent` s’applique à toutes les solutions Adobe prises en charge par Platform Web SDK. |
| `overrideMboxEdgeServer` et `overrideMboxEdgeServerTimeout` | Sans objet. Toutes les requêtes Platform Web SDK utilisent le réseau Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Définissez l’option `renderDecisions` sur `true` avec la commande `sendEvent` |
| `secureOnly` | Non pris en charge. Platform Web SDK définit tous les cookies avec les attributs `secure` et `sameSite="none"`. |
| `selectorsPollingTimeout` | Non pris en charge. Platform Web SDK utilise une valeur de 5 secondes. Le code personnalisé peut être utilisé pour effectuer manuellement le rendu du contenu, si nécessaire. |
| `serverDomain` | Utilisation du paramètre `edgeDomain` avec la commande `configure` |
| `telemetryEnabled` | Non applicable |
| `timeout` | Non pris en charge. Nous vous conseillons de vous assurer que tout code de réduction du scintillement inclut un délai d’expiration approprié. |
| `viewsEnabled` | Non pris en charge. Le contenu des vues Target est toujours récupéré lors du premier appel de `sendEvent()` si `renderDecisions` est défini sur `true` ou si la portée de décision `__view__` est incluse dans la requête. |
| `visitorApiTimeout` | Non applicable |


## Comparaison des diagrammes système

Les diagrammes ci-dessous doivent vous aider à comprendre les différences de flux de données entre une implémentation de Target utilisant at.js et une implémentation utilisant le SDK web de Platform.

### Diagramme système d’at.js 2.x

![comportement d’at.js 2.0 au chargement de la page](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Appel | Détails |
| --- | --- |
| 1 | L’appel renvoie l’Experience Cloud ID (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID client. |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document (at.js peut également être chargé de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page). |
| 3 | La requête de chargement de page est effectuée, y compris tous les paramètres configurés, l’ECID, le SDID et l’ID client. |
| 4 | Les scripts de profil s’exécutent et se chargent dans le magasin de profils. Le magasin demande des audiences qualifiées à la bibliothèque d’audiences (par exemple, les audiences partagées à partir d’Analytics, d’Audience Manager, etc.). Les attributs du client sont envoyés au magasin de profils dans un traitement par lots. |
| 5 | En fonction de l’URL, des paramètres de requête et des données de profil, Target décide des activités et expériences à renvoyer au visiteur pour la page actuelle et les vues futures. |
| 6 | Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.<br><br>Le contenu ciblé sur la page active est révélé le plus rapidement possible sans scintillement du contenu par défaut.<br><br>Le contenu ciblé pour les vues futures d’une application d’une seule page est mis en cache dans le navigateur, afin qu’il puisse être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. |
| 7 | Données Analytics envoyées de la page aux serveurs de collecte de données. |
| 8 | Les données cibles sont associées aux données Analytics via le SDID et traitées dans le stockage de rapports Analytics. Les données Analytics peuvent ensuite être affichées dans Analytics et Target au moyen de rapports A4T. |

Pour plus d’informations sur la [implémentation de Target à l’aide d’at.js pour les applications d’une seule page](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/), consultez le guide de développement .

### Diagramme système de Platform Web SDK

![Diagramme d’Adobe Target Edge Decisioning avec Platform Web SDK](assets/target-platform-web-sdk.png)

| Appel | Détails |
| --- | --- |
| 1 | L’appareil charge Platform Web SDK. Platform Web SDK envoie une requête au réseau Edge avec les données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant client (facultatif). La page (ou les conteneurs) est prémasquée. |
| 2 | Le réseau Edge envoie la requête aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles du visiteur, telles que la géolocalisation et les noms conviviaux pour les appareils. |
| 3 | Le réseau Edge envoie la demande de personnalisation enrichie au Edge de Target avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont intégrés au stockage du profil cible. Le stockage des profils récupère les segments de la bibliothèque d’audiences (par exemple, les segments partagés depuis Adobe Analytics, Adobe Audience Manager et Adobe Experience Platform). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, Target détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les vues prérécupérées futures. Target le renvoie ensuite au réseau Edge. |
| 6 | a. Edge Network renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est révélé le plus rapidement possible sans scintillement du contenu par défaut.<br><br>b. Le contenu personnalisé des vues affichées à la suite d’actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache pour un rendu instantané sans appels au serveur supplémentaires.<br><br>c. Le réseau Edge envoie l’identifiant visiteur et d’autres valeurs dans les cookies (par exemple, consentement, ID de session, identité, vérification des cookies, personnalisation, etc.). |
| 7 | Le réseau Edge transfère les détails d’Analytics for Target (A4T) (métadonnées d’activité, d’expérience et de conversion) vers Analytics Edge. |

Pour plus d’informations sur la [implémentation de Target à l’aide de Platform Web SDK pour les applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=fr), consultez le guide de développement .

Une fois que vous avez une bonne compréhension technique de votre implémentation Target actuelle et des fonctionnalités que vous utilisez, l’étape suivante consiste à effectuer la [configuration initiale](initial-setup.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
