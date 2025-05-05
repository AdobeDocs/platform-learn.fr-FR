---
title: 'Comparaison d’at.js 2.x avec le SDK Web : migration de Target d’at.js 2.x vers le SDK Web'
description: Découvrez les différences entre at.js 2.x et le SDK Web Platform, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 4%

---

# Comparaison d’at.js avec le SDK Web Platform

La bibliothèque Adobe Target at.js autonome diffère considérablement du SDK Web Platform. Les tableaux suivants constituent une référence pour vous aider à évaluer les zones de votre mise en oeuvre sur lesquelles vous devrez peut-être vous concentrer pendant le processus de migration.

Après avoir examiné les informations ci-dessous et évalué votre implémentation technique actuelle d’at.js, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par le SDK Web Platform ?
- Quelles fonctions at.js ont des équivalents du SDK Web Platform ?
- Application des paramètres Target avec le SDK Web Platform
- Différence entre le flux de données d’at.js et le SDK Web Platform

Si vous découvrez le SDK Web Platform, ne vous inquiétez pas : les éléments ci-dessous sont abordés plus en détail tout au long de ce tutoriel.

## Comparaison des fonctionnalités

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Mettre à jour le profil Target | Pris en charge | Pris en charge |
| Affichage Déclencheur pour SPA | Pris en charge | Pris en charge |
| Target Recommendations | Pris en charge | Pris en charge |
| Récupération des offres basées sur des formulaires | Pris en charge | Pris en charge |
| Suivi des événements | Pris en charge | Pris en charge |
| A4T : application d’une seule page | Pris en charge | Pris en charge |
| A4T : suivi des clics | Pris en charge | Pris en charge |
| A4T : journalisation côté client | Pris en charge | Pris en charge |
| A4T : journalisation côté serveur | Pris en charge | Pris en charge |
| Appliquer des offres | Pris en charge | Pris en charge |
| Rerendu de la vue dans SPA sans notifications | Pris en charge | Pris en charge |
| Applications hybrides | Pris en charge | Pris en charge |
| URL d’assurance qualité | Pris en charge | Pris en charge |
| Mbox 3rd Party ID | Pris en charge | Pris en charge |
| Attributs du client | Pris en charge | Pris en charge |
| Offres distantes | Pris en charge | Pris en charge |
| Offres de redirection | Pris en charge | Pris en charge. Cependant, une redirection d’une page avec le SDK Web Platform vers une page avec at.js (et dans la direction opposée) n’est pas prise en charge. |
| Prise de décision sur appareil | Pris en charge | Non pris en charge actuellement |
| Prérécupération des mbox | Pris en charge pour les portées personnalisées et SPA VEC | La prérécupération est le mode par défaut du SDK Web. |
| Événements personnalisés | Pris en charge | Non pris en charge. Voir la [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) pour connaître l’état actuel. |
| Jetons de réponse | Pris en charge | Pris en charge. Reportez-vous à la [documentation sur les jetons de réponse dédiés](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr) pour consulter des exemples de code et des différences entre at.js et le SDK Web Platform. |
| Fournisseurs de données | Pris en charge | Non pris en charge. Le code personnalisé peut être utilisé pour déclencher une commande du SDK Web Platform `sendEvent` après la récupération des données d’un autre fournisseur. |


