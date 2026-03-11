---
title: Mise à l’échelle des fragments de contenu avec le serveur ChatGPT et MCP
description: Mise à l’échelle des fragments de contenu avec le serveur ChatGPT et MCP
kt: 5342
doc-type: tutorial
exl-id: b7105351-e9de-4b2c-b3d7-2d4c8627f852
source-git-commit: a57050bf40105a0b0c6d4ce615aa640e878ece12
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 2%

---

# 1.6.3 Mise à l’échelle des fragments de contenu avec le serveur ChatGPT et MCP

>[!IMPORTANT]
>
>Pour réaliser cet exercice, vous devez avoir accès à un environnement AEM Sites et Assets CS avec services de développement intégré (EDS) fonctionnel, et les différents agents AEM doivent être activés pour l’organisation IMS que vous utilisez.
>
>Si vous ne disposez pas encore d’un tel environnement, passez à l’exercice [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Sites et Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.6.3.1 Créer un modèle de fragment de contenu

Revenez à votre environnement de création Adobe Experience Manager, sur **Outils**, puis accédez à **Navigateur de configuration**.

![Agents AEM](./images/aemagentscfm1.png)

Cliquez sur **Créer**.

![Agents AEM](./images/aemagentscfm2.png)

Utilisez des `Content Fragments` pour les champs **Titre** et **Nom**.

Assurez-vous que les options **Modèles de fragment de contenu** et **Requêtes persistantes GraphQL** sont toutes deux activées.

Cliquez sur **Créer**.

![Agents AEM](./images/aemagentscfm3.png)

Revenez à votre environnement de création Adobe Experience Manager, puis accédez à **Fragments de contenu**.

![Agents AEM](./images/aemagentscf1.png)

Accédez à **Modèles de fragment de contenu**, sélectionnez votre configuration **Fragments de contenu** puis cliquez sur **Créer**.

![Agents AEM](./images/aemagentscfm4.png)

Utilisez le nom `--aepUserLdap-- - CitiSignal CFM`. Cliquez sur **Créer et ouvrir**.

![Agents AEM](./images/aemagentscfm5.png)

Vous devriez alors voir ceci. Faites glisser et déposez un champ **texte monoligne** sur la zone de travail.

![Agents AEM](./images/aemagentscfm6.png)

Remplacez le champ **Libellé du champ** par `Header`.

![Agents AEM](./images/aemagentscfm7.png)

Revenez à **Types de données**. Faites glisser et déposez un champ **texte monoligne** sur la zone de travail.

![Agents AEM](./images/aemagentscfm8.png)

Remplacez le champ **Libellé du champ** par `Subheader`.

![Agents AEM](./images/aemagentscfm9.png)

Revenez à **Types de données**. Faites glisser et déposez un champ **texte multiligne** sur la zone de travail.

![Agents AEM](./images/aemagentscfm10.png)

Remplacez le champ **Libellé du champ** par `Detail Description`.

![Agents AEM](./images/aemagentscfm11.png)

Revenez à **Types de données**. Faites glisser et déposez un champ **texte monoligne** sur la zone de travail.

![Agents AEM](./images/aemagentscfm12.png)

Remplacez le champ **Libellé du champ** par `CTA Text`.

![Agents AEM](./images/aemagentscfm13.png)

Revenez à **Types de données**. Faites glisser et déposez un champ **texte monoligne** sur la zone de travail.

![Agents AEM](./images/aemagentscfm14.png)

Remplacez le champ **Libellé du champ** par `CTA Link`. Cliquez sur **Enregistrer**.

![Agents AEM](./images/aemagentscfm15.png)

Vous devriez alors voir ceci.

![Agents AEM](./images/aemagentscfm16.png)

Sélectionnez votre modèle de fragment de contenu et cliquez sur **Publier**.

![Agents AEM](./images/aemagentscfm17.png)

Cliquez sur **Publier**.

![Agents AEM](./images/aemagentscfm18.png)

## 1.6.3.2 Créer un fragment de contenu

Revenez à votre environnement de création Adobe Experience Manager, puis accédez à **Fragments de contenu**.

![Agents AEM](./images/aemagentscf1.png)

Vous devriez alors voir ceci. Cliquez sur **Créer** puis sélectionnez **Dossier**.

![Agents AEM](./images/aemagentscf2.png)

Saisissez le titre : `--aepUserLdap-- - CF`. Cliquez sur **Créer**.

![Agents AEM](./images/aemagentscf3.png)

Revenez à votre environnement de création Adobe Experience Manager, puis accédez à **Assets**.

![Agents AEM](./images/aemagentscfmm1.png)

Accédez à **Fichiers**.

![Agents AEM](./images/aemagentscfmm2.png)

Sélectionnez le dossier que vous venez de créer, qui doit être nommé `--aepUserLdap-- - CF` et cliquez sur **Propriétés**.

![Agents AEM](./images/aemagentscfmm3.png)

Accédez à **Services cloud** puis cliquez sur l’icône **dossier**.

![Agents AEM](./images/aemagentscfmm4.png)

Sélectionnez la configuration cloud que vous avez créée précédemment et qui doit être nommée **Fragments de contenu**. Cliquez sur **Sélectionner**.

![Agents AEM](./images/aemagentscfmm5.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer et fermer**.

![Agents AEM](./images/aemagentscfmm6.png)

Revenez à votre environnement de création Adobe Experience Manager, puis accédez à **Fragments de contenu**.

![Agents AEM](./images/aemagentscf1.png)

Vous devriez alors voir ceci. Cliquez sur **Créer** puis sélectionnez **Fragment de contenu**.

![Agents AEM](./images/aemagentscf4.png)

Sélectionnez le **modèle de fragment de contenu** que vous avez créé précédemment et qui doit être nommé `--aepUserLdap-- - CitiSignal CFM`. Utilisez le nom `--aepUserLdap-- CitiSignal Fiber Max`.

Cliquez sur **Créer et ouvrir**.

![Agents AEM](./images/aemagentscf5.png)

Vous devriez alors voir ceci.

![Agents AEM](./images/aemagentscf5a.png)

Renseignez les champs comme suit :

- **En-tête** : `CitiSignal Fiber Max`
- **Sous-en-tête** : `Experience high speed internet now`
- **Description détaillée** :

```
Experience the future of connectivity with CitiSignal Fiber Max, the ultimate solution for high-speed internet. Designed for homes and businesses that demand performance, Fiber Max delivers blazing-fast fiber speeds, ensuring seamless streaming, ultra-responsive gaming, and crystal-clear video calls.

Key Features:

Unmatched Speed: Enjoy lightning-fast downloads and uploads powered by cutting-edge fiber technology.
Reliable Performance: Consistent connectivity for work, entertainment, and everything in between.
Future-Ready: Built to handle the growing demands of smart homes and digital lifestyles.
Unlimited Potential: No data caps, no throttling—just pure speed.
Why Choose CitiSignal Fiber Max? Stay ahead with internet that works as hard as you do. Whether you’re powering a remote office or streaming in 4K, Fiber Max ensures you never miss a beat.
```

**Texte CTA** : `Upgrade now by signing your new contract!`
**Lien CTA** : `https://techinsiders68.adobedemosystem.com/`

Cliquez sur **Publier** puis sélectionnez **Maintenant**.

![Agents AEM](./images/aemagentscf6.png)

Cliquez sur **Publier**.

![Agents AEM](./images/aemagentscf7.png)

## 1.6.3.3 Configurer le serveur MCP dans ChatGPT

>[!NOTE]
>
>L’utilisation de Adobe Marketing Agent dans ChatGPT nécessite ce qui suit :
>- une version payante du ChatGPT Enterprise d’OpenAI
>- en utilisant le client web ChatGPT Enterprise

Accédez à [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} et connectez-vous à l’aide des détails de votre compte. Une fois la connexion effectuée, vous devriez voir ceci. Cliquez sur votre nom d’utilisateur, puis sélectionnez **Paramètres**.

![ChatGPT](./images/chatgpt2.png)

Accédez à **Applications** puis sélectionnez **Paramètres avancés**.

![ChatGPT](./images/chatgpt3.png)

Activez le **mode Développeur** puis cliquez sur **Précédent**.

![ChatGPT](./images/chatgpt4.png)

Cliquez sur **Créer une application**.

![ChatGPT](./images/chatgpt5.png)

Renseignez les champs comme suit :

- **Nom** : `aem`
- **URL du serveur MCP** : `https://mcp.adobeaemcloud.com/adobe/mcp/content`
- **Authentification** : `OAuth`

Cochez la case **Je comprends et je souhaite continuer**.

Cliquez sur **Créer**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT va maintenant essayer de se connecter à votre compte Adobe. Sélectionnez **Autoriser l’accès** puis vous devrez vous connecter à l’aide de votre compte Adobe.

Une fois la connexion établie, vous devriez voir que votre Adobe Marketing Agent est maintenant connecté.

![ChatGPT](./images/chatgpt8.png)

## 1.6.3.4 Utiliser le serveur AEM MCP dans ChatGPT

Fermez cette fenêtre.

![Agent Orchestrator](./images/chatgpt8.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **+**, accédez à **Plus** puis sélectionnez **aem**.

![Agent Orchestrator](./images/chatgpt10.png)

Saisissez l’invite suivante et cliquez sur **Envoyer**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Agent Orchestrator](./images/chatgpt11.png)

Vous devriez alors voir quelque chose comme ça. Saisissez l’invite suivante et cliquez sur **Envoyer**.

```
use the author url https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/ from now on
```

![Agent Orchestrator](./images/chatgpt12.png)

Vous devriez alors voir quelque chose comme ça. Saisissez l’invite suivante et cliquez sur **Envoyer**.

```
find the content fragment --aepUserLdap-- - CitiSignal Fiber Max and make a variation called --aepUserLdap-- - CitiSignal Fiber Max (FR), then translate all fields into french
```

![Agent Orchestrator](./images/chatgpt13.png)

Cliquez sur **CreateFragmentVariation**.

![Agent Orchestrator](./images/chatgpt14.png)

Cliquez sur **UpdateFragment**.

![Agent Orchestrator](./images/chatgpt15.png)

Vous devriez alors voir ceci. Votre variation de fragment a été créée avec succès.

![Agent Orchestrator](./images/chatgpt16.png)

Votre nouvelle variation apparaît désormais également dans l’interface utilisateur d’AEM.

![Agent Orchestrator](./images/chatgpt17.png)

Ensuite, utilisez le ChatGPT pour traduire votre fragment de contenu en davantage de variations. Saisissez l’invite suivante et cliquez sur **Envoyer**.

```
now do the same thing for the 5 top country's languages that CitiSignal does business with
```

![Agent Orchestrator](./images/chatgpt18.png)

Confirmez votre choix de langue.

![Agent Orchestrator](./images/chatgpt23.png)

Cliquez sur **CreateFragmentVariation**.

![Agent Orchestrator](./images/chatgpt22.png)

Cliquez sur **UpdateFragment**.

![Agent Orchestrator](./images/chatgpt24.png)

Répétez ce processus pour chacune des langues que vous avez sélectionnées. Une fois cette opération terminée, vous devriez voir quelque chose comme ceci :

![Agent Orchestrator](./images/chatgpt26.png)

Revenez à l’interface utilisateur d’AEM et actualisez votre écran. Vous pouvez maintenant voir vos nouvelles variations dans votre fragment de contenu.

![Agent Orchestrator](./images/chatgpt27.png)

## Étapes suivantes

Revenir à [AEM et agents](./aemagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
