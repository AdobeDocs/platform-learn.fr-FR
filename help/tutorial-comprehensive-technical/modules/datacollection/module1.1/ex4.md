---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Collecte de données Web côté client
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Collecte de données Web côté client
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 1.1.4 Collecte de données Web côté client

## 1.1.4.1 Validation des données dans la requête

### Installation de l’Adobe Experience Platform Debugger

Le débogueur Experience Platform est une extension disponible pour les navigateurs Chrome et Firefox qui vous permet de voir la technologie d’Adobe mise en oeuvre dans vos pages web. Téléchargez la version de votre navigateur préféré :

- [Extension Firefox](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)

- [Extension Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé le débogueur auparavant (et que celui-ci est différent du débogueur Adobe Experience Cloud précédent), vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Étant donné que vous allez charger le site web de démonstration en mode incognito, vous devez vous assurer que l’Experience Platform Debugger est également disponible en mode incognito. Pour ce faire, accédez à **chrome://extensions** dans votre navigateur et ouvrez l’extension Experience Platform Debugger.

Vérifiez que ces deux paramètres sont activés :

- Mode Développeur
- Autoriser dans incognito

![Page d’accueil EXP News](./images/ext1.png)

### Ouvrir le site web de démonstration

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

Sur la page **Screens**, cliquez sur **Exécuter**.

![DSN](./images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

### Utilisez l’Experience Platform Debugger pour afficher les appels allant à Edge

Assurez-vous que le site web de démonstration est ouvert et cliquez sur l’icône de l’extension Debugger Experience Platform.

![Page d’accueil EXP News](./images/ext2.png)

Le débogueur s’ouvre et affiche les détails de l’implémentation créée dans votre propriété de collecte de données Adobe Experience Platform. N’oubliez pas que vous déboguez l’extension et les règles que vous venez de modifier.

Cliquez sur le bouton **[!UICONTROL Se connecter]** en haut à droite pour vous authentifier. Si un onglet de navigateur est déjà ouvert avec l’interface Collecte de données de Adobe Experience Platform, l’étape d’authentification sera automatique et vous n’aurez plus à saisir votre nom d’utilisateur et votre mot de passe.

![Débogueur AEP](./images/validate2.png)

Appuyez sur le bouton recharger de votre site web de démonstration pour connecter le débogueur à cet onglet spécifique.

![Débogueur AEP](./images/validate2a.png)

Vérifiez que le débogueur est **[!UICONTROL connecté à l’accueil]** comme illustré ci-dessus, puis cliquez sur l’icône **[!UICONTROL lock]** pour verrouiller le débogueur sur le site web de démonstration. Si vous ne le faites pas, le débogueur continuera de changer pour afficher les détails de mise en oeuvre de tout onglet de navigateur actif, ce qui peut être déroutant.

![Débogueur AEP](./images/validate3.png)

Ensuite, accédez à n’importe quelle page du site web de démonstration comme, par exemple, la page de catégorie **Men** .

![Extension AEP Debugger SDK Web AEP](./images/validate4.png)

Cliquez maintenant sur **[!UICONTROL SDK Web Experience Platform]** dans le volet de navigation de gauche pour afficher les **[!UICONTROL requêtes réseau]**.

Chaque requête contient une ligne **[!UICONTROL events]**.

![Extension AEP Debugger SDK Web AEP](./images/validate5.png)

Cliquez pour ouvrir la ligne **[!UICONTROL events]** . Notez comment vous pouvez voir l’événement **web.webpagedetails.pageViews**, ainsi que d’autres variables prêtes à l’emploi conformes au format **Web SDK ExperienceEvent XDM**.

![Valeur des événements](./images/validate8.png)

Ces types de détails de requête sont également visibles dans l’onglet Réseau. Filtrez les requêtes avec **interaction** pour localiser les requêtes envoyées par le SDK Web. Vous trouverez tous les détails de la charge utile XDM dans les en-têtes de charge utile de requête :

![Onglet Réseau](./images/validate9.png)

Étape suivante : [1.1.5 Mise en oeuvre d’Adobe Analytics et de Adobe Audience Manager](./ex5.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
