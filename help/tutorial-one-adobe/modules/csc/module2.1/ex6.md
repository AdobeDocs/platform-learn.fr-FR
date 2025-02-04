---
title: Plug-in AEM CS - MarTech
description: Plug-in AEM CS - MarTech
kt: 5342
doc-type: tutorial
exl-id: 8a2c6327-8d3d-4048-bf89-9d4371e18e1b
source-git-commit: 311dd09c901f1be07a4ee20cdc1f4597bd9a9410
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# 2.1.6 Plug-in AEM Edge Delivery Services MarTech

Le plug-in AEM MarTech permet de configurer rapidement une pile MarTech complète pour votre projet AEM.

>[!NOTE]
>
>Ce plug-in est actuellement disponible pour les clients en collaboration avec l’ingénierie AEM dans le cadre de projets de co-innovation. Vous trouverez plus d’informations sur [https://github.com/adobe-rnd/aem-martech](https://github.com/adobe-rnd/aem-martech).

Accédez au dossier que vous utilisez pour votre référentiel GitHub **citisignal**. Cliquez avec le bouton droit sur le nom du dossier, puis sélectionnez **Nouveau terminal dans le dossier**.

![ AEMCS ](./images/mtplugin1.png)

Tu verras ça. Collez la commande suivante et appuyez sur **entrée**.

```
git subtree add --squash --prefix plugins/martech https://github.com/adobe/aem-experimentation.git main
```

Vous devriez alors voir ceci.

![ AEMCS ](./images/mtplugin3.png)

Accédez au dossier que vous utilisez pour votre référentiel **citisignal** GitHub, ouvrez le dossier **plugins**. Vous devriez maintenant voir un dossier nommé **martech**.

![ AEMCS ](./images/mtplugin4.png)


Dans Visual Studio Code, ouvrez le fichier **head.html**. Copiez le code ci-dessous et collez-le dans le fichier **head.html**.

```javascript
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/index.js"/>
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/alloy.min.js"/>
<link rel="preconnect" href="https://edge.adobedc.net"/>
<!-- change to adobedc.demdex.net if you enable third party cookies -->
```

Enregistrez vos modifications.

![ AEMCS ](./images/mtplugin5.png)

Dans Visual Studio Code, accédez au dossier **scripts** et ouvrez le fichier **scripts.js**. Copiez le code ci-dessous et collez-le dans le fichier **scripts.js**, sous les scripts d’importation existants.

```javascript
import {
  initMartech,
  updateUserConsent,
  martechEager,
  martechLazy,
  martechDelayed,
} from '../plugins/martech/src/index.js';
```

Enregistrez vos modifications.

![ AEMCS ](./images/mtplugin6.png)

```javascript
const isConsentGiven = true;
  const martechLoadedPromise = initMartech(
    // The WebSDK config
    // Documentation: https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview#configure-js
    {
      datastreamId: "045c5ee9-468f-47d5-ae9b-a29788f5948f",
      orgId: "907075E95BF479EC0A495C73@AdobeOrg",
      onBeforeEventSend: (payload) => {
        // set custom Target params 
        // see doc at https://experienceleague.adobe.com/en/docs/platform-learn/migrate-target-to-websdk/send-parameters#parameter-mapping-summary
        payload.data.__adobe.target ||= {};

        // set custom Analytics params
        // see doc at https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping
        payload.data.__adobe.analytics ||= {};
      },

      // set custom datastream overrides
      // see doc at:
      // - https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/datastream-overrides
      // - https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides
      edgeConfigOverrides: {
        // Override the datastream id
        // datastreamId: '...'

        // Override AEP event datasets
        // com_adobe_experience_platform: {
        //   datasets: {
        //     event: {
        //       datasetId: '...'
        //     }
        //   }
        // },

        // Override the Analytics report suites
        // com_adobe_analytics: {
        //   reportSuites: ['...']
        // },

        // Override the Target property token
        // com_adobe_target: {
        //   propertyToken: '...'
        // }
      },
    },
    // The library config
    {
      launchUrls: ["https://assets.adobedtm.com/b754ed1bed61/b9f7c7c484de/launch-28b548849fb9.min.js"],
      personalization: !!getMetadata('target') && isConsentGiven,
    },
  );
```

![ AEMCS ](./images/mtplugin8.png)

![ AEMCS ](./images/mtplugin7.png)

```javascript
if (main) {
    decorateMain(main);
    await Promise.all([
      martechLoadedPromise.then(martechEager),
      waitForLCP(LCP_BLOCKS),
    ]);
  }
```

![ AEMCS ](./images/mtplugin10.png)

```javascript
await martechLazy();
```

![ AEMCS ](./images/mtplugin9.png)

```javascript
window.setTimeout(() => {
    martechDelayed();
    return import('./delayed.js');
  }, 3000);
```

![ AEMCS ](./images/mtplugin11.png)


![ AEMCS ](./images/mtplugin12.png)


![ AEMCS ](./images/mtplugin13.png)

Vous pourrez désormais afficher les modifications apportées à votre site web en accédant à `main--citisignal--XXX.aem.page/us/en` et/ou `main--citisignal--XXX.aem.live/us/en`, après avoir remplacé XXX par votre compte utilisateur GitHub, ce qui est `woutervangeluwe` dans cet exemple.

Dans cet exemple, l’URL complète devient :
`https://main--citisignal--woutervangeluwe.aem.page/us/en` et/ou `https://main--citisignal--woutervangeluwe.aem.live/us/en`

Étape suivante : [Résumé et avantages](./summary.md){target="_blank"}

[Retour au module 2.1](./aemcs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