## Légendes dignes de mention

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Réduction du scintillement | Le fragment de code de masquage préalable pour les implémentations asynchrones utilise un ID de style `at-body-style`. at.js recherche cet ID d’élément pour supprimer le style une fois qu’une réponse est reçue. | Le fragment de code de masquage préalable par défaut utilise un ID de style `alloy-prehiding`. Le SDK Web n’est pas compatible avec le fragment de code de masquage préalable d’at.js. Il doit donc être modifié dans le cadre du processus de migration. |
| Rendu automatique du contenu au chargement de la page | Contrôlé avec un paramètre global de Target. Activé lorsque `pageLoadEnabled` est défini sur `true`. | Spécifié dans la commande SDK Web Platform `sendEvent`. Activé en définissant l’option `renderDecisions` sur `true`. |
| Rendu manuel du contenu | Les fonctions `applyOffer()` et `applyOffers()` prennent uniquement en charge l’HTML des paramètres. | La commande `applyPropositions` prend en charge le paramétrage, le remplacement ou l’ajout d’un HTML pour une plus grande flexibilité. |
| Suivi des événements personnalisés | Pris en charge avec les fonctions `trackEvent()` et `sendNotifications()`. Ces fonctions sont spécifiques à Target et n’ont aucune incidence sur les mesures Adobe Analytics. | Toutes les données des appels `sendEvent` du SDK Web Platform sont transférées à Target. Les données supplémentaires nécessaires spécifiquement à Target doivent être incluses avec la commande `sendEvent` avec un eventType `decisioning.propositionDisplay` ou `decisioning.propositionInteract` pour s’assurer que les mesures Adobe Analytics ne sont pas affectées. |
| CNAME Target | Pris en charge. Il est distinct du CNAME utilisé pour Analytics et du service d’ID Experience Cloud. | Plus pertinent. Un seul CNAME peut être utilisé pour tous les appels du SDK Web Platform. |
| Débogage | Les paramètres d’URL `mboxDisable`, `mboxDebug` et `mboxTrace` peuvent être utilisés pour le débogage avec les outils de développement de votre navigateur.<br><br>L’Adobe Experience Platform Debugger est également un outil de débogage pris en charge. | Les paramètres d’URL `mboxDisable`, `mboxDebug` et `mboxTrace` ne sont pas pris en charge.<br><br>Vous pouvez activer le débogage du SDK Web en ajoutant le `alloy_debug=true` à votre chaîne de requête ou en exécutant `alloy("setDebug", { "enabled": true });` dans votre console de développement.<br><br>L’extension de navigateur Adobe Experience Platform Debugger peut être utilisée pour lancer une trace de périphérie pour le débogage.<br><br>Pour plus d’informations, consultez la documentation [Débogage du SDK Web Platform](debugging.md) . |
| Analytics for Target (A4T) | Utilise des valeurs SDID pour regrouper les appels Target et Analytics | Prise en charge native sans besoin de groupement |

