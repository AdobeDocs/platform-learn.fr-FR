---
title: Real-Time CDP - Créez une audience et effectuez une action - Envoyez votre audience à DV360
description: Real-Time CDP - Créez une audience et effectuez une action - Envoyez votre audience à DV360
kt: 5342
doc-type: tutorial
exl-id: 5cdb1f66-580c-4b3f-ada6-e224762eab59
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 3%

---

# 2.3.3 Agir : envoyez votre audience à DV360

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la [!UICONTROL sandbox] appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Parcourir**. Vous verrez alors la destination **DV360**. Cliquez sur le **de 3 points...**, puis sur **Activer les audiences**.

![ RTCDP ](./images/rtcdpmenudest.png)

Dans la liste des audiences disponibles, sélectionnez l’audience que vous avez créée dans l’exercice précédent. Cliquez sur **Suivant**.

![ RTCDP ](./images/rtcdpcreatedest3.png)

Sur la page **Planification de l’audience**, cliquez sur **Suivant**.

![ RTCDP ](./images/rtcdpcreatedest4.png)

Enfin, sur la page **Réviser**, cliquez sur **Terminer**.

![ RTCDP ](./images/rtcdpcreatedest5.png)

Votre audience est maintenant liée à Google DV360. Chaque fois qu’un client se qualifie pour cette audience, un signal est envoyé à Google DV360 pour l’inclure dans l’audience côté DV360 Google.

## Étapes suivantes

Accédez à [2.3.4 Prendre des mesures : envoyer votre audience vers une destination S3](./ex4.md){target="_blank"}

Revenez à [Real-time CDP - Créer une audience et prendre des mesures](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
