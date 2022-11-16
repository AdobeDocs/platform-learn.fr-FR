---
title: Collecte de données et transfert côté serveur en temps réel - Création et configuration d’une fonction cloud Google
description: Création et configuration d’une fonction Google Cloud
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d3678a30-6df9-44aa-a2fa-970127f75f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 1%

---

# 14.4 Création et configuration d’une fonction cloud Google

## 14.4.1 Création de la fonction cloud Google

Accédez à [https://console.cloud.google.com/](https://console.cloud.google.com/). Accédez à **Fonctions cloud**.

![GCP](./images/gcp1.png)

Vous verrez alors ceci. Cliquez sur **FONCTION CREATE**.

![GCP](./images/gcp2.png)

Vous verrez alors ceci.

![GCP](./images/gcp6.png)

Effectuez les choix suivants :

- **Nom de la fonction**: `--demoProfileLdap---event-forwarding`
- **Région**: sélectionner une région
- **Type de déclencheur**: select **HTTP**
- **Authentification**: select **Autoriser les appels non authentifiés**

Vous devriez maintenant avoir ceci. Cliquez sur **ENREGISTRER**.

![GCP](./images/gcp7.png)

Cliquez sur **SUIVANT**.

![GCP](./images/gcp8.png)

Vous verrez alors :

![GCP](./images/gcp9.png)

Effectuez les choix suivants :

- **Exécution**: select **Node.js 16** (ou plus récent)
- **Point d’entrée**: enter **helloAEP**

Cliquez sur **ACTIVER L’API** pour activer **API Cloud Build**. Vous verrez alors une nouvelle fenêtre. Dans cette nouvelle fenêtre, cliquez sur **ACTIVER** encore une fois.

![GCP](./images/gcp10.png)

Vous verrez alors ceci. Cliquez sur **Activer**.

![GCP](./images/gcp11.png)

Une fois **API Cloud Build** a été activé, vous verrez ceci.

![GCP](./images/gcp12.png)

Revenez à la **Fonction cloud**.
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

Vous verrez alors ceci. Accédez à **TRIGGER**. Vous verrez alors le **URL de déclenchement** qui est ce que vous utiliserez pour définir le point de terminaison dans Launch côté serveur.

![GCP](./images/gcp16.png)

Copiez l&#39;URL du déclencheur, qui se présente comme suit : **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**.

Dans les étapes suivantes, vous allez configurer le serveur de collecte de données Adobe Experience Platform pour diffuser des informations spécifiques sur **Pages vues** à votre fonction cloud Google. Au lieu de simplement transférer la charge utile complète en l’état, vous enverrez uniquement des éléments tels que **ECID**, **timestamp** et **Nom de la page** à votre fonction cloud Google.

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
- Nom de la page : **events.xdm.web.webPageDetails.name**

Allons maintenant sur le serveur de collecte de données Adobe Experience Platform pour configurer les éléments de données afin de rendre cela possible.

## 14.4.2 Mettez à jour la propriété Event Forwarding : Éléments de données

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) et accédez à **Transfert d’événement**. Recherchez la propriété Event Forwarding et cliquez dessus pour l’ouvrir.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/prop1.png)

Dans le menu de gauche, accédez à **Éléments de données**. Cliquez sur **Ajouter un élément de données**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/de1gcp.png)

Un nouvel élément de données à configurer s’affiche.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/de2gcp.png)

Effectuez la sélection suivante :

- Comme la variable **Nom**, saisissez **customerECID**.
- Comme la variable **Extension**, sélectionnez **Core**.
- Comme la variable **Type d’élément de données**, sélectionnez **Chemin**.
- Comme la variable **Chemin**, saisissez `arc.event.xdm.--aepTenantId--.identification.core.ecid`. En entrant ce chemin, vous allez filtrer le champ. **ecid** à partir de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

>[!NOTE]
>
>Dans les chemins ci-dessus et ci-dessous, une référence est faite à **arc**. **arc** signifie Adobe Resource Context et **arc** désigne toujours l’objet disponible le plus élevé disponible dans le contexte côté serveur. Des enrichissements et des transformations peuvent y être ajoutés. **arc** à l’aide des fonctions du serveur de collecte de données Adobe Experience Platform.
>
>Dans les chemins ci-dessus et ci-dessous, une référence est faite à **event**. **event** représente un événement unique et le serveur de collecte de données Adobe Experience Platform évalue toujours chaque événement individuellement. Parfois, une référence à **events** dans la charge utile envoyée par le SDK Web côté client, mais dans le serveur de collecte de données Adobe Experience Platform, chaque événement est évalué individuellement.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/gcdpde1.png)

Cliquez sur **Ajouter un élément de données**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/addde.png)

Un nouvel élément de données à configurer s’affiche.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/de2gcp.png)

Effectuez la sélection suivante :

- Comme la variable **Nom**, saisissez **eventTimestamp**.
- Comme la variable **Extension**, sélectionnez **Core**.
- Comme la variable **Type d’élément de données**, sélectionnez **Chemin**.
- Comme la variable **Chemin**, saisissez **arc.event.xdm.timestamp**. En entrant ce chemin, vous allez filtrer le champ. **timestamp** à partir de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/gcdpde2.png)

Cliquez sur **Ajouter un élément de données**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/addde.png)

