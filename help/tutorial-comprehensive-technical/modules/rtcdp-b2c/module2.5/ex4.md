---
title: Collecte de données et transfert côté serveur en temps réel - Création et configuration d’une fonction cloud Google
description: Création et configuration d’une fonction Google Cloud
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---

# 2.5.4 Création et configuration d’une fonction cloud Google

## 2.5.4.1 Création de la fonction Cloud Google

Accédez à [https://console.cloud.google.com/](https://console.cloud.google.com/). Accédez à **Cloud Functions**.

![GCP](./images/gcp1.png)

Vous verrez alors ceci. Cliquez sur **CREATE FUNCTION**.

![GCP](./images/gcp2.png)

Vous verrez alors ceci.

![GCP](./images/gcp6.png)

Effectuez les choix suivants :

- **Nom de fonction** : `--demoProfileLdap---event-forwarding`
- **Région** : sélectionnez une région
- **Type de déclencheur** : sélectionnez **HTTP**
- **Authentification** : sélectionnez **Autoriser les appels non authentifiés**

Vous devriez maintenant avoir ceci. Cliquez sur **SAVE**.

![GCP](./images/gcp7.png)

Cliquez sur **NEXT**.

![GCP](./images/gcp8.png)

Vous verrez alors :

![GCP](./images/gcp9.png)

Effectuez les choix suivants :

- **Runtime** : sélectionnez **Node.js 16** (ou plus récent)
- **Point d’entrée** : saisissez **helloAEP**

Cliquez sur **ENABLE API** pour activer l’ **API Cloud Build**. Vous verrez alors une nouvelle fenêtre. Dans cette nouvelle fenêtre, cliquez de nouveau sur **ENABLE**.

![GCP](./images/gcp10.png)

Vous verrez alors ceci. Cliquez sur **Activer**.

![GCP](./images/gcp11.png)

Une fois que l’ **API Cloud Build** a été activée, vous verrez ceci.

![GCP](./images/gcp12.png)

Revenez à la **fonction cloud**.
Dans votre éditeur en ligne de fonction Cloud, assurez-vous que vous y avez le code suivant :

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

Cliquez ensuite sur **DEPLOY**.

![GCP](./images/gcp13.png)

Vous verrez alors ceci. Votre fonction cloud est en cours de création. Cela peut prendre quelques minutes.

![GCP](./images/gcp14.png)

Une fois votre fonction créée et en cours d’exécution, vous verrez ceci. Cliquez sur le nom de la fonction pour l’ouvrir.

![GCP](./images/gcp15.png)

Vous verrez alors ceci. Accédez à **TRIGGER**. Vous verrez ensuite l’ **URL de déclenchement** qui est ce que vous utiliserez pour définir le point de terminaison dans Launch côté serveur.

![GCP](./images/gcp16.png)

Copiez l&#39;URL du déclencheur, qui ressemble à ceci : **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**.

Dans les étapes suivantes, vous allez configurer le serveur de collecte de données Adobe Experience Platform pour diffuser des informations spécifiques sur les **pages vues** vers votre fonction cloud Google. Au lieu de transférer uniquement la charge utile complète en l’état, vous enverrez uniquement des éléments tels que **ECID**, **horodatage** et **Nom de page** à votre fonction cloud Google.

Voici un exemple de payload que vous devez analyser pour filtrer les variables mentionnées ci-dessus :

```json
{
  "events": [
    {
      "xdm": {
        "eventType": "web.webpagedetails.pageViews",
        "web": {
          "webPageDetails": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC",
            "name": "vangeluw-OCUC",
            "viewName": "vangeluw-OCUC",
            "pageViews": {
              "value": 1
            }
          },
          "webReferrer": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/equipment"
          }
        },
        "device": {
          "screenHeight": 1080,
          "screenWidth": 1920,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1920,
            "viewportHeight": 451
          }
        },
        "placeContext": {
          "localTime": "2022-02-23T06:51:07.140+01:00",
          "localTimezoneOffset": -60
        },
        "timestamp": "2022-02-23T05:51:07.140Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy/reactor",
          "version": "2.8.0+2.9.0",
          "environment": "browser"
        },
        "_experienceplatform": {
          "identification": {
            "core": {
              "ecid": "08346969856929444850590365495949561249"
            }
          },
          "demoEnvironment": {
            "brandName": "vangeluw-OCUC"
          },
          "interactionDetails": {
            "core": {
              "channel": "web"
            }
          }
        }
      },
      "query": {
        "personalization": {
          "schemas": [
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
          ],
          "decisionScopes": [
            "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0YzA1MjM4MmUxYjY1MDUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTRiZjA5ZGM0MTkwZWJiYSJ9",
            "__view__"
          ]
        }
      }
    }
  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  },
  "meta": {
    "state": {
      "domain": "adobedemo.com",
      "cookiesEnabled": true,
      "entries": [
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_identity",
          "value": "CiYwODM0Njk2OTg1NjkyOTQ0NDg1MDU5MDM2NTQ5NTk0OTU2MTI0OVIPCPn66KfyLxgBKgRJUkwx8AH5-uin8i8="
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent_check",
          "value": "1"
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent",
          "value": "general=in"
        }
      ]
    }
  }
}
```

Il s’agit des champs qui contiennent les informations qui doivent être analysées :

- ECID : **events.xdm._experienceplatform.identification.core.ecid**
- timestamp : **timestamp**
- Nom de page : **events.xdm.web.webPageDetails.name**

Allons maintenant sur le serveur de collecte de données Adobe Experience Platform pour configurer les éléments de données afin de rendre cela possible.

## 2.5.4.2 Mise à jour de la propriété Event Forwarting : Data Elements

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) et à **Transfert d’événement**. Recherchez la propriété Event Forwarding et cliquez dessus pour l’ouvrir.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Dans le menu de gauche, accédez à **Data Elements**. Cliquez sur **Ajouter un élément de données**.

