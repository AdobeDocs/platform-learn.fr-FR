---
title: Real-time CDP - Créez une audience et effectuez une action - Configurez une destination Advertising telle que Google DV360
description: Real-time CDP - Créez une audience et effectuez une action - Configurez une destination Advertising telle que Google DV360
kt: 5342
doc-type: tutorial
exl-id: 2498c80f-8ba8-4563-ac37-52f461f706f4
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 2.3.2 Configuration d’une destination Advertising telle que Google DV360

>[!IMPORTANT]
>
>Le contenu ci-dessous est en partie destiné à servir d’information : si une telle destination existe déjà dans votre instance, vous n’avez **PAS** à configurer une nouvelle destination pour DV360. La destination a déjà été créée dans ce cas et vous pouvez l’utiliser dans l’exercice suivant.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la [!UICONTROL sandbox] appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Catalogue**. Vous verrez ensuite le **Catalogue des destinations**.

![&#x200B; RTCDP &#x200B;](./images/rtcdp.png)

Dans **Destinations**, cliquez sur **Google Display &amp; Video 360** puis sur **+ Configurer**.

![&#x200B; RTCDP &#x200B;](./images/rtcdpgoogle.png)

Tu verras ça. Cliquez sur **Se connecter à la destination**.

![&#x200B; RTCDP &#x200B;](./images/rtcdpgooglecreate1.png)

Dans l’écran suivant, vous pouvez configurer la destination vers Google DV360.

![&#x200B; RTCDP &#x200B;](./images/rtcdpgooglecreatedest.png)

Saisissez une valeur dans les champs **Nom** et **Description**.

Le champ **ID de compte** est l’**ID publicitaire** du compte DV360. Vous pouvez le trouver ici :

![&#x200B; RTCDP &#x200B;](./images/rtcdpgoogledv360advid.png)

Le **Type de compte** doit être défini sur **Inviter un annonceur**.

Maintenant, vous avez ceci. Cliquez sur **Suivant**.

![&#x200B; RTCDP &#x200B;](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google doit placer Adobe sur la liste autorisée pour que Adobe Experience Platform envoie des données aux DV360 Google. Contactez votre gestionnaire de compte Google pour activer ce flux de données.

Après avoir créé la destination, vous verrez ceci. Vous pouvez éventuellement sélectionner une politique de gouvernance des données. Cliquez ensuite sur **Enregistrer et quitter**.

![&#x200B; RTCDP &#x200B;](./images/rtcdpcreatedest1.png)

Une liste des destinations disponibles s’affiche alors.
Dans l’exercice suivant, vous allez connecter l’audience que vous avez créée dans l’exercice précédent à la destination DV360 de Google.

## Étapes suivantes

Accédez à [2.3.3 Prendre des mesures : envoyer votre audience à DV360](./ex3.md){target="_blank"}

Revenez à [Real-time CDP - Créer une audience et prendre des mesures](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