>[!NOTE]
>
>La migration de Target vers le SDK Web Platform tout en conservant une mise en oeuvre Adobe Analytics d’AppMeasurement existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre implémentation d’at.js (et d’AppMeasurement.js) vers le SDK Web Platform une page à la fois. Si vous optez pour cette approche, il est préférable de définir les options [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#targetMigrationEnabled) sur `true` avec la commande `configure`.

## Fonctions d’at.js et équivalents du SDK Web Platform

De nombreuses fonctions at.js ont une approche équivalente à l’aide du SDK Web Platform décrit dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| fonction at.js 2.x | Équivalent SDK Web Platform |
| --- | --- | 
| `getOffer()` et `getOffers()` | Pour demander et [ générer automatiquement des expériences Target basées sur le VEC, utilisez la commande `sendEvent` et définissez l’option `renderDecisions` sur true.](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#automatically-rendering-content)<br><br>Pour demander des expériences basées sur des formulaires ou du contenu [rendu manuel](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#manually-rendering-content), spécifiez un tableau de `decisionScopes` (mbox) avec la commande `sendEvent`. |
| `applyOffer()` et `applyOffers()` | Utilisez la commande [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr#applypropositions) pour appliquer du contenu. Vous pouvez choisir de définir, remplacer ou ajouter un HTML à un sélecteur spécifique. |
| `triggerView()` | Le SDK Web Platform déclenche automatiquement un [changement d’affichage](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=fr#how-to-trigger-a-view-change-in-a-single-page-application) aux fins du SPA VEC si la propriété `web.webPageDetails.viewName` est définie sous l’option `xdm` de la commande `sendEvent`. |
| `trackEvent()` et `sendNotifications()` | Utilisez la commande `sendEvent` avec un ensemble [ `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=fr#how-to-track-events) spécifique : <br><br>`decisioning.propositionDisplay` signale le rendu d’une activité <br><br>`decisioning.propositionInteract` signale une interaction de l’utilisateur avec une activité, comme un clic de souris. |
| `targetGlobalSettings()` | Pas d&#39;équivalent direct. Pour plus d’informations, consultez la [comparaison des paramètres de Target](detailed-comparison.md) . |
| `targetPageParams()` et `targetPageParamsAll()` | Toutes les données transmises dans l’option `xdm` de la commande `sendEvent` sont mappées aux paramètres de mbox Target. Puisque les paramètres de mbox sont nommés à l’aide de la notation par points sérialisés, la migration vers le SDK Web Platform peut nécessiter la mise à jour des audiences et des activités existantes pour utiliser les nouveaux noms de paramètres de mbox. <br><br>Les données transmises dans le cadre de `data.__adobe.target` de la commande `sendEvent` sont mappées à [Profil Target et paramètres spécifiques à Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=fr#single-profile-update). |
| événements personnalisés at.js | Non pris en charge. Voir la [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) pour connaître l’état actuel. [Les jetons de réponse](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=fr) sont exposés en tant que partie de `propositions` dans la réponse de l’appel `sendEvent`. |

## Paramètres d’at.js et équivalents du SDK Web Platform

La bibliothèque at.js peut être configurée et téléchargée avec divers paramètres dans l’interface utilisateur de Target. Ces paramètres peuvent également être mis à jour avec la fonction [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) . Le tableau ci-dessous compare ces paramètres à ceux disponibles avec le SDK Web Platform.

| Paramètre at.js | Équivalent SDK Web Platform |
| --- | --- |
| `bodyHiddenStyle` | Définissez la [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#prehidingStyle) avec la commande `configure` |
| `bodyHidingEnabled` | Si un `prehidingStyle` est défini avec la commande `configure`, cette fonction est activée. Si aucun style n’est défini, le SDK Web Platform ne tente pas de masquer le contenu. |
| `clientCode` | Automatiquement configuré |
| `cookieDomain` | Non applicable |
| `crossDomain` | Définissez l’option `thirdPartyCookiesEnabled` sur `true` avec la commande `configure` pour activer les cookies propriétaires et tiers pour les cas d’utilisation inter-domaines. |
| `cspScriptNonce` et `cspStyleNonce` | Reportez-vous à la documentation pour [configurer une CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html?lang=fr) |
| `dataProviders` | Non pris en charge |
| `decisioningMethod` | Toutes les commandes du SDK Web Platform `sendEvent` utilisent la prise de décision côté serveur. La prise de décision hybride et sur appareil n’est pas prise en charge. |
| `defaultContentHiddenStyle` et `defaultContentVisibleStyle` | Applicable uniquement avec at.js 1.x. Tout comme at.js 2.x, toute atténuation du scintillement pour les expériences basées sur les formulaires peut être réalisée à l’aide de code personnalisé. |
| `deviceIdLifetime` | Non pris en charge. Si `targetMigrationEnabled` est défini sur `true` avec la commande `configure`, le cookie `mbox` est défini avec la durée de vie de l’appareil définie sur 2 ans. Cette valeur n’est pas configurable. |
| `enabled` | La fonctionnalité Target est activée ou désactivée avec la configuration du flux de données. |
| `globalMboxAutoCreate` | Définissez l’option `renderDecisions` sur `true` avec la commande `sendEvent` pour récupérer et effectuer automatiquement le rendu des expériences basées sur le VEC.<br><br>Demandez un `decisionScope` pour `__view__` si vous préférez effectuer le rendu manuel des expériences basées sur le VEC. |
| `imsOrgId` | Définissez le `orgId` avec la commande `configure` |
| `optinEnabled` et `optoutEnabled` | Reportez-vous aux [options de confidentialité](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=fr) du SDK Web Platform. L’option `defaultConsent` s’applique à toutes les solutions d’Adobe prises en charge par le SDK Web Platform. |
| `overrideMboxEdgeServer` et `overrideMboxEdgeServerTimeout` | Non applicable. Toutes les demandes du SDK Web Platform utilisent le réseau Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Définissez l’option `renderDecisions` sur `true` avec la commande `sendEvent` |
| `secureOnly` | Non pris en charge. Le SDK Web Platform définit tous les cookies avec les attributs `secure` et `sameSite="none"`. |
| `selectorsPollingTimeout` | Non pris en charge. Le SDK Web Platform utilise une valeur de 5 secondes. Si nécessaire, vous pouvez utiliser du code personnalisé pour effectuer le rendu manuel du contenu. |
| `serverDomain` | Utilisation du paramètre `edgeDomain` avec la commande `configure` |
| `telemetryEnabled` | Non applicable |
| `timeout` | Non pris en charge. Il est conseillé de vous assurer que tout code d’atténuation du scintillement comprend un délai d’expiration approprié. |
| `viewsEnabled` | Non pris en charge. Le contenu des vues Target est toujours récupéré lors du premier appel `sendEvent()` si `renderDecisions` est défini sur `true` ou si la variable `__view__` DecisionScope est incluse dans la requête. |
| `visitorApiTimeout` | Non applicable |


## Comparaison des diagrammes système

Les diagrammes suivants doivent vous aider à comprendre les différences de flux de données entre une implémentation Target à l’aide d’at.js et une implémentation à l’aide du SDK Web Platform.

### Diagramme du système at.js 2.x

![Comportement at.js 2.0 au chargement de la page](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Appeler | Détails |
| --- | --- |
| 1 | L’appel renvoie un ID d’Experience Cloud (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID de client. |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document (at.js peut également être chargé de manière asynchrone avec un extrait de code prémasqué facultatif implémenté sur la page). |
| 3 | La requête de chargement de page est effectuée, y compris tous les paramètres configurés, ECID, SDID et ID de client. |
| 4 | Les scripts de profil s’exécutent et sont introduits dans le magasin de profils. Le magasin demande des audiences qualifiées auprès de la bibliothèque d’audiences (par exemple, audiences partagées à partir d’Analytics, d’Audience Manager, etc.). Les attributs du client sont envoyés par lot dans le magasin de profils. |
| 5 | En fonction de l’URL, des paramètres de requête et des données de profil, Target décide quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues. |
| 6 | Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.<br><br> Le contenu ciblé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br><br>Le contenu ciblé pour les futures vues d’une application d’une seule page est mis en cache dans le navigateur. Il peut donc être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. |
| 7 | Données Analytics envoyées de la page aux serveurs de collecte de données. |
| 8 | Les données Target sont associées aux données Analytics par l’intermédiaire du SDID et sont traitées dans le stockage de rapports Analytics. Les données Analytics peuvent ensuite être visualisées à la fois dans Analytics et dans Target au moyen de rapports A4T. |

Reportez-vous au guide de développement pour plus d’informations sur la [mise en oeuvre de Target à l’aide d’at.js pour les applications d’une seule page](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagramme du système SDK Web Platform

![Diagramme de prise de décision Adobe Target Edge avec le SDK Web Platform](assets/target-platform-web-sdk.png)

| Appeler | Détails |
| --- | --- |
| 1 | L’appareil charge le SDK Web Platform. Le SDK Web Platform envoie une demande au réseau Edge avec des données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant client (facultatif). La page (ou les conteneurs) est prémasquée. |
| 2 | Le réseau Edge envoie la demande aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles sur le visiteur, telles que la géolocalisation et les noms conviviaux de l’appareil. |
| 3 | Le réseau Edge envoie la demande de personnalisation enrichie à Target Edge avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans le stockage des profils Target. Le stockage des profils récupère les segments de la bibliothèque d’audiences (par exemple, les segments partagés à partir d’Adobe Analytics, de Adobe Audience Manager et de Adobe Experience Platform). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, Target détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les futures vues prérécupérées. Target renvoie ensuite cette information au réseau Edge. |
| 6 | a. Le réseau Edge renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br><br>b. Le contenu personnalisé pour les vues affichées suite aux actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache pour un rendu instantané sans appels au serveur supplémentaires.<br><br>c. Le réseau Edge envoie l’identifiant visiteur et d’autres valeurs dans les cookies (par exemple, consentement, ID de session, identité, vérification de cookies, personnalisation, etc.). |
| 7 | Le réseau Edge transfère les détails d’Analytics for Target (A4T) (métadonnées d’activité, d’expérience et de conversion) vers le serveur Analytics Edge. |

Reportez-vous au guide de développement pour plus d’informations sur la [mise en oeuvre de Target à l’aide du SDK Web Platform pour les applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=fr).

Une fois que vous avez une bonne compréhension technique de votre mise en oeuvre actuelle de Target et des fonctionnalités que vous utilisez, l’étape suivante consiste à effectuer la [configuration initiale](initial-setup.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
