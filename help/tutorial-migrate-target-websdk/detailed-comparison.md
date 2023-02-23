---
title: Comparaison d’at.js 2.x avec le SDK Web | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez les différences entre at.js 2.x et le SDK Web Platform, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 8%

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

|  | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Mettre à jour le profil Target | Pris en charge | Pris en charge |
| Affichage Déclencheur pour SPA | Pris en charge | Pris en charge |
| Target Recommendations | Pris en charge | Pris en charge |
| Récupération des offres basées sur des formulaires | Pris en charge | Pris en charge |
| Suivi des événements | Pris en charge | Pris en charge |
| A4T : Application d’une seule page | Pris en charge | Pris en charge |
| A4T : Suivi des clics | Pris en charge | Pris en charge |
| A4T : Journalisation côté client | Pris en charge | Pris en charge |
| A4T : Journalisation côté serveur | Pris en charge | Pris en charge |
| Appliquer des offres | Pris en charge | Pris en charge |
| Rerendu de la vue dans SPA sans notifications | Pris en charge | Pris en charge |
| Applications hybrides | Pris en charge | Pris en charge |
| URL d’assurance qualité | Pris en charge | Pris en charge |
| Mbox 3rd Party ID | Pris en charge | Pris en charge |
| Attributs du client | Pris en charge | Pris en charge |
| Offres distantes | Pris en charge | Pris en charge |
| Offres de redirection | Pris en charge | Pris en charge. Cependant, une redirection d’une page avec le SDK Web Platform vers une page avec at.js (et dans la direction opposée) n’est pas prise en charge. |
| Prise de décision sur appareil | Pris en charge | Non pris en charge actuellement |
| Prérécupération des mbox | Pris en charge | Activé par défaut dans toutes les nouvelles migrations commencées après le 1er octobre 2022 |
| Événements personnalisés | Pris en charge | Non pris en charge. Voir [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) pour l’état actuel. |
| Jetons de réponse | Pris en charge | Pris en charge. Reportez-vous à la section [documentation sur les jetons de réponse dédiés](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) pour obtenir des exemples de code et des différences entre at.js et le SDK Web Platform |
| Fournisseurs de données  | Pris en charge | Non pris en charge. Le code personnalisé peut être utilisé pour déclencher un SDK Web Platform. `sendEvent` une fois les données récupérées auprès d’un autre fournisseur. |


## Légendes dignes de mention

|  | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Réduction du scintillement | Le fragment de code de masquage préalable pour les implémentations asynchrones utilise un ID de style de `at-body-style`. at.js recherche cet ID d’élément pour supprimer le style une fois qu’une réponse est reçue. | Le fragment de code de masquage préalable par défaut utilise un ID de style de `alloy-prehiding`. Le SDK Web n’est pas compatible avec le fragment de code de masquage préalable d’at.js. Il doit donc être modifié dans le cadre du processus de migration. |
| Rendu automatique du contenu au chargement de la page | Contrôlé avec un paramètre global de Target. Activé lorsque `pageLoadEnabled` est défini sur `true`. | Spécifié dans le SDK Web Platform `sendEvent` . Activé en définissant la variable `renderDecisions` option à `true`. |
| Rendu manuel du contenu | Le `applyOffer()` et `applyOffers()` les fonctions prennent uniquement en charge le paramètre de HTML | Le `applyPropositions` prend en charge le paramétrage, le remplacement ou l’ajout de HTMLS pour une plus grande flexibilité ; |
| Suivi des événements personnalisés | Pris en charge avec `trackEvent()` et `sendNotifications()` fonctions. Ces fonctions sont spécifiques à Target et n’ont aucune incidence sur les mesures Adobe Analytics. | Toutes les données du SDK Web Platform `sendEvent` Les appels sont transférés vers Target. Les données supplémentaires nécessaires spécifiquement à Target doivent être incluses dans la variable `sendEvent` avec un eventType de `decisioning.propositionDisplay` ou `decisioning.propositionInteract` pour garantir que les mesures Adobe Analytics ne sont pas affectées. |
| CNAME Target | Pris en charge. Il est distinct du CNAME utilisé pour Analytics et du service d’ID Experience Cloud. | Plus pertinent. Un seul CNAME peut être utilisé pour tous les appels du SDK Web Platform. |
| Débogage | Le `mboxDisable`, `mboxDebug`, et `mboxTrace` Les paramètres d’URL peuvent être utilisés pour le débogage avec les outils de développement de votre navigateur.<br><br>Le débogueur Adobe Experience Platform est également un outil de débogage pris en charge. | Le `mboxDisable`, `mboxDebug`, et `mboxTrace` Les paramètres d’URL ne sont pas pris en charge.<br><br>Vous pouvez activer le débogage du SDK Web en ajoutant la variable `alloy_debug=true` à votre chaîne de requête ou à votre exécution `alloy("setDebug", { "enabled": true });` dans votre console de développement.<br><br>L’extension de navigateur Adobe Experience Platform Debugger peut être utilisée pour lancer une trace de périphérie pour le débogage.<br><br>Reportez-vous à la section [débogage du SDK Web de Platform](debugging.md) pour plus d’informations. |
| Analytics for Target (A4T) | Utilise des valeurs SDID pour regrouper les appels Target et Analytics | Prise en charge native sans besoin de groupement |

