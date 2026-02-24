---
title: Surveiller les événements dans Slack
description: Découvrez comment recevoir des notifications Experience Platform dans Slack en intégrant un proxy webhook Adobe App Builder.
feature: Monitoring
role: Developer, Admin
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
thumbnail: KT-20339.jpeg
source-git-commit: 268df348b1151394acde869ba4814b658a27e8ff
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 0%

---


# Surveillance des événements Experience Platform dans Slack

Découvrez comment recevoir des notifications Experience Platform dans Slack en intégrant un proxy webhook Adobe App Builder. Les ingénieurs et administrateurs de données peuvent souhaiter recevoir des notifications proactives dans Slack de Adobe Experience Platform pour surveiller l’intégrité de leurs implémentations de Platform. Ce tutoriel décrit l’architecture et les étapes d’implémentation pour connecter Adobe I/O Events à Slack à l’aide d’Adobe App Builder.


>[!VIDEO](https://video.tv.adobe.com/v/3480183?learn=on)

## Pourquoi utiliser un proxy webhook ?

La connexion directe de Adobe I/O Events à un Webhook entrant Slack n’est pas possible en raison d’une incohérence du protocole dans le processus de vérification.

* **Le défi** : lorsque vous enregistrez un webhook avec Adobe I/O Events, Adobe envoie une requête « Challenge » (un `GET` ou un `POST`) à votre point d’entrée. Votre point d’entrée doit traiter ce défi avec succès et renvoyer la valeur spécifique pour confirmer la propriété.

* **La limite** : les Webhooks entrants Slack sont conçus uniquement pour ingérer des payloads JSON pour la messagerie. Ils n’ont pas de logique pour reconnaître ou répondre à la négociation de défi de vérification d’Adobe.

* **La solution** : déployez un proxy webhook intermédiaire à l’aide d’Adobe App Builder. Ce proxy se trouve entre Adobe et Slack pour :
   1. Interceptez la requête d’Adobe et répondez au défi de vérification.
   1. Formatez la payload dans un message compatible avec Slack et transférez-le vers Slack.

* **Méthode de diffusion** : actions d’exécution.  Les actions d’exécution sont fournies avec Adobe App Builder. Lors de l’utilisation d’une action d’exécution (action non web) comme gestionnaire d’événements, Adobe I/O Events gère automatiquement les réponses de vérification des signatures et de vérification des défis. Les actions d’exécution sont l’approche recommandée, car elles nécessitent moins de code et offrent une sécurité intégrée.

## Aperçu de l’architecture

### Qu’est-ce que Adobe Developer Console ?

Adobe Developer Console est le portail central de gestion de vos projets, API et informations d’identification Adobe. C’est là que vous créez votre projet, configurez l’authentification et enregistrez vos Webhooks.

### Qu’est-ce qu’App Builder ?

Adobe App Builder est un framework complet qui permet aux développeurs d’entreprise de créer des applications natives dans le cloud.

* **Mise en service** : App Builder n’est pas activé par défaut ; il doit être mis en service pour votre organisation en tant que fonctionnalité. Assurez-vous que votre organisation dispose des droits **[!DNL App Builder]**.

* **Modèle de projet** : les projets App Builder sont créés spécifiquement à l’aide du modèle **[!UICONTROL App Builder]** dans le [!DNL Developer Console] ([!UICONTROL Projet à partir d’un modèle] > [!UICONTROL App Builder]). Le modèle configure automatiquement les espaces de travail et les environnements d’exécution nécessaires.

* **Guide de prise en main d’App Builder** : consultez la documentation [pour configurer et créer votre premier projet à partir du modèle](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}.

### Qu’est-ce que Adobe I/O Runtime ?

Adobe I/O Runtime est la plateforme sans serveur qui alimente App Builder. Il permet aux développeurs de déployer du code (Fonctions en tant que service) qui s’exécute en réponse aux requêtes HTTP sans gérer l’infrastructure du serveur.

Dans cette implémentation, nous utilisons une **Action**. Une action est une fonction sans état (écrite dans Node.js) qui s’exécute sur le Adobe I/O Runtime. Notre action sert de point d’entrée HTTP public auquel Adobe I/O Events s’adresse.

Pour plus d’informations, consultez la documentation de [Adobe I/O Runtime](https://developer.adobe.com/runtime/){target=_blank}.

## Guide de mise en œuvre

### Conditions préalables

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* **Accès à Adobe Developer Console** : vous devez avoir accès à un rôle d’administrateur système ou de [développeur](../admin/add-developers.md) au sein d’une organisation pour laquelle App Builder est activé.

  >[!TIP]
  > Pour vérifier l’approvisionnement d’App Builder, connectez-vous à [Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}, vérifiez que vous vous trouvez dans l’organisation souhaitée, sélectionnez **[!UICONTROL Créer un projet à partir d’un modèle]**, puis vérifiez que le modèle App Builder est disponible. Si ce n’est pas le cas, consultez la section FAQ d’App Builder « [ Comment obtenir App Builder ](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank} »


* **Node.js et npm** : ce projet nécessite Node.js, qui inclut NPM (Node Package Manager). NPM est utilisé pour installer l’interface de ligne de commande Adobe et gérer les dépendances de projet.

   * [Télécharger Node.js (version LTS recommandée)](https://nodejs.org/){target=_blank}
   * [Guide de prise en main de npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank} - Guide expliquant comment vérifier votre installation.

* **`aio CLI`** : installé via votre terminal : `npm install -g @adobe/aio-cli`
* **Configuration de l’application Slack** : une application Slack doit être configurée dans votre espace de travail avec un **Webhook entrant** activé.

   * [Créer une application Slack](https://api.slack.com/apps){target=_blank}
   * [Guide des Webhooks entrants Slack ](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank} - Suivez ce guide pour créer votre application et générer l’URL du Webhook (commence par `https://hooks.slack.com/`...).

### Étape 1 : créer un projet dans Adobe Developer Console

Tout d’abord, créez un projet avec le modèle App Builder dans Adobe Developer Console :

1. Se connecter à [Adobe Developer Console](https://developer.adobe.com/console)
1. Sélectionnez **[!UICONTROL Créer un projet à partir d’un modèle]**
1. Sélection du modèle App Builder
1. Saisissez un titre de projet, par exemple `Slack webhook integration`
1. Sélectionnez **[!UICONTROL Enregistrer]**

### Étape 2 : initialiser l’environnement d’exécution

Exécutez les commandes suivantes dans votre terminal pour créer la structure du projet :

#### Connexion à `aio`

```
aio login
```

#### Initialiser un nouveau projet App Builder

```
aio app init slack-webhook-proxy
```

1. Sélectionnez votre organisation et appuyez sur **Entrée**
1. Sélectionnez le projet que vous avez créé à l’étape précédente (par exemple, `Slack webhook integration`) et appuyez sur **Entrée**
1. Sélectionnez l’option **[!UICONTROL Seuls les modèles pris en charge par mon organisation]**
1. Ignorer la section d’exemple en appuyant sur **Entrée**
1. Lorsque vous y êtes invité, assurez-vous que les composants suivants sont sélectionnés (un cercle doit être renseigné) et appuyez sur **Entrée** :
   1. **[!UICONTROL Actions : déployer des actions d’exécution]**
   1. **[!UICONTROL Événements : publication sur Adobe I/O Events]**
   1. **[!UICONTROL Web Assets : déploiement sur les ressources statiques hébergées]**
1. Avec vos flèches « Haut » et « Bas », naviguez dans la liste entrante, choisissez **[!UICONTROL Adobe Experience Platform : profil client en temps réel]** puis appuyez sur **Entrée**
1. Les actions **[!UICONTROL génériques]** sont générées automatiquement
1. Choisissez le **[!UICONTROL HTML pur/JS]** pour l’interface utilisateur et appuyez sur **Entrée**
1. Conservez **[!UICONTROL générique]** comme exemple d’action pour montrer comment accéder à un nom d’API externe et appuyez sur **Entrée**
1. Conservez la **[!UICONTROL publish-events]** comme nom d’action d’exemple pour créer des messages au format d’événements cloud et appuyez sur **Entrée**

L&#39;initialisation de votre application doit être terminée.

#### Accédez au répertoire du projet

```
cd slack-webhook-proxy
```

#### Ajouter l’action web

```
aio app add action
```

1. Choisissez **[!UICONTROL Uniquement les modèles pris en charge par mon organisation]** puis appuyez sur **Entrée**.
2. Voir l’action **[!UICONTROL publish-events]** dans le tableau présenté ; appuyer sur **Space** pour sélectionner l’action. Si le cercle en regard du nom est plein comme illustré dans le tutoriel vidéo, appuyez sur **Entrée**
3. Nommez l’action `webhook-proxy`

### Étape 3 : Code De L’Action Proxy

Dans un IDE ou un éditeur de texte, créez/modifiez le fichier `actions/webhook-proxy/index.js` avec le code suivant. Cette implémentation transfère les événements vers Slack. La vérification des signatures et la gestion des défis sont automatiques lors de l’utilisation de l’enregistrement de l’action d’exécution.

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Étape 4 : configurer l’action

La configuration de l’action dans `app.config.yaml` est essentielle. Utilisez web : non pour créer une action non web qui peut être enregistrée en tant qu’action d’exécution dans le Developer Console.

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### Pourquoi `web: no?`

Lorsque vous utilisez une action non web et que vous l’enregistrez via l’option « Action d’exécution » dans le Developer Console, Adobe I/O Events effectue automatiquement les opérations suivantes :

* Gère la vérification de défi (`GET` et `POST`)
* Vérifie les signatures numériques avant d’appeler votre action
* Enchaîne une action de validation de signature devant votre action

Cela signifie que votre code ne doit gérer que la logique commerciale (transfert vers Slack).

### Étape 5 : Variables D’Environnement

Pour gérer les informations d’identification en toute sécurité, nous utilisons des variables d’environnement. Créez/modifiez le fichier `.env` à la racine de votre projet pour ajouter votre URL de webhook Slack. Veillez à afficher les fichiers masqués sur votre système si vous ne voyez pas le fichier `.env` :

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Étape 6 : déployer

Une fois les variables d’environnement définies, déployez l’action. Assurez-vous d’être à la racine de votre projet, à savoir `slack-webhook-proxy`, lors de l’exécution de cette commande dans le terminal.

```
aio app deploy
```

Votre action est déployée sur Adobe I/O Runtime et peut être enregistrée dans Developer Console.

### Étape 7 : Enregistrement final (Adobe Developer Console)

Maintenant que votre action est déployée, enregistrez-la en tant que destination des événements Adobe.

1. Accédez à [Adobe Developer Console](https://developer.adobe.com/console){target=_blank} et ouvrez votre projet App Builder.
1. Choisissez votre **[!UICONTROL Workspace]**
1. Sélectionnez **[!UICONTROL Ajouter un service]** puis **[!UICONTROL Événement]**.
1. Sélectionnez **[!UICONTROL Adobe Experience Platform]** comme produit.
1. Sélectionnez **[!UICONTROL Notifications Platform]** comme type d’événement.
1. Sélectionnez les événements spécifiques (ou tous) dont vous souhaitez être averti dans Slack et sélectionnez **[!UICONTROL Suivant]**.
1. Sélectionnez ou [créez vos informations d’identification OAuth](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}.
1. Configurez **[!UICONTROL Détails de l’enregistrement de l’événement]** :
   1. **[!UICONTROL Nom de l’enregistrement]** : attribuez un nom explicite à votre enregistrement.
   1. **[!UICONTROL Description de l’enregistrement]** : assurez-vous que cela est explicite afin que les autres contributeurs ou contributrices puissent savoir ce que cela fait.
   1. Sélectionnez **[!UICONTROL Suivant]**
   1. **[!UICONTROL Méthode de diffusion]** : sélectionnez **[!UICONTROL Action d’exécution]** (et non « Webhook »).
   1. **[!UICONTROL Action d’exécution]** : sélectionnez `webhook-proxy` dans la liste déroulante (actualisez la page si vous ne la voyez pas).
1. Sélectionnez **[!UICONTROL Enregistrer les événements configurés]**.


### Étape 8 : valider avec un exemple d’événement

Vous pouvez tester l’ensemble du flux de bout en bout en cliquant sur le bouton « Envoyer un exemple d’événement » en regard de tout événement configuré.

L’exemple d’événement est envoyé sur le canal que vous avez configuré lors de la création de votre application Slack et du webhook. Vous devriez voir un élément similaire à ce qui suit :

![Exemple d’événement de surveillance dans Slack](../assets/slack-monitor.png)

Félicitations, vous avez intégré Slack aux événements Experience Platform.

### Problèmes courants

Voici quelques problèmes que vous pouvez rencontrer lors de la configuration du proxy et quelques moyens potentiels de les résoudre.

* **Impossible d’afficher les organisations IMS** : si vous ne voyez pas votre liste d’organisations IMS lors de l’exécution, `aio app init` comme suit. Exécutez `aio logout` dans votre terminal, déconnectez-vous d’Experience Cloud sur votre navigateur web par défaut, puis `aio login`.
* **L’action n’apparaît pas dans la liste déroulante** : assurez-vous que `web: no` est défini dans `app.config.yaml`. Seules les actions non web s’affichent dans le menu déroulant Action d’exécution . Actualisez la page Developer Console après le déploiement.
* **Échec de la vérification des signatures** : si vous le voyez dans les journaux d’activation, cela signifie que le programme de validation intégré d’Adobe a rejeté la demande. Cela ne devrait pas se produire pour les événements Adobe légitimes. Vérifiez que l’enregistrement de l’événement est correctement configuré.
* **Slack ne recevant pas de messages** : vérifiez que `SLACK_WEBHOOK_URL` est correctement défini dans votre fichier `.env` et que le Webhook entrant est activé pour l’application Slack.
* **Délai d’action** : les actions d’exécution ont un délai d’expiration de 60 secondes. Si votre action prend plus de temps, pensez à utiliser l’approche de journalisation .