Un nouvel élément de données à configurer s’affiche.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/de2gcp.png)

Effectuez la sélection suivante :

- Comme la variable **Nom**, saisissez **pageName**.
- Comme la variable **Extension**, sélectionnez **Core**.
- Comme la variable **Type d’élément de données**, sélectionnez **Chemin**.
- Comme la variable **Chemin**, saisissez **arc.event.xdm.web.webPageDetails.name**. En entrant ce chemin, vous allez filtrer le champ. **name** à partir de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/gcdpde3.png)

Ces éléments de données sont maintenant créés :

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/de3gcp.png)

## 14.4.3 Mettez à jour la propriété Event Forwarding : Mettre à jour une règle

Dans le menu de gauche, accédez à **Règles**. Dans l’exercice précédent, vous avez créé la règle **Toutes les pages**. Cliquez sur cette règle pour l’ouvrir.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl1gcp.png)

Vous ferez alors ceci. Cliquez sur le bouton **+** icône sous **Actions** pour ajouter une nouvelle action.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl2gcp.png)

Vous verrez alors ceci.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl4gcp.png)

Effectuez la sélection suivante :

- Sélectionnez la **Extension**: **Connecteur Adobe Cloud**.
- Sélectionnez la **Type d’action**: **Rendre l’appel de récupération**.

Cela devrait vous donner ceci : **Nom**: **Connecteur Adobe Cloud - Lancer un appel de récupération**. Vous devriez maintenant voir ceci :

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl5gcp.png)

Configurez ensuite les éléments suivants :

- Modifiez le protocole de requête de GET à **POST**
- Saisissez l’URL de la fonction Cloud Google que vous avez créée lors de l’une des étapes précédentes qui ressemble à ceci : **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**

Vous devriez maintenant avoir ceci. Ensuite, accédez à **Corps**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl6gcp.png)

Vous verrez alors ceci. Cliquez sur le bouton radio pour **JSON**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl7gcp.png)

Configurez la variable **Corps** comme suit :

| CLÉ | VALEUR |
|--- |--- |
| customerECID | {{customerECID}} |
| pageName | {{pageName}} |
| eventTimestamp | {{eventTimestamp}} |

Vous verrez alors ceci. Cliquez sur **Conserver les modifications**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl9gcp.png)

Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl10gcp.png)

Vous avez maintenant mis à jour votre règle existante dans une propriété de serveur de collecte de données Adobe Experience Platform. Accédez à **Flux de publication** pour publier vos modifications. Ouvrir votre bibliothèque de développement **Principal** en cliquant **Modifier** comme indiqué.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl12gcp.png)

Cliquez sur le bouton **Ajouter toutes les ressources modifiées** , après quoi votre règle et votre élément de données apparaîtront dans cette bibliothèque. Cliquez ensuite sur **Enregistrement et création pour le développement**. Vos modifications sont en cours de déploiement.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl13gcp.png)

Au bout de quelques minutes, vous verrez que le déploiement est terminé et prêt à être testé.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/rl14.png)

## 14.3.4 Test de votre configuration

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../module0/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../module0/images/web1.png)

Sur le **Intégrations** , vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../module0/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../module0/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../module0/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../module0/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../module0/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../module0/images/web7.png)

Lorsque vous ouvrez la vue Développeur de votre navigateur, vous pouvez examiner les demandes réseau comme indiqué ci-dessous. Lorsque vous utilisez le filtre **interagir**, vous verrez les requêtes réseau envoyées par le client de collecte de données Adobe Experience Platform à Adobe Edge.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook1.png)

Basculez votre vue vers votre fonction de cloud Google et accédez à **LOGS**. Vous devriez maintenant avoir une vue similaire à celle-ci, avec plusieurs entrées de journal affichées. Chaque fois que vous voyez **Exécution de la fonction démarrée**, cela signifie que le trafic entrant a été reçu dans votre fonction cloud Google.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook3gcp.png)

Mettons un peu à jour votre fonction pour qu’elle fonctionne avec les données entrantes et affiche les informations reçues du serveur de collecte de données Adobe Experience Platform. Accédez à **SOURCE** et cliquez sur **MODIFIER**.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook4gcp.png)

Dans l’écran suivant, cliquez sur **SUIVANT**.

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

Sur votre site web de démonstration, accédez à un produit, par exemple **CAPRI DÉIRDRE RELAXED-FIT**.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf3a.png)

Basculez votre vue vers votre fonction de cloud Google et accédez à **LOGS**. Vous devriez maintenant avoir une vue similaire à celle-ci, avec plusieurs entrées de journal affichées.

Pour chaque page vue de votre site web de démonstration, une nouvelle entrée de journal s’affiche dans les journaux de votre fonction Cloud Google, qui affiche les informations reçues.

![Configuration de la collecte de données Adobe Experience Platform](./images/gcf4.png)

Vous avez maintenant envoyé avec succès des données collectées par la collecte de données Adobe Experience Platform, en temps réel, à un point de terminaison de fonction Google Cloud. À partir de là, ces données peuvent être utilisées par n’importe quelle application Google Cloud Platform, comme BigQuery pour le stockage et la création de rapports, ou pour des cas pratiques d’apprentissage automatique.

Étape suivante : [14.5 Événements de transfert vers l’écosystème AWS](./ex5.md)

[Revenir au module 14](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../overview.md)