![Adobe Experience Platform Data Collection SSF](./images/de1gcp.png)

Un nouvel élément de données à configurer s’affiche.

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

Effectuez la sélection suivante :

- En tant que **Nom**, saisissez **customerECID**.
- En tant que **Extension**, sélectionnez **Core**.
- En tant que **Type d’élément de données**, sélectionnez **Chemin**.
- En tant que **Chemin**, saisissez `arc.event.xdm.--aepTenantId--.identification.core.ecid`. En entrant ce chemin, vous allez filtrer le champ **ecid** de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

>[!NOTE]
>
>Dans les chemins ci-dessus et au-dessous, une référence est faite à **arc**. **arc** signifie Adobe Resource Context et **arc** signifie toujours l’objet disponible le plus élevé disponible dans le contexte côté serveur. Des enrichissements et des transformations peuvent être ajoutés à cet objet **arc** à l’aide des fonctions du serveur de collecte de données Adobe Experience Platform.
>
>Dans les chemins ci-dessus et ci-dessous, une référence est faite à **event**. **event** correspond à un événement unique et le serveur de collecte de données Adobe Experience Platform évalue toujours chaque événement individuellement. Parfois, vous pouvez voir une référence à **events** dans la payload envoyée par le SDK Web côté client, mais dans le serveur de collecte de données Adobe Experience Platform, chaque événement est évalué individuellement.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/gcdpde1.png)

Cliquez sur **Ajouter un élément de données**.

![Adobe Experience Platform Data Collection SSF](./images/addde.png)

Un nouvel élément de données à configurer s’affiche.

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

Effectuez la sélection suivante :

- En tant que **Name**, saisissez **eventTimestamp**.
- En tant que **Extension**, sélectionnez **Core**.
- En tant que **Type d’élément de données**, sélectionnez **Chemin**.
- En tant que **Chemin**, saisissez **arc.event.xdm.timestamp**. En entrant ce chemin, vous allez filtrer le champ **horodatage** de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/gcdpde2.png)

Cliquez sur **Ajouter un élément de données**.

![Adobe Experience Platform Data Collection SSF](./images/addde.png)

Un nouvel élément de données à configurer s’affiche.

![Adobe Experience Platform Data Collection SSF](./images/de2gcp.png)

Effectuez la sélection suivante :

- En tant que **Nom**, saisissez **pageName**.
- En tant que **Extension**, sélectionnez **Core**.
- En tant que **Type d’élément de données**, sélectionnez **Chemin**.
- En tant que **Chemin**, saisissez **arc.event.xdm.web.webPageDetails.name**. En entrant ce chemin, vous allez filtrer le champ **name** de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/gcdpde3.png)

Ces éléments de données sont maintenant créés :

![Adobe Experience Platform Data Collection SSF](./images/de3gcp.png)

## 2.5.4.3 Mise à jour de la propriété Event Forwarting : mise à jour d’une règle

Dans le menu de gauche, accédez à **Règles**. Dans l’exercice précédent, vous avez créé la règle **Toutes les pages**. Cliquez sur cette règle pour l’ouvrir.

![Adobe Experience Platform Data Collection SSF](./images/rl1gcp.png)

Vous ferez alors ceci. Cliquez sur l’icône **+** sous **Actions** pour ajouter une nouvelle action.

![Adobe Experience Platform Data Collection SSF](./images/rl2gcp.png)

Vous verrez alors ceci.

![Adobe Experience Platform Data Collection SSF](./images/rl4gcp.png)

Effectuez la sélection suivante :

