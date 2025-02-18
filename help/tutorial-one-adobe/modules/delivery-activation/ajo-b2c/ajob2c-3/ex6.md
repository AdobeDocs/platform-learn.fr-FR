---
title: Offer Decisioning - Testez votre décision à l’aide de l’API
description: Tester votre décision à l’aide de l’API
kt: 5342
doc-type: tutorial
exl-id: 52f90b9f-32ea-49c2-af5d-8742ca8b3b4e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 3.3.6 Tester votre décision à l’aide de l’API

## 3.3.6.1 Utiliser l’API Offer Decisioning à l’aide de Postman

>[!IMPORTANT]
>
>Si vous êtes un employé d&#39;Adobe, veuillez suivre les instructions ici pour utiliser [PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md).

Téléchargez [cette collection Postman pour Offer Decisioning](./../../../../assets/postman/postman_offer-decisioning.zip) sur votre bureau et décompressez-la. Voici ce que vous obtiendrez :

API ![OD](./images/unzip.png)

Ce fichier se trouve maintenant sur votre bureau :

- `_AJO- Decisioning Service.postman_collection.json`

Dans [Exercice 2.1.3 - Authentification Postman à Adobe I/O](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/ex3.md) vous avez installé Postman. Vous devrez réutiliser Postman pour cet exercice.

Ouvrez Postman et importez le fichier `_AJO- Decisioning Service.postman_collection.json`. Cette collection sera alors disponible dans Postman.

![Nouvelle intégration Adobe I/O](./images/postmanui.png)

Vous disposez désormais de tout ce dont vous avez besoin dans Postman pour commencer à interagir avec Adobe Experience Platform par le biais des API.

Avant de pouvoir utiliser les API ci-dessous, veillez à vous authentifier à nouveau à l’aide de la collection **Adobe IO - OAuth** que vous avez configurée dans l’exercice 2.1.3.

![Nouvelle intégration Adobe I/O](./images/postmanui1.png)


### 3.3.6.2 Obtenir des offres pour le profil client

Cliquez pour ouvrir la demande **POST - Obtenir des offres pour le profil client**. La première chose à mettre à jour est la variable **Header** pour **x-sandbox-name**. Vous devriez le définir sur `--aepSandboxName--`.

API ![OD](./images/api23.png)

Un certain nombre de champs doivent être mis à jour pour cette requête. Accédez à **Corps**.

- **xdm:placementId**
- **xdm:activityId**
- **xdm:id**
- **xdm:itemCount** (remplacez-le par une valeur de votre choix)

API ![OD](./images/api24.png)

Le champ **xdm:activityId** doit être rempli. Vous pouvez la récupérer dans l’interface utilisateur de Adobe Experience Platform, comme indiqué ci-dessous.

API ![OD](./images/activityid.png)

Le champ **[!UICONTROL xdm:placementId]** doit être rempli. Vous pouvez la récupérer dans l’interface utilisateur de Adobe Experience Platform, comme indiqué ci-dessous. Dans l&#39;exemple ci-dessous, vous pouvez voir l&#39;emplacement placementId **[!UICONTROL Web - Image]**.

API ![OD](./images/placementid.png)

Dans le champ **xdm:id**, saisissez l’adresse e-mail du profil client pour lequel vous souhaitez demander une offre. Une fois toutes les valeurs définies, cliquez sur **[!UICONTROL Envoyer]**.

API ![OD](./images/api24a.png)

Enfin, vous verrez le résultat du type d’offre personnalisée et les ressources qui doivent être affichées pour ce client. Dans cet exemple, 2 éléments ont été demandés et, comme vous pouvez le constater, 2 offres personnalisées ont été renvoyées. 1 offre pour Apple Watch et une autre pour Galaxy Watch 7.

API ![OD](./images/api25.png)

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à [ Résumé et avantages ](./summary.md){target="_blank"}

Revenir à [Offer Decisioning](offer-decisioning.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
