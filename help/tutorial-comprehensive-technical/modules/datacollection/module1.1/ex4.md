---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Collecte de données web côté client
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Collecte de données web côté client
kt: 5342
doc-type: tutorial
exl-id: dce7f1b5-72ca-41b2-9aa8-41c13ce25c82
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# 1.1.4 Collecte de données web côté client

## Valider les données de la requête

### Installation d’Adobe Experience Platform Debugger

Experience Platform Debugger est une extension disponible pour les navigateurs Chrome et Firefox qui vous permet de voir la technologie Adobe mise en œuvre dans vos pages web. Installez la version correspondant au navigateur de votre choix :

- [Extension Firefox ](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)

- [Extension Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé le débogueur auparavant (et que celui-ci est différent du débogueur Adobe Experience Cloud précédent), vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on&enablevpops)

Étant donné que vous allez charger le site web de démonstration en mode incognito, vous devez vous assurer que le débogueur Experience Platform est également disponible en mode incognito. Pour ce faire, accédez à **chrome://extensions** dans votre navigateur et ouvrez l’extension Experience Platform Debugger.

Vérifiez que ces 2 paramètres sont activés :

- Mode Développeur
- Autoriser dans incognito

![Page d&#39;accueil d&#39;EXP News](./images/ext1.png)

### Ouvrir le site web de démonstration

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **de 3 points...** sur le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN ](./images/web8.png)

Vous verrez ensuite votre site web de démonstration s’ouvrir. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN ](./../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur en mode privé.

![DSN ](./../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Il vous sera ensuite demandé de vous connecter à l’aide de votre Adobe ID.

![DSN ](./../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez votre type de compte et terminez le processus de connexion.

![DSN ](./../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur en mode privé. Pour chaque démonstration, vous devez utiliser une nouvelle fenêtre de navigateur en mode privé pour charger l’URL de votre site web de démonstration.

![DSN ](./../../gettingstarted/gettingstarted/images/web7.png)

### Utilisez Experience Platform Debugger pour afficher les appels allant à Edge

Assurez-vous que le site web de démonstration est ouvert et cliquez sur l’icône de l’extension Experience Platform Debugger .

![Page d&#39;accueil d&#39;EXP News](./images/ext2.png)

Le débogueur s’ouvre et affiche les détails de l’implémentation créée dans votre propriété de collecte de données Adobe Experience Platform. N’oubliez pas que vous déboguez l’extension et les règles que vous venez de modifier.

Cliquez sur le bouton **[!UICONTROL Se connecter]** en haut à droite pour vous authentifier. Si un onglet de navigateur est déjà ouvert avec l’interface de collecte de données de Adobe Experience Platform, l’étape d’authentification sera automatique et vous n’aurez pas à saisir à nouveau votre nom d’utilisateur et votre mot de passe.

![ Débogueur AEP ](./images/validate2.png)

Vous serez alors connecté au débogueur.

![ Débogueur AEP ](./images/validate2ab.png)

Appuyez sur le bouton recharger de votre site web de démonstration pour connecter le débogueur à cet onglet spécifique.

![ Débogueur AEP ](./images/validate2a.png)

Vérifiez que le débogueur est **[!UICONTROL connecté à l’accueil]** comme illustré ci-dessus, puis cliquez sur l’icône **[!UICONTROL verrouiller]** pour verrouiller le débogueur sur le site web de démonstration. Si vous ne le faites pas, le débogueur continue de basculer pour exposer les détails d’implémentation de l’onglet du navigateur dans lequel le focus se trouve, ce qui peut prêter à confusion. Une fois le débogueur verrouillé, l’icône devient **Déverrouiller**.

![ Débogueur AEP ](./images/validate3.png)

Ensuite, accédez à n’importe quelle page du site web de démonstration, comme par exemple la page de catégorie **Plans**.

![Extension AEP Debugger Web SDK](./images/validate4.png)

Cliquez maintenant sur **[!UICONTROL Experience Platform Web SDK]** dans le volet de navigation de gauche, pour afficher le **[!UICONTROL Requêtes réseau]**.

Chaque requête contient une ligne **[!UICONTROL events]**.

![Extension AEP Debugger Web SDK](./images/validate5.png)

Cliquez pour ouvrir une ligne **[!UICONTROL événements]**. Notez comment vous pouvez voir l’événement **web.webpagedetails.pageViews**, ainsi que d’autres variables prêtes à l’emploi adhérant au format **Web SDK ExperienceEvent XDM**.

![Valeur des événements](./images/validate8.png)

Ces types de détails de requête sont également visibles dans l’onglet Réseau . Filtrez les requêtes avec **interaction** pour localiser les requêtes envoyées par Web SDK. Tous les détails de la payload XDM sont disponibles dans la section Payload :

![Onglet Réseau](./images/validate9.png)

Étape suivante : [1.1.5 Mise en œuvre d’Adobe Analytics et de Adobe Audience Manager](./ex5.md)

[Retour au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