- Sélectionnez l’ **extension** : **Adobe Cloud Connector**.
- Sélectionnez le **Type d’action** : **Lancer l’appel de récupération**.

Cela devrait vous donner ce **Nom** : **Connecteur Adobe Cloud - Lancer l’appel de récupération**. Vous devriez maintenant voir ceci :

![Adobe Experience Platform Data Collection SSF](./images/rl5gcp.png)

Configurez ensuite les éléments suivants :

- Modifiez le protocole de requête de GET en **POST**
- Saisissez l’URL de la fonction cloud Google que vous avez créée lors de l’une des étapes précédentes qui ressemble à ceci : **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**

Vous devriez maintenant avoir ceci. Ensuite, accédez à **Body**.

![Adobe Experience Platform Data Collection SSF](./images/rl6gcp.png)

Vous verrez alors ceci. Cliquez sur le bouton radio pour **JSON**.

![Adobe Experience Platform Data Collection SSF](./images/rl7gcp.png)

Configurez **Body** comme suit :

| CLÉ | VALEUR |
|--- |--- |
| customerECID | {{customerECID}} |
| pageName | {{pageName}} |
| eventTimestamp | {{eventTimestamp}} |

Vous verrez alors ceci. Cliquez sur **Conserver les modifications**.

![Adobe Experience Platform Data Collection SSF](./images/rl9gcp.png)

Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/rl10gcp.png)

Vous avez maintenant mis à jour votre règle existante dans une propriété de serveur de collecte de données Adobe Experience Platform. Accédez à **Flux de publication** pour publier vos modifications. Ouvrez votre bibliothèque de développement **Main** en cliquant sur **Modifier** comme indiqué.

![Adobe Experience Platform Data Collection SSF](./images/rl12gcp.png)

Cliquez sur le bouton **Ajouter toutes les ressources modifiées**, après lequel votre règle et votre élément de données apparaîtront dans cette bibliothèque. Cliquez ensuite sur **Enregistrer et créer pour le développement**. Vos modifications sont en cours de déploiement.

![Adobe Experience Platform Data Collection SSF](./images/rl13gcp.png)

Au bout de quelques minutes, vous verrez que le déploiement est terminé et prêt à être testé.

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## 2.5.3.4 Test de votre configuration

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Sur la page **Intégrations**, vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Lorsque vous ouvrez la vue Développeur de votre navigateur, vous pouvez examiner les demandes réseau comme indiqué ci-dessous. Lorsque vous utilisez le filtre **interagit**, vous verrez les requêtes réseau envoyées par le client de collecte de données Adobe Experience Platform à Adobe Edge.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook1.png)

Basculez votre vue vers votre fonction de cloud Google et accédez à **LOGS**. Vous devriez maintenant avoir une vue similaire à celle-ci, avec plusieurs entrées de journal affichées. Chaque fois que vous voyez **L’exécution de fonction démarrée**, cela signifie que le trafic entrant a été reçu dans votre fonction cloud Google.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook3gcp.png)

Mettons un peu à jour votre fonction pour qu’elle fonctionne avec les données entrantes et affiche les informations reçues du serveur de collecte de données Adobe Experience Platform. Accédez à **SOURCE** et cliquez sur **EDIT**.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook4gcp.png)

Dans l’écran suivant, cliquez sur **NEXT**.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf1.png)

Mettez à jour votre code comme suit :

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  console.log('>>>>> Function has started. The following information was received from Event Forwarding:');
  console.log(req.body);

  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

Vous aurez alors ceci. Cliquez sur **DEPLOY**.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf2.png)

Au bout de quelques minutes, votre fonction sera de nouveau déployée. Cliquez sur le nom de votre fonction pour l’ouvrir.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf3.png)

Sur votre site web de démonstration, accédez à un produit, par exemple **DEIRDRE RELAXED-FIT CAPRI**.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf3a.png)

Basculez votre vue vers votre fonction de cloud Google et accédez à **LOGS**. Vous devriez maintenant avoir une vue similaire à celle-ci, avec plusieurs entrées de journal affichées.

Pour chaque page vue de votre site web de démonstration, une nouvelle entrée de journal s’affiche dans les journaux de votre fonction Cloud Google, qui affiche les informations reçues.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf4.png)

Vous avez maintenant envoyé avec succès des données collectées par la collecte de données Adobe Experience Platform, en temps réel, à un point de terminaison de fonction Google Cloud. À partir de là, ces données peuvent être utilisées par n’importe quelle application Google Cloud Platform, comme BigQuery pour le stockage et la création de rapports, ou pour des cas pratiques d’apprentissage automatique.

Étape suivante : [2.5.5 Événements de transfert vers l’écosystème AWS](./ex5.md)

[Revenir au module 2.5](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../../overview.md)
