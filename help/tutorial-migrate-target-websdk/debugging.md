---
title: Débogage - Migration de Target d’at.js 2.x vers Web SDK
description: Découvrez comment déboguer une implémentation d’Adobe Target à l’aide de Adobe Experience Platform Web SDK. Les rubriques incluent les options de débogage, les extensions de navigateur et les différences entre at.js et Platform Web SDK.
exl-id: 20699551-a708-469a-8980-67586db82787
source-git-commit: d70d5df8b11c8500dbe4764b08e2627893f436f0
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 2%

---

# Déboguer Target avec Platform Web SDK

la vérification des activités Target et le débogage de Web SDK pour résoudre les problèmes d’implémentation, de diffusion de contenu ou de qualification des audiences ; Cette page du guide de migration explique les différences entre le débogage avec at.js et Platform Web SDK.

Le tableau ci-dessous résume les fonctionnalités et la prise en charge des approches de test et de débogage.

| Fonctionnalité ou outil | Prise en charge d’at.js | Prise en charge de Platform Web SDK |
| --- | --- | --- |
| URL d’AQ d’activité | Oui | Oui |
| Paramètre d’URL `mboxDisable` | Oui | Reportez-vous aux informations ci-dessous pour [désactiver la fonctionnalité Target](#disable-target-functionality) |
| Paramètre d’URL `mboxDebug` | Oui | Utilisez `alloy_debug` paramètre pour obtenir des informations de débogage similaires |
| Paramètre d’URL `mboxTrace` | Oui | Utilisation de l’extension de navigateur Experience Platform Debugger |
| Extension Adobe Experience Platform Debugger | Oui | Oui |
| Paramètre d’URL `alloy_debug` | Non applicable | Oui |
| Assurance d’Adobe Experience Platform Assurance | Non applicable | Oui |

## Extension de navigateur Adobe Experience Platform Debugger

L’extension Adobe Experience Platform Debugger pour Chrome et Firefox examine vos pages web et vous aide à valider vos implémentations Adobe Experience Cloud.

Vous pouvez exécuter Platform Debugger sur n’importe quelle page web et l’extension a accès aux données publiques. Pour accéder aux données non publiques à l’aide de l’extension, telles que les informations de Target Trace, vous devez vous authentifier auprès d’Experience Cloud via le lien **[!UICONTROL Se connecter]**.

### Obtention et installation d’Adobe Experience Platform Debugger

Adobe Experience Platform Debugger peut être installé dans Google Chrome. Suivez le lien approprié ci-dessous pour installer l’extension :

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Après avoir installé l’extension Chrome ou le module complémentaire Firefox, une icône (![](assets/start-icon.jpg)) est ajoutée à la barre d’extension. Sélectionnez cette icône pour ouvrir l’extension.

Reportez-vous au guide dédié pour plus d’informations sur l’extension [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) et sur la manière de déboguer toutes les applications web Adobe.

## Prévisualiser les activités Target avec les URL d’assurance qualité

at.js et Platform Web SDK vous permettent de prévisualiser les activités de Target à l’aide des URL d’assurance qualité de Target. Les deux méthodes d’implémentation prennent en charge les mêmes fonctionnalités d’assurance qualité.

Les URL d’assurance qualité de Target fonctionnent en demandant à at.js ou à Platform Web SDK d’écrire un cookie spécifique dans votre navigateur nommé `at_qa_mode`. Ce cookie est utilisé pour forcer la qualification pour une activité et une expérience spécifiques.

>[!CAUTION]
>
>La fonctionnalité du mode QA de Target est prise en charge par la version 2.13.0 ou ultérieure de Platform Web SDK. Le mode QA de Target est activé en fonction de la valeur `xdm.web.webPageDetails.URL` transmise dans l’appel `sendEvent`. Toute modification de cette valeur, telle que la mise en minuscules de tous les caractères, peut empêcher le mode AQ de Target de fonctionner correctement.

Reportez-vous au guide dédié pour plus d’informations sur l’[AQ de l’activité Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## Implémentation de Debug Target

Le tableau ci-dessous décrit les différences entre les tactiques de débogage d’at.js et de Platform Web SDK :

| Fonction at.js | Équivalent de Platform Web SDK |
| --- | --- |
| **Mbox désactivée** - Désactivez la récupération et le rendu de Target pour vérifier si la page est rompue sans interactions avec Target<br><br>Chargez la page avec le paramètre d’URL : `mboxDisable=true` | Pas d&#39;équivalent direct. Vous pouvez bloquer toutes les requêtes de Platform Web SDK à l’aide des outils de développement de votre navigateur. |
| **Débogage de mbox** - consigne chaque action at.js dans la console du navigateur pour résoudre les problèmes de rendu<br><br>Charger la page avec le paramètre d’URL : `mboxDebug=true` | **Alloy Debug** : consigne les actions détaillées du SDK, y compris, mais sans s’y limiter, les actions de personnalisation de Target.<br><br>Charger la page avec le paramètre d’URL : `alloy_debug=true` <br /><br />Ou exécuter `alloy("setDebug", { "enabled": true });` dans votre Developer Console |
| **Target Trace** - Avec un jeton mbox trace généré dans l’interface utilisateur de Target, un objet de trace avec les détails qui ont participé au processus de prise de décision est disponible sous `window.___target_trace` objet .<br><br>Charger la page avec le paramètre URL : `mboxTrace=window&authorization={TOKEN}` | Utilisez l’extension Adobe Experience Platform debugger ou Platform Assurance. |

>[!NOTE]
>
>Toutes les fonctionnalités de débogage d’at.js répertoriées ci-dessus sont disponibles avec des fonctionnalités améliorées dans Adobe Experience Platform Debugger.

### Désactivation de la fonctionnalité Target

Actuellement, Platform Web SDK ne dispose pas d’une fonctionnalité permettant de supprimer de manière sélective les réponses de Target. Cependant, il est possible de supprimer les requêtes de SDK Web Platform à l’aide des outils de développement de votre navigateur, de diverses extensions de navigateur ou d’applications tierces. Par exemple, pour bloquer Platform Web SDK avec Google Chrome :

1. Faites un clic droit n’importe où sur la page et sélectionnez **Inspecter**
1. Sélectionnez l’onglet **Réseau**
1. Filtrez par le `//ee//` de chaîne pour afficher uniquement les appels SDK Web Platform
1. Recharger la page
1. Cliquez avec le bouton droit sur l’une des requêtes réseau filtrées et sélectionnez **Bloquer le domaine de la requête**
1. Rechargez la page et notez que la demande réseau est bloquée
1. Lorsque vous avez terminé le débogage, cliquez avec le bouton droit sur la demande réseau bloquée et sélectionnez **Débloquer**, ou fermez le panneau Outils de développement

### Afficher la journalisation du débogage

La journalisation du débogage pour at.js à l’aide du paramètre d’URL `mboxDebug=true` affiche des informations détaillées sur chaque requête, réponse et tentative de Target pour effectuer le rendu du contenu sur la page. La journalisation du débogage de Platform Web SDK est similaire à l’aide du paramètre d’URL `alloy_debug=true`.

| Informations enregistrées | at.js `mboxDebug=true`) | SDK Web de Platform (`alloy_debug=true`) |
| --- | --- | --- |
| Préfixe de journalisation pour le filtrage | `AT:` | `[alloy]` |
| Détails de la requête de chargement de page | Oui | Oui |
| Détails de la mbox ou de la demande d’étendue | Oui | Oui |
| Statut de la requête | Oui | Oui |
| Détails de la réponse | Oui | Oui |
| Statut du rendu | Succès et erreurs | Erreurs uniquement |
| Détails du rendu | Oui | Oui |

>[!NOTE]
>
>Les journaux de débogage pour at.js et Platform Web SDK fournissent le même niveau de détail, à l’exception notable que Web SDK ne signale que les erreurs de rendu dues à des sélecteurs non valides. La journalisation du débogage ne confirme pas actuellement que le rendu a réussi.

### Afficher les traces de Target

Les traces de Target fournissent des informations détaillées sur les qualifications des activités et le profil Target du visiteur. Comme les traces de Target contiennent des informations qui ne sont pas disponibles publiquement, leur affichage nécessite un jeton d’autorisation ou une authentification dans la fenêtre de l’extension de navigateur Adobe Experience Platform Debugger.

| Méthode de Target Trace | at.js | SDK Web de Platform |
| --- | --- | --- |
| Paramètre d’URL `mboxTrace` | Oui | Non |
| Extension de navigateur Adobe Experience Platform Debugger | Oui | Oui |
| Assurance d’Adobe Experience Platform Assurance | Non | Oui |


Pour afficher les traces de Platform Web SDK Target avec Adobe Experience Platform Debugger, procédez comme suit :

1. Accédez à une page de votre site sur laquelle Target est implémenté avec Platform Web SDK
1. Ouvrez l’extension Adobe Experience Platform Debugger en sélectionnant l’icône (![](assets/start-icon.jpg)) dans la barre de navigation de votre navigateur
1. Sélectionnez le lien **[!UICONTROL Se connecter]**
1. Authentification à l’aide de votre identifiant Adobe Experience Cloud
1. Sélectionnez l’onglet **[!UICONTROL Journaux]** à gauche
1. Sélectionnez l’onglet **[!UICONTROL Edge]** en haut
1. Attribuez éventuellement un nom à votre session de débogage et cliquez sur le bouton **[!UICONTROL Se connecter]**
1. Rechargez la page et le journal doit être renseigné avec des informations détaillées sur les interactions du réseau Edge
1. Concentrez-vous sur les entrées de journal commençant par « Target Traces » dans la description, puis sélectionnez **[!UICONTROL Afficher]** pour afficher les détails de Target Trace

![Comment afficher les traces de Target avec Adobe Experience Platform Debugger &#x200B;](assets/target-trace-debugger.png){zoomable="yes"}

Après avoir sélectionné **[!UICONTROL Afficher]**, un recouvrement s’affiche, vous permettant d’afficher les informations suivantes relatives à la requête :

- Activités correspondantes
- Activités sans correspondance
- Détails de la demande
- Instantané de profil

Pour plus d’informations sur les traces de Target, consultez le guide dédié sur le [débogage de la diffusion de contenu de Target](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html).

### Résolution des problèmes liés à Assurance

Les informations de Target Trace sont visibles dans l’extension de navigateur Adobe Experience Platform Debugger et dans l’application Assurance (anciennement appelée Projet Griffon). Pour afficher les traces de Target dans Assurance, procédez comme suit :

1. Ouvrez l’extension de navigateur Adobe Experience Platform Debugger et connectez une session de débogage à distance comme indiqué ci-dessus
1. Sélectionnez le lien avec le nom de votre session au-dessus du journal de débogage
1. Platform Assurance charge et affiche la journalisation détaillée de toutes les applications Adobe configurées dans le flux de données pour votre implémentation
1. Filtrer le journal par `adobe.target`
1. Sélectionnez une entrée de journal avec le type `com.adobe.target.trace`
1. Développez les détails de la payload et affichez les informations sous `context > targetTrace`

![Comment afficher les traces de Target avec Assurance &#x200B;](assets/target-trace-assurance.png){zoomable="yes"}

## Examiner la requête et la réponse du réseau

La payload et la réponse de requête des appels de `sendEvent` de Platform Web SDK diffèrent d’at.js. La description ci-dessous doit vous aider à comprendre la structure de la requête et de la réponse lors de l’examen des appels réseau avec les outils de développement de votre navigateur.

### Payload de requête de contenu

![Éléments spécifiques à Target de la payload de Platform Web SDK](assets/target-payload.png){zoomable="yes"}

- Les paramètres de profil, d’entité et autres que mbox sont transmis dans le tableau d’événements sous `data.__adobe.target`
- Les portées de décision se trouvent dans le tableau d’événements sous `query.personalization.decisionScopes`
- Les données XDM mappées aux paramètres de mbox en aval se trouvent dans le tableau d’événements sous `xdm`

### Corps de réponse du contenu

![Cibler des éléments spécifiques du corps de réponse de Platform Web SDK](assets/target-response.png){zoomable="yes"}

- Platform Web SDK renvoie des actions pour toutes les applications Adobe sous l’objet `handle`
- L’action `personalization:decisions` signifie une réponse de Target ou d’Offer Decisioning
- Les propositions cibles sont présentées sous la forme d’un tableau, chacune avec un identifiant de proposition unique précédé de `AT:`
- La portée de décision et les détails de l’activité se trouvent dans le tableau des propositions
- Les détails de l’offre se trouvent dans le tableau `items` sous `data`
- Les jetons de réponse se trouvent dans le tableau `items` sous `meta`

### Payload de l’événement de proposition

![Exemple d’événement de proposition cible](assets/target-proposition-event.png){zoomable="yes"}

- Les événements SDK spécifiques à Target sont `decisioning.propositionDisplay` pour une impression ou `decisioning.propositionInteract` pour une interaction, telle qu’un clic
- Les détails de l’événement de proposition se trouvent dans le tableau d’événements sous `xdm._experience.decisioning`
- L’identifiant de proposition de l’événement d’affichage ou d’interaction doit correspondre à l’identifiant de proposition du contenu renvoyé par Target


Félicitations, vous avez atteint la fin du tutoriel. Bonne chance pour la migration de votre implémentation Adobe Target vers Web SDK !

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