>[!NOTE]
>
>La migration de Target vers le SDK Web Platform tout en conservant une mise en oeuvre Adobe Analytics AppMeasurement existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre mise en oeuvre d’at.js (et d’AppMeasurement.js) vers le SDK Web Platform une page à la fois. Si vous optez pour cette approche, il est préférable de définir la variable [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) options de `true` avec le `configure` .

## Fonctions d’at.js et équivalents du SDK Web Platform

De nombreuses fonctions at.js ont une approche équivalente à l’aide du SDK Web Platform décrit dans le tableau ci-dessous. Pour plus d’informations sur la variable [Fonctions d’at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), reportez-vous au Guide du développeur Adobe Target.

| fonction at.js 2.x | Équivalent SDK Web Platform |
| --- | --- | 
| `getOffer()` et `getOffers()` | Pour demander et [rendu automatique](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Expériences basées sur le VEC de Target, utilisez la variable `sendEvent` et définissez `renderDecisions` sur true.<br><br>Pour demander des expériences basées sur des formulaires ou à [rendu manuel](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) contenu, spécifiez un tableau de `decisionScopes` (mbox) avec la fonction `sendEvent` . |
| `applyOffer()` et `applyOffers()` | Utilisez la variable [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) pour appliquer du contenu. Vous pouvez choisir de définir, remplacer ou ajouter un HTML à un sélecteur spécifique. |
| `triggerView()` | Le SDK Web Platform déclenche automatiquement une [changement d’affichage](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) aux fins du SPA VEC, si la variable `web.webPageDetails.viewName` est définie sous la propriété `xdm` de l’option `sendEvent` . |
| `trackEvent()` et `sendNotifications()` | Utilisez la variable `sendEvent` avec une commande [spécifique `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) set :<br><br>`decisioning.propositionDisplay` signale le rendu d’une activité ;<br><br>`decisioning.propositionInteract` signale une interaction utilisateur avec une activité, comme un clic de souris. |
| `targetGlobalSettings()` | Pas d&#39;équivalent direct. Reportez-vous à la section [Comparaison des paramètres de Target](detailed-comparison.md) pour plus d’informations. |
| `targetPageParams()` et `targetPageParamsAll()` | Toutes les données transmises dans la variable `xdm` de l’option `sendEvent` est mappée aux paramètres de mbox Target. Puisque les paramètres de mbox sont nommés à l’aide de la notation par points sérialisés, la migration vers le SDK Web Platform peut nécessiter la mise à jour des audiences et des activités existantes pour utiliser les nouveaux noms de paramètres de mbox. <br><br>Données transmises dans le cadre de `data.__adobe.target` de `sendEvent` est mappée sur [Profil Target et paramètres spécifiques à Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| événements personnalisés at.js | Non pris en charge. Voir [feuille de route publique](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) pour l’état actuel. [Jetons de réponse](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) sont exposées dans le cadre de la fonction `propositions` dans la réponse de la variable `sendEvent` appelez . |

## Paramètres d’at.js et équivalents du SDK Web Platform

La bibliothèque at.js peut être configurée et téléchargée avec divers paramètres dans l’interface utilisateur de Target. Ces paramètres peuvent également être mis à jour avec la variable [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) fonction . Le tableau ci-dessous compare ces paramètres à ceux disponibles avec le SDK Web Platform.

| Paramètre at.js | Équivalent SDK Web Platform |
| --- | --- |
| `bodyHiddenStyle` | Définissez la variable [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) avec le `configure` command |
| `bodyHidingEnabled` | Si une `prehidingStyle` est défini avec la fonction `configure` , puis cette fonction est activée. Si aucun style n’est défini, le SDK Web Platform ne tente pas de masquer le contenu. |
| `clientCode` | Automatiquement configuré |
| `cookieDomain` | Non applicable |
| `crossDomain` | Définissez la variable `thirdPartyCookiesEnabled` option à `true` avec le `configure` pour activer les cookies propriétaires et tiers pour les cas d’utilisation inter-domaines |
| `cspScriptNonce` et `cspStyleNonce` | Reportez-vous à la documentation pour [configuration d’une CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Non pris en charge |
| `decisioningMethod` | SDK Web de toutes les plateformes `sendEvent` Les commandes utilisent la prise de décision côté serveur. La prise de décision hybride et sur appareil n’est pas prise en charge. |
| `defaultContentHiddenStyle` et `defaultContentVisibleStyle` | Applicable uniquement avec at.js 1.x. Tout comme at.js 2.x, toute atténuation du scintillement pour les expériences basées sur les formulaires peut être réalisée à l’aide de code personnalisé. |
| `deviceIdLifetime` | Non pris en charge. If `targetMigrationEnabled` est défini sur `true` avec le `configure` , la commande `mbox` est défini avec la durée de vie de l’appareil définie sur 2 ans. Cette valeur n’est pas configurable. |
| `enabled` | La fonctionnalité Target est activée ou désactivée avec la configuration du flux de données. |
| `globalMboxAutoCreate` | Définissez la variable `renderDecisions` option à `true` avec le `sendEvent` pour récupérer et générer automatiquement des expériences basées sur le compositeur d’expérience visuelle.<br><br>Demander une `decisionScope` pour `__view__` si vous préférez effectuer le rendu manuel d’expériences basées sur le compositeur d’expérience visuelle. |
| `imsOrgId` | Définissez la variable `orgId` avec le `configure` command |
| `optinEnabled` et `optoutEnabled` | Reportez-vous au SDK Web Platform [options de confidentialité](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). Le `defaultConsent` s’applique à toutes les solutions d’Adobe prises en charge par le SDK Web de Platform. |
| `overrideMboxEdgeServer` et `overrideMboxEdgeServerTimeout` | Non applicable. Toutes les demandes du SDK Web Platform utilisent le réseau Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Définissez la variable `renderDecisions` option à `true` avec le `sendEvent` command |
| `secureOnly` | Non pris en charge. Le SDK Web de Platform définit tous les cookies avec la variable `secure` et `sameSite="none"` attributs. |
| `selectorsPollingTimeout` | Non pris en charge. Le SDK Web Platform utilise une valeur de 5 secondes. Si nécessaire, vous pouvez utiliser du code personnalisé pour effectuer le rendu manuel du contenu. |
| `serverDomain` | Utilisez la variable `edgeDomain` avec le paramètre `configure` command |
| `telemetryEnabled` | Non applicable |
| `timeout` | Non pris en charge. Il est conseillé de vous assurer que tout code d’atténuation du scintillement comprend un délai d’expiration approprié. |
| `viewsEnabled` | Non pris en charge. Le contenu des vues Target est toujours récupéré lors de la première consultation `sendEvent()` call if `renderDecisions` est défini sur `true` ou le `__view__` décisionScope est inclus dans la requête. |
| `visitorApiTimeout` | Non applicable |


## Comparaison des diagrammes système

Les diagrammes suivants doivent vous aider à comprendre les différences de flux de données entre une implémentation Target à l’aide d’at.js et une implémentation à l’aide du SDK Web Platform.

### Diagramme du système at.js 2.x

![Comportement d’at.js 2.0 au chargement de la page](assets/target-at-js-2x-diagram.png){zoomable=&quot;yes&quot;}

| Appel | Détails |
| --- | --- |
| 1 | L’appel renvoie un ID d’Experience Cloud (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID de client. |
| 2 | La bibliothèque at.js se charge de manière synchrone et masque le corps du document (at.js peut également être chargé de manière asynchrone avec un extrait de code prémasqué facultatif implémenté sur la page). |
| 3 | La requête de chargement de page est effectuée, y compris tous les paramètres configurés, ECID, SDID et ID de client. |
| 4 | Les scripts de profil s’exécutent et sont introduits dans le magasin de profils. Le magasin demande des audiences qualifiées auprès de la bibliothèque d’audiences (par exemple, audiences partagées à partir d’Analytics, d’Audience Manager, etc.). Les attributs du client sont envoyés par lot dans le magasin de profils. |
| 5 | En fonction de l’URL, des paramètres de requête et des données de profil, Target décide quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues. |
| 6 | Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.<br><br>Le contenu ciblé sur la page actuelle est affiché aussi rapidement que possible, sans scintillement du contenu par défaut.<br><br>Le contenu ciblé pour les futures vues d’une application d’une seule page est mis en cache dans le navigateur. Il peut donc être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. (Voir le diagramme suivant pour connaître le comportement de triggerView()). |
| 7 | Données Analytics envoyées de la page aux serveurs de collecte de données. |
| 8 | Les données Target sont associées aux données Analytics par l’intermédiaire du SDID et sont traitées dans le magasin de rapports Analytics. Il est alors possible de consulter les données Analytics à la fois dans Analytics et Target, par l’intermédiaire des rapports d’A4T. |

Pour plus d’informations sur la manière de procéder, reportez-vous au guide de développement . [implémentation de Target à l’aide d’at.js pour les applications d’une seule page](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagramme système du SDK Web Platform

![Diagramme de prise de décision Adobe Target Edge avec le SDK Web Platform](assets/target-platform-web-sdk.png)

| Appel | Détails |
| --- | --- |
| 1 | Le périphérique charge le SDK Web Platform. Le SDK Web Platform envoie une demande au réseau Edge avec des données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant client (facultatif). La page (ou les conteneurs) est prémasquée. |
| 2 | Le réseau Edge envoie la demande aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles sur le visiteur, telles que la géolocalisation et les noms conviviaux de l’appareil. |
| 3 | Le réseau Edge envoie la demande de personnalisation enrichie à Target Edge avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans le stockage des profils Target. Le stockage des profils récupère les segments de la bibliothèque d’audiences (par exemple, les segments partagés à partir d’Adobe Analytics, de Adobe Audience Manager et de Adobe Experience Platform). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, Target détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les futures vues prérécupérées. Target renvoie ensuite cette information au réseau Edge. |
| 6 | a. Le réseau Edge renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br><br>b. Le contenu personnalisé pour les vues affichées suite aux actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache pour un rendu instantané sans appels au serveur supplémentaires.<br><br>c. Le réseau Edge envoie l’identifiant visiteur et d’autres valeurs dans les cookies (par exemple, consentement, ID de session, identité, vérification de cookies, personnalisation, etc.). |
| 7 | Le réseau Edge transfère les détails d’Analytics for Target (A4T) (métadonnées d’activité, d’expérience et de conversion) vers le serveur Analytics Edge. |

Pour plus d’informations sur la manière de procéder, reportez-vous au guide de développement . [mise en oeuvre de Target à l’aide du SDK Web Platform pour les applications d’une seule page](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Une fois que vous avez une bonne compréhension technique de votre mise en oeuvre actuelle de Target et des fonctionnalités que vous utilisez, l’étape suivante consiste à effectuer la [configuration initiale](initial-setup.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